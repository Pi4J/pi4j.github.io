---
title: "RISC-V in Pi4J V5"
date: 2026-07-20
tags: ["FFM", "RISC-V", "GPIO", "I2C"]
---

2026-07-20, by Nick Gritsenko 

## RISC-V Support Landing in Pi4J V5

### Pi4J's FFM Provider Now Runs on RISC-V

[Pull request #697](https://github.com/Pi4J/pi4j/pull/697) by [@DigitalSmile](https://github.com/DigitalSmile), merged on July 18, adds RISC-V support to the current SNAPSHOT [FFM provider](/documentation/providers/ffm/), the modern Pi4J backend built on Java's Foreign Function & Memory API. The change lands on `main`, which is building towards **Pi4J 5.0.0**, so support for RISC-V boards will available from V5 onward, alongside the usual ARM64 hosts.

This builds on the [recent Banana Pi experiments](/blog/2026/20260717-java-on-banana-pi-arm-riscv/), which already showed Java and Pi4J running on a RISC-V board through manual GPIO offset calculations. The [x86 vs ARM vs RISC-V](/sbc/x86-arm-riscv/) overview on this site could previously only say "not sure yet if Pi4J works on RISC-V" — as of this PR, it does.

#### The fix: stop guessing the architecture, ask the linker instead

The FFM provider talks to `libi2c` through Java's foreign linker, and until now it located that native library itself. `Pi4JArchitectureGuess` hardcoded two paths: `/usr/lib/x86_64-linux-gnu/` for `amd64` and `/usr/lib/aarch64-linux-gnu/` for `aarch64`. Any other `os.arch`, including `riscv64`, hit an `UnsupportedOperationException`-style rejection before a single GPIO pin could be touched.

The PR deletes that class and replaces it with `Pi4JNativeLibrary`, which hands the job to the OS's own dynamic linker instead of maintaining a per-architecture switch statement:

```java
public static SymbolLookup load(String baseName, Arena arena) {
    assertLinuxHost();
    var candidates = libraryCandidates(baseName);
    for (var name : candidates) {
        try {
            return SymbolLookup.libraryLookup(name, arena);
        } catch (IllegalArgumentException e) {
            // try the next candidate
        }
    }
    throw new Pi4JException("Could not load native library '" + baseName + "' ...");
}
```

`SymbolLookup.libraryLookup(String, Arena)` calls straight into `dlopen`, which already searches `ld.so.cache`, `LD_LIBRARY_PATH`, and the standard multiarch directories for whatever architecture it's running on. Pi4J no longer needs to know those paths at all: it tries the plain mapped name from `System.mapLibraryName()` first (the `-dev` package's unversioned symlink), then falls back to the `.0` and `.1` runtime sonames so loading still works when only the runtime package is installed. The result is a lookup that resolves correctly on `amd64`, `aarch64`, `riscv64`, or any future architecture Linux runs on, with no code changes required.

#### Along for the ride: two file descriptor leak fixes

The same PR closes two related bugs in `FFMDigitalInput` and `FFMDigitalOutput` that surfaced while getting the test suite green on RISC-V hardware:

- The chip device file descriptor opened to read line info and issue the line request is now closed in a `finally` block. Previously, an early exit — the line already being in use, an overflowing debounce value, or a failing `ioctl` — could leak that descriptor.
- `shutdownInternal()` in `FFMDigitalInput` only waited for the event-processing executor when the watchers list still looked non-empty. Since `removeListener()` clears that list without waiting for the watcher thread to actually leave its native `poll()` call, the shutdown could return while a thread was still holding the requested line's file descriptor — leaving the GPIO line flagged `USED` and breaking the next request for the same BCM.

Also included: a new `Pi4JNativeLibraryTest` covering the OS guard and candidate-resolution logic, plus JMH benchmark fixes (explicit `.bus()` values instead of relying on a default `gpiochip0`) so the performance tests run correctly on non-Raspberry-Pi hardware too.

#### Why it matters

Between this change and the GPIO-chip-selection groundwork from the Banana Pi post, Pi4J V5 is shaping up to be usable on any 64-bit Linux SBC the JVM itself supports, not just Raspberry Pi. RISC-V boards are still the least mature link in the chain — see the [performance caveats](/sbc/x86-arm-riscv/) — but the software side is no longer the blocker.
