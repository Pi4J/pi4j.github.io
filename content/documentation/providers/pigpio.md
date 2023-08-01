---
title: PiGpio
tags: ["PiGpio"]
---

The current implementation of the PiGpio exposes the GPIO functions available on the Raspberry Pi.

Providers in the PiGpio plugin:

* pigpio-digital-input
* pigpio-digital-output
* pigpio-pwm
* pigpio-i2c
* pigpio-spi
* pigpio-serial

To use the PiGpio provider include the following dependencies:

``` xml
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-core</artifactId>
    <version>${pi4j.version}</version>
</dependency>
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-plugin-raspberrypi</artifactId>
    <version>${pi4j.version}</version>
</dependency>
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-plugin-pigpio</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```
