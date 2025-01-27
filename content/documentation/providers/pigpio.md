---
title: PiGpio Provider
weight: 95
tags: ["PiGpio", "PWM", "I2C", "SPI", "Serial", "Digital Input", "Digital Output"]
---

The current implementation of the PiGpio exposes the GPIO functions available on the Raspberry Pi (see Note Pi5 below). 
This implementation is developed/supported by a team separate of Pi4j.  Pi4j is a consumer of that PiGpio work.

```shell
Pi5  At the present time the PiGpio implementation does not support the new Pi5 board. 
- This new Pi5 RP1 chip will require a large development effort. There is no known plan for this develoment.   
```

Providers in the PiGpio plugin:

* pigpio-digital-input
* pigpio-digital-output
* pigpio-pwm
* pigpio-i2c
* pigpio-spi
* pigpio-serial

{{% notice warning %}}
Applications which use the PiGpio Provider, need to be started with `sudo` to be able to interface with the GPIOs.
{{% /notice %}}

When you don't use `sudo`, you'll see an error like this:

```shell
WARN com.pi4j.library.pigpio.impl.PiGpioNativeImpl 
    - PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
```

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
