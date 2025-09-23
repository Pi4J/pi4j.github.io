---
title: FFM Provider
weight: 91
tags: ["FFM"]
---

The FFM plugin provider was added in Pi4J 4.0.0 based on the Foreign Function & Memory (FFM) API

Providers in the GpioD plugin:

* ffm-digital-input
* ffm-digital-output
* ffm-i2c
* ffm-pwm
* ffm-serial
* ffm-spi

## Supported Operating System Versions



## Dependencies 

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
    <artifactId>pi4j-plugin-ffm</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```
