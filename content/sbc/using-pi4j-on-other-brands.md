---
title: "Using Pi4J on Other Brands"
weight: 30
tags: ["FFM", "GPIO", "Allwinner", "Banana Pi"]
---

Pi4J started with, and is best documented for, the Raspberry Pi. On a Raspberry Pi, the GPIO numbers you pass to Pi4J match the SoC's own "BCM" numbering directly, so pin 16 on the header is BCM 23 as you can see in the GPIO header for, for instance, the [Raspberry Pi 5](https://api.pi4j.com/board-information/MODEL_5_B).

Many other SBCs (Banana Pi, Orange Pi, and other Allwinner- or Rockchip-based boards) use a different SoC with its own GPIO controller and numbering scheme, even when the board physically matches the Raspberry Pi's header layout. This page walks through the general process of finding the right GPIO addressing for such a board, using a Banana Pi M4 Zero (Allwinner H618) as an example.

## 1. Find the board's official pinout table

Start with the manufacturer's documentation. For the Banana Pi M4 Zero, the [official pinout table](https://docs.banana-pi.org/en/BPI-M4_Zero/BananaPi_BPI-M4_Zero#_gpio_pin_define) lists physical pin 16 as `PI15`: GPIO bank `I`, pin `15`.

{{% notice warning %}}
Don't assume every pin on a Raspberry-Pi-compatible header is actually a GPIO. On the Banana Pi M4 Zero, physical pin 22 — which is BCM 25 (a GPIO) on a Raspberry Pi — is wired to 3.3V power instead. Always check the pinout table before wiring!
{{% /notice %}}

## 2. Identify the right `gpiochip`

Allwinner chips group GPIOs into lettered banks of 32 pins each (`PA0`-`PA31`, `PB0`-`PB31`, and so on — see [linux-sunxi.org/GPIO](https://linux-sunxi.org/GPIO)), exposed as `/dev/gpiochip*` character devices. Install `libgpiod`'s command-line tools and list the chips:

```shell
sudo apt install -y gpiod
gpiodetect
gpioinfo
```

On the Banana Pi M4 Zero this showed `gpiochip0` with 32 lines and `gpiochip1` with 288 lines. Since 288 = 9 × 32, matching banks A through I, `gpiochip1` is the controller behind the 40-pin header — not the default `gpiochip0`.

```text
gpiochip0 - 32 lines:
	line   0:      unnamed       kernel   input  active-high [used]
	line   1:      unnamed       kernel   input  active-high [used]
	line   2:      unnamed       unused   input  active-high 
    ...
gpiochip1 - 288 lines:
	line   0:      unnamed       unused   input  active-high 
	line   1:      unnamed       unused   input  active-high 
	line   2:      unnamed       unused   input  active-high 
    ...
```

## 3. Compute the line offset

Each bank's index (A=0, B=1, C=2, ... I=8) times 32, plus the pin number within the bank, gives the absolute line offset on the chip. For `PI15` with `I=8`: `8 × 32 + 15 = 271`.

## 4. Verify before wiring it into code

Confirm the offset with `gpioset` and an LED (or multimeter) before touching Java:

```shell
gpioset gpiochip1 271=1 # ON
gpioset gpiochip1 271=0 # OFF
```

## 5. Configure Pi4J's FFM provider

Once verified, use `.bus()` to select the chip and `.bcm()` for the line offset (see [FFM Provider: GPIO Chip Selection](/documentation/providers/ffm/#gpio-chip-selection)):

```java
private static final int GPIO_LED = 271;   // physical pin 16 = PI15 on gpiochip1

var ledRed = pi4j.create(DigitalOutput.newConfigBuilder(pi4j)
    .id("led").name("LED").bus(1).bcm(GPIO_LED)
    .shutdown(DigitalState.LOW).initial(DigitalState.LOW));
```

## Summary

1. Check the board's official pinout table — physical pin numbers don't always map to the SoC's native GPIO numbering, and some pins may not be GPIOs at all.
2. Use `gpiodetect`/`gpioinfo` to find which `gpiochip` actually serves the header.
3. Compute the candidate line offset from the bank/pin naming.
4. Verify with `gpioset`/`gpioget` before writing any Java code.
5. Configure Pi4J's FFM provider with `.bus()` and `.bcm()` accordingly.
