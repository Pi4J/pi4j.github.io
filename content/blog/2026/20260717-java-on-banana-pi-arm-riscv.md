---
title: "Java on Banana Pi"
date: 2026-07-17
tags: ["FFM", "GPIO", "Allwinner", "Banana Pi", "RISC-V"]
---

2026-07-17, by Frank Delporte

## Java on Banana Pi ARM and RISC-V, Plus a Blinking LED with Pi4J

In a new post on my blog, I tried out Java on two Banana Pi boards that step outside the usual Raspberry Pi comfort zone: the **BPI-M4 Zero**, an ARM board built around the Allwinner H618 (four Cortex-A53 cores at 1.5GHz, 4GB RAM), and the **BPI-F3**, an industrial RISC-V board powered by SpacemiT's eight-core K1 SoC. Both keep the familiar 40-pin, Raspberry-Pi-compatible header, but under the hood they are a different world entirely.

Read the full article: [First test of Java on Banana Pi ARM and RISC-V, plus a blinking LED with Pi4J](https://webtechie.be/post/first-test-of-java-on-banana-pi-arm-and-risc-v-plus-a-blinking-led-with-pi4j/) on webtechie.be.

{{< youtube 78Jm2sR33fI >}}

### Java runs fine, out of the box

Java 25 was installed via SDKMAN on the ARM board and via `apt` on the RISC-V board. `HelloWorld.java`, a JSON parsing example, and JBang scripts all ran without any special tricks on both boards. Performance-wise, the BPI-M4 Zero beat a Raspberry Pi Zero 2 by 35-47% in the benchmarks, and the BPI-F3 held its own against other RISC-V hardware.

### The real challenge: GPIO addressing

Blinking an LED turned out to be the hard part, not because of Java, but because of how the Allwinner H618 organizes its GPIOs. Where a Raspberry Pi has a single `gpiochip0` behind the header with numbering that matches Pi4J's BCM values directly, the Banana Pi exposes GPIOs in lettered banks (`PA0`-`PA31`, `PB0`-`PB31`, ...) spread across multiple `gpiochip` devices — in this case `gpiochip0` (32 lines) and `gpiochip1` (288 lines).

Working from the board's official pinout table, physical pin 16 turned out to be `PI15`. With the banks indexed `A=0, B=1, ... I=8`, the absolute line offset became `(8 × 32) + 15 = 271` on `gpiochip1`. That offset was verified with `gpioset gpiochip1 271=1` before touching any Java code, using the RGB LED's other two pins (272 and 230) the same way.

With the correct offsets in hand, only a small change to the JBang `RgbLed.java` example was needed: adding `.bus(1)` to target `gpiochip1` and swapping in the calculated `.bcm()` values. The result: the RGB LED blinked — the first working Pi4J example on a non-Raspberry-Pi board.

### More on this site

This exact workflow — finding the pinout table, identifying the right `gpiochip`, computing the line offset, and verifying it before writing code — is now documented step by step in [Using Pi4J on Other Brands](/sbc/using-pi4j-on-other-brands/), using the same Banana Pi M4 Zero as an example. It ties directly into the [FFM provider's new "GPIO Chip Selection" section](/documentation/providers/ffm/#gpio-chip-selection), which explains how `.bus()` and `.bcm()` work together to target a specific chip and line offset when your board doesn't put the header on `gpiochip0`.
