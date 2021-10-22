---
title: PiGpio
---

The current implementation of the PiGpio exposes the GPIO functions available on the Raspberry Pi.

Providers in the PiGpio plugin:

* pigpio-digital-input
* pigpio-digital-output
* pigpio-pwm
* pigpio-i2c
* pigpio-spi
* pigpio-serial

To use the LinuxFS provider first add the proper dependency:

``` xml
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-plugin-raspberrypi</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```