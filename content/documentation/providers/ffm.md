---
title: FFM Provider
weight: 91
tags: ["FFM"]
---

The FFM plugin provider was added in Pi4J 4.0.0 based on the Foreign Function & Memory (FFM) API

Providers in the FFM plugin:

* ffm-digital-input
* ffm-digital-output
* ffm-i2c
* ffm-pwm
* ffm-spi

## Quick Start

1. Ensure you are running JDK25+
1. Add dependency to your maven/gradle
   ```xml
   <dependency>
       <groupId>com.pi4j</groupId>
       <artifactId>pi4j-plugin-ffm</artifactId>
       <version>${pi4j.version}</version>
   </dependency>
   ```

When using FFM API functionality added to Java in version 22, you will be alerted at startup of the application with this message:

```text
WARNING: A restricted method in java.lang.foreign.AddressLayout has been called
WARNING: java.lang.foreign.AddressLayout::withTargetLayout has been called by ... in an unnamed module (file:...)
WARNING: Use --enable-native-access=ALL-UNNAMED to avoid a warning for callers in this module
WARNING: Restricted methods will be blocked in a future release unless native access is enabled
```

You can either ignore this message, or add `--enable-native-access=com.pi4j.plugin.ffm` to your run, or add `Enable-Native-Access: ALL-UNNAMED` to the `MANIFEST.MF` file in your project.

## Implementation notes

### I2C

The FFM plugin supports three types of I2C implementations:

* `I2CImplementation.DIRECT`: default option when you don't specify any I2C implementation.
* `I2CImplementation.FILE`
* `I2CImplementation.SMBUS`

```java
var i2cConfig = I2C.newConfigBuilder(pi4j)
        .bus(I2C_BUS)
        .device(I2C_DEVICE)
        .i2cImplementation(I2CImplementation.DIRECT)
        .build();
var i2c = pi4j.create(i2cConfig);
```

### PWM

Only hardware PWM is supported in V4.0.0.

### GPIO Chip Selection

On Raspberry Pi boards, `/dev/gpiochip0` is the single controller behind the 40-pin header, so the FFM plugin uses it by default. Many other SBCs (for example Allwinner- or Rockchip-based boards) expose multiple `gpiochip` devices, and the header pins are not necessarily on `gpiochip0`.

You can list the available chips and their line count with:

```shell
gpiodetect
```

or inspect line usage in detail with:

```shell
gpioinfo
```

To target a chip other than `gpiochip0`, set it with `.bus()` on the config builder — the value is appended to `/dev/gpiochip`, so `.bus(1)` targets `/dev/gpiochip1`:

```java
var ledConfig = DigitalOutput.newConfigBuilder(pi4j)
    .id("led")
    .name("LED Flasher")
    .bus(1)
    .bcm(GPIO_LINE_OFFSET)
    .shutdown(DigitalState.LOW)
    .initial(DigitalState.LOW);
```

{{% notice tip %}}
Despite its name, `.bcm()` is simply the line offset on the selected chip — it is not tied to Raspberry Pi's BCM numbering. On non-Raspberry-Pi boards, find the correct offset for your physical pin using the board's pinout documentation, then verify it with `libgpiod`'s `gpioset`/`gpioget` tools before wiring it into your Pi4J code. See [Using Pi4J on other brands](/sbc/using-pi4j-on-other-brands/) for a worked example.
{{% /notice %}}

## Dependencies and Permissions

Since FFM provider does not rely on third-party native code and handles all the work between the JVM and Linux kernel, we have to be very cautious with permissions given to the user, and a correct device setup.

In short, the following is needed:

* I2C dependency needed by the FFM plugin: `sudo apt install -y libi2c-dev`
* User permissions to access GPIO pins.

To simplify this, a few scripts are provided in the Pi4J OS repository on GitHub.

### Install Dependencies on Raspberry Pi OS

When you use the default Raspberry Pi OS (e.g. [installed on an SD Card with the Raspberry Pi Imager tool](/prepare/sd-card/)), you can add all the required dependencies, extra tools, apply settings for Java development, etc. with this command:

```bash
curl -sL https://raw.githubusercontent.com/Pi4J/pi4j-os/main/script/prepare-for-java.sh | bash
```

### Install Dependencies on Linux

When you are not using Raspberry Pi OS, but another Linux distribution, you can add all the required dependencies, extra tools, apply settings for Java development, etc. with this command:

```bash
curl -sL https://raw.githubusercontent.com/Pi4J/pi4j-os/main/script/prepare-for-java-non-rpi.sh | bash
```

### Configure Permissions for the FFM Plugin

To make sure you have the correct permissions to access GPIO pins and execute the FFM plugin, you can execute the following command:

```bash
curl -sL https://raw.githubusercontent.com/Pi4J/pi4j-os/main/script/setup-permissions.sh | bash
```

This script will do the following:
* Make sure you have the right groups in your distro:
  * Raspbian: `gpio` group and current user should be the member of this group
  * Ubuntu: `dialout` group and current user should be the member of this group
* Make sure you have correct `udev` rules, that are running your devices:
  * All devices should belong to group `gpio` or `dialout`
  * All devices should have `0660` rights to access them in safe manner

{{% notice warning %}}
Do not run any Pi4J FFM application with `sudo` or by `root`. That's unsecure, and third-party dependencies added to your application can compromise your hardware.
{{% /notice %}}

## Supported Operating System Versions

Any Linux kernel with GLIBC >= 2.13. That covers all modern distros (Ubuntu, Raspbian, Debian, Arch, etc.).
