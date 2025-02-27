---
title: GpioD Provider
weight: 91
tags: ["GpioD", "Digital Input", "Digital Output"]
---

The GpioD plugin provider was added in Pi4J 2.5.0 to be able to support the Raspberry Pi 5 with the new [GPIO chip RP1](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html).

Providers in the GpioD plugin:

* gpiod-digital-input
* gpiod-digital-output

## Supported Operating System Versions

{{% notice warning %}}
The GpioD provider requires minimum kernel Bullseye 6.1.21 and Bookworm 6.6.22 !
{{% /notice %}}

If you get an error at startup with the following content, your OS is outdated for the GpioD implementation used in Pi4J:

```shell
UNDERLYING EXCEPTION: [java.lang.UnsatisfiedLinkError]=/tmp/libgpiod368899536808039438.so: /lib/aarch64-linux-gnu/libc.so.6: version `GLIBC_2.33' not found (required by /tmp/libgpiod368899536808039438.so)
```

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
    <artifactId>pi4j-plugin-gpiod</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```

## Specifying the GPIO Chip

On devices like industrial Raspberry Pis and the Raspberry Pi 5 that are equipped with multiple GPIO chips, it is necessary to explicitly specify the target GPIO chip when using Pi4J to control GPIO. This prevents unintended access to other GPIO chips and enables accurate control.

### Checking GPIO Chips

You can check the list of GPIO chips installed on the system using the `gpiodetect` command.

```shell
$ sudo gpiodetect
gpiochip0 [pinctrl-bcm2711] (58 lines)
gpiochip1 [raspberrypi-exp-gpio] (8 lines)
gpiochip2 [1-0027] (16 lines)
gpiochip3 [10-0020] (16 lines)
```

In the example above, four GPIO chips (`gpiochip0`, `gpiochip1`, `gpiochip2`, `gpiochip3`) are detected.

### Specifying GPIO Chips in Pi4J

To control a specific GPIO chip with Pi4J, specify the GPIO chip name with the `.setGpioChipName()` method when creating a context using `Pi4J.newContextBuilder()`. This new method has been added in V3.0.0 of Pi4J.

```java
Context pi4j = Pi4J.newContextBuilder()
    .add(GpioDDigitalInputProvider.newInstance())
    .setGpioChipName("gpiochip2")
    .build();
```

By default, `gpiochip0` is used. You only need to specify the chip if you want to use another one.