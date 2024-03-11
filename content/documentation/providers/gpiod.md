---
title: GpioD Provider
weight: 91
tags: ["GpioD"]
---

The GpioD plugin provider was added in Pi4J 2.5.0 to be able to support the Raspberry Pi 5 with the new [GPIO chip RP1](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html). 

Providers in the GpioD plugin:

* linuxfs-i2c
* Under construction
    * gpiod-digital-input
    * gpiod-digital-output

To use the GpioD provider include the following dependencies:

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
    <artifactId>pi4j-plugin-gpiod</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```