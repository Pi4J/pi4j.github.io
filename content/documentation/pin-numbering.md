---
title: Pin numbering
weight: 40
---

Pi4J V1 took a pretty opinionated approach to pin numbering as the scheme was based on the underlying WiringPi.
This scheme was incompatibility with other pin diagrams and pin numbering used by other development platforms and libraries.
   
As Pi4J V2+ is built as a "pass thru library" on top of the underlying framework (the [FFM provider](/documentation/providers/ffm/) as of V5), the more well-known BCM numbering is being used now.

This drawing shows the different numbers for WiringPi and BCM in a 40-pins Raspberry Pi header:

![40-pins header](/assets/documentation/headerpins_in_header.png)

{{% notice warning %}}
**Pi4J does not validate that a BCM/line number corresponds to a physical pin.** The [FFM provider](/documentation/providers/ffm/) will accept any line number that's valid for the selected `gpiochip`, even one outside the 40-pin header. Pi4J also runs on many SBCs other than the Raspberry Pi, each with its own valid range and pin layout, so Pi4J cannot reliably police "valid" BCM/line numbers for every board out there — doing so per-board would be a maintenance burden and would still not catch every case.

In practice this means: it's **your responsibility** to pass a BCM/line number that actually exists on your board and maps to the header pin you intend to use. Passing an out-of-range or otherwise invalid number can cause unexpected behavior — on some boards (e.g. Raspberry Pi 5) this has been observed to hang the application entirely rather than fail with a clear error (see [pi4j#750](https://github.com/Pi4J/pi4j/issues/750)).

Double-check your pin/BCM number against your board's official pinout documentation, and use `gpiodetect`/`gpioinfo` (see [FFM Provider](/documentation/providers/ffm/#gpio-chip-selection)) to verify it before wiring it into your code.
{{% /notice %}}