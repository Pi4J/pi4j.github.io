---
title: GpioD Provider
weight: 91
tags: ["GpioD"]
---

The GpioD plugin provider was added in Pi4J 2.5.0 to be able to support the Raspberry Pi 5 with the new [GPIO chip RP1](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html). 

Providers in the GpioD plugin:

* gpiod-digital-input
* gpiod-digital-output

{{% notice warn %}}
The GpioD Provider needs a recent Raspberry Pi OS version (Bookworm)!
{{% /notice %}}

If you get an error at startup with the following content, your OS is outdated for the GpioD implementation used in Pi4J:

```shell
UNDERLYING EXCEPTION: [java.lang.UnsatisfiedLinkError]=/tmp/libgpiod368899536808039438.so: /lib/aarch64-linux-gnu/libc.so.6: version `GLIBC_2.33' not found (required by /tmp/libgpiod368899536808039438.so)
```

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