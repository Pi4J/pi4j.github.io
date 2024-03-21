---
title: PiGpio Provider
weight: 95
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

{{% notice warn %}}
Applications which use the PiGpio Provider, need to be started with `sudo` to be able to interface with the GPIOs. When you don't use `sudo`, you'll see an error like this:

```shell
WARN com.pi4j.library.pigpio.impl.PiGpioNativeImpl 
    - PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
```
{{% /notice %}}

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
