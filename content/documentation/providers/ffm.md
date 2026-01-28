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
       <artifactId>pi4j-ffm-plugin</artifactId>
       <version>${pi4j.version}</version>
   </dependency>
   ```

When using FFM API functionality added to Java in version 22, you will be alerted at startup of the applicatoin with this message:

```text
WARNING: A restricted method in java.lang.foreign.AddressLayout has been called
WARNING: java.lang.foreign.AddressLayout::withTargetLayout has been called by ... in an unnamed module (file:...)
WARNING: Use --enable-native-access=ALL-UNNAMED to avoid a warning for callers in this module
WARNING: Restricted methods will be blocked in a future release unless native access is enabled
```

You can either ignore this message, or add `--enable-native-access=com.pi4j.plugin.ffm` to your run, or add `Enable-Native-Access: ALL-UNNAMED` to the `MANIFEST.MF` file in your project.

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
