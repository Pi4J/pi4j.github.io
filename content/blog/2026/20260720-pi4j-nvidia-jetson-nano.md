---
title: "Pi4J on NVIDIA"
date: 2026-07-20
tags: ["GPIO", "Jetson Nano", "Tegra"]
---

2026-07-20 by Igor De Souza

## Pi4J on NVIDIA Jetson Nano

### Running Pi4J on the NVIDIA Jetson Nano

Pi4J is built for the Raspberry Pi, but the underlying `libgpiod`-based approach works on any Linux board that exposes its GPIOs through the kernel's `gpiochip` interface. In a [new article on dev.to](https://dev.to/igoriot/running-pi4j-on-the-nvidia-jetson-nano-42kc), Igor De Souza puts that to the test on an [NVIDIA Jetson Nano](https://developer.nvidia.com/embedded/jetson-nano-developer-kit) (an A02 board running the 2019-era JetPack 4.2 / L4T R32.1), with the same simple goal as the [recent Banana Pi experiments](https://www.pi4j.com/blog/2026/20260717-java-on-banana-pi-arm-riscv/): blink an LED.

#### The challenge: Tegra's own GPIO naming scheme

The Jetson Nano's Tegra SoC doesn't number its GPIOs the way a Raspberry Pi does. Pins are grouped into named ports (`AA`, `BB`, `CC`, `DD`, ...) rather than a flat BCM range, and NVIDIA's documentation on how those map to Linux `gpiochip` line numbers turned out to be scattered across multiple documents, source files, and forum posts, with no single authoritative reference. A newer NVIDIA utility, `jetson-gpio-pinmux-lookup`, would have made this easier, but it requires a JetPack version newer than what this older board was running.

Working from NVIDIA's `Jetson.GPIO` repository, the article derives the offset formula for Tegra: `(port_index × 8) + line_number`. For header J41, physical pin 12 maps to `PJ.07` in Tegra's own nomenclature, and with port `J` at index 9, that resolves to line `9 × 8 + 7 = 79` on `gpiochip0`. As with the Banana Pi board, that offset was verified independently before writing any Java code, using `sudo gpioset --mode=wait gpiochip0 79=1`.

#### Getting Pi4J to target it

With the correct offset confirmed, the article uses a draft `LineHelper` utility to translate the Tegra port/pin notation directly into a Pi4J GPIO address:

```java
LineHelper.getAddress(GpioLineFamily.TEGRA, 'J', 7)
```

That resolved address is then used the same way any BCM value is elsewhere in Pi4J, and the LED blinked.

#### Why it matters

Each SoC family — Allwinner, Tegra, Rockchip, and others — turns out to follow its own GPIO addressing rules, but once the pattern for a given family is understood, it's manageable. The article's broader point is a proposal for Pi4J's core: a pluggable `LineMapper` interface that would let SoC-specific address translation (like the Tegra formula above) live behind a clean extension point, so Pi4J can stay platform-agnostic instead of hardcoding knowledge of every board family it might run on.

Read the full article on dev.to: [Running Pi4J on the NVIDIA Jetson Nano](https://dev.to/igoriot/running-pi4j-on-the-nvidia-jetson-nano-42kc).
