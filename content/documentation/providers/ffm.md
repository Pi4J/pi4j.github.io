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
* ffm-serial
* ffm-spi

## Quick start

1. Ensure you are running JDK25+
2. Add `--enable-native-access=com.pi4j.plugin.ffm` to your run or add to MANIFEST.MF `Enable-Native-Access: ALL-UNNAMED`
3. Add dependency to your maven/gradle
``` xml
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-ffm-plugin</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```
4. (optional) Use new API Provided by package `...`

## Note on permissions

Since FFM provider does not rely on third-party native code and do all work between JVM and Linux kernel we have to be very cautious with permissions user have and devices setup correctly.
That is why we have a special checker, that helps users setup security aspect of using pi4j.

TLDR; Use `sudo /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/,,,/permissions_install.sh)"` and reboot the device.

What the user should consider:
1. Do not run any of pi4j FFM with `sudo` or by `root`. That's unsecure and third-party dependencies added to your application can compromise you hardware.
2. Make sure you have right groups in your distro:
    - Raspbian: `gpio` group and current user should be the member of this group
    - Ubuntu: `dialout` group and current user should be the member of this group
3. Make sure you have correct `udev` rules, that are running your devices:
    - All devices should belong to group `gpio` or `dialout`
    - All devices should have `0660` rights to access them in safe manner


## Implementation notes

### GPIO (Digital Input / Digital Output)

### I2C

### SPI

### Serial

Serial protocol is considered as alpha for now, use at your own risk.

### PWM

## Supported Operating System Versions

Any Linux kernel with GLIBC >= 2.13. That covers all modern distros (Ubuntu, Raspbian, Debian, Arch, etc.).

## Dependencies 

To use the FFM provider include the following dependencies:

``` xml
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-ffm-plugin</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```
