---
title: Choosing an I/O Provider
weight: 90
tags: ["FFM", "Mock"]
---

Providers are extensible service modules responsible for the concrete implementation of a specific I/O type. The providers also allow separating the internal logic of the Pi4J core from the concrete implementation of the board on which they are used.

As of Pi4J 2.5 multiple providers for the same I/O type is no longer supported. During the Context initialization it will ensure only a single provider for an I/O type is loaded. In addition, the Mock Providers are not loaded unless expressly requested when creating the Context. [See Create Context](../create-context/)

## Available Providers

**{{% notice info %}}
Starting from Pi4J V5, [FFM](/documentation/providers/ffm/) is the only provider for real hardware, complemented by the [Mock](/documentation/providers/mock/) provider for testing. All other providers (GpioD, LinuxFS, PiGpio) have been removed. See below for details.
{{% /notice %}}**

* [FFM](/documentation/providers/ffm/)
  * The provider for real hardware, introduced in Pi4J 4.0.0
  * Pro
    * Doesn't need complex Docker-based builds of libraries
    * Uses latest modern Java LTS version 25
    * Simplifies code
    * Can be used on other boards than Raspberry Pi
  * Contra
    * Not found yet... ;-)
* [Mock](/documentation/providers/mock/)
  * Used for unit and integration testing without real hardware
  * Not loaded automatically on a Raspberry Pi; use `autoDetectMockPlugins()` or the Alternate Context Creation shown on the [Create Context](../create-context/) page

## Check Loaded Providers

After creating the `Context` the following code will print the currently loaded provider for each I/O type.
```
    System.out.println("-------------------------------------------------");
    System.out.println("PI4J PROVIDERS");
    System.out.println("-------------------------------------------------");
    pi4j.providers().describe().print(System.out);
    System.out.println("-------------------------------------------------");
```

## Related to functionality existing in V4, but no longer included in V5

Pi4J V5 removed the GpioD, LinuxFS and PiGpio providers to simplify the codebase, drop the Docker-based native builds, and simplify the build process. If you are upgrading from V4, migrate your code to the [FFM provider](/documentation/providers/ffm/).

* [GpioD](/documentation/providers/gpiod/) — was introduced in Pi4J 2.5.0, supported DigitalInput and DigitalOutput
* [LinuxFS](/documentation/providers/linuxfs/) — supported I2C, SPI, and PWM Hardware
* [PiGpio](/documentation/providers/pigpio/) — supported DigitalInput, DigitalOutput, PWM, I2C, SPI, Serial
