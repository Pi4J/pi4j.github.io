---
title: 'Drivers History'
weight: 5
---

## Drivers in Pi4J V1

Pi4J V1, the original library that started in 2012, shipped with two companion libraries alongside the core:

* `pi4j-device` — ready-to-use drivers for components such as buttons, rotary encoders, temperature sensors, motor controllers, and displays.
* `pi4j-gpio-extension` — support for GPIO expander chips.

These libraries lowered the barrier for beginners. Instead of writing raw I2C or SPI communication code, developers could grab a ready-made driver class and focus on their application logic.

## Why drivers were removed

As Pi4J matured, the bundled device library became a maintenance burden. Every new component added to the library required ongoing testing, bug fixes, and updates whenever the core changed. With a small volunteer team, keeping dozens of device drivers current alongside the core library was not sustainable.

Pi4J V1.4.0, released on 2021-03-03, **removed `pi4j-device` and `pi4j-gpio-extension`** as part of a deliberate refocus. The project shifted its energy to the core I/O primitives: GPIO, I2C, SPI, PWM, and Serial. That decision unlocked a cleaner architecture in V2, Java module support, and eventually the jump to Java 21 in V3 and Java 25 in V4.

Read the full context in the [Pi4J V1 release notes](/about/info-v1/) and the [release notes for V2+](/about/release-notes/).

## A new community-driven drivers library

The gap left by removing the device library did not go unnoticed. Over the years, community members built their own device implementations and shared them in the [pi4j-examples](https://github.com/Pi4J/pi4j-examples) repository. That work became the foundation for a proper solution.

The result is the **Pi4J Drivers library**: a standalone Maven library, maintained separately from the Pi4J core, that provides drivers for a growing set of components. Keeping it separate means:

* The Pi4J core stays lean and focused.
* Driver releases are independent of core releases.
* Community contributors can add or fix drivers without touching the core.
* Users pick only the drivers they need.

The library targets **Pi4J V4+** and lives in its own GitHub repository:
[github.com/Pi4J/pi4j-drivers](https://github.com/Pi4J/pi4j-drivers)

## Getting started

Add the Pi4J Drivers library to your Maven project:

```xml
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-drivers</artifactId>
    <version>${pi4j.drivers.version}</version>
</dependency>
```

Check the [release notes](/drivers/drivers-release-notes/) for the latest version. For complete example applications that use the drivers, see [Example Devices](/drivers/example-devices/).

