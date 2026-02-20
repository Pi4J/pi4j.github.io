---
title: Choosing an I/O Provider
weight: 90
tags: ["GpioD", "LinuxFS", "PiGpio"]
---

Providers are extensible service modules responsible for the concrete implementation of a specific I/O type. The providers also allow separating the internal logic of the Pi4J core from the concrete implementation of the board on which they are used.

As of Pi4J 2.5 multiple providers for the same I/O type is no longer supported. During the Context initialization it will ensure only a single provider for an I/O type is loaded. In addition, the Mock Providers are not loaded unless expressly requested when creating the Context. [See Create Context](../create-context/)

## Available Providers

* [FFM](/documentation/providers/ffm/)
  * Was introduced in Pi4J 4.0.0
  * Pro
    * Doesn't need complex Docker-based builds of libraries
    * Uses latest modern Java LTS version 25
    * Simplifies code
    * Can be used on other boards than Raspberry Pi
  * Contra
    * Not found yet... ;-)
* [GpioD](/documentation/providers/gpiod/)
  * Was introduced in Pi4J 2.5.0
  * Pro
    * Works on Raspberry Pi 5
    * Doesn't need sudo
    * Supports DigitalInput and DigitalOutput
* [LinuxFS](/documentation/providers/linuxfs/)
  * Pro
    * Works on Raspberry Pi 5
    * Generic for any SoC supporting LinuxFS
    * Supports I2C, SPI, and PWM Hardware
    * Doesn't need `sudo`
  * Contra
    * Doesn't provide serial and SPI 
    * DigitalInput and DigitalOutput under construction
    * Latency (? - still to be tested)
* [PiGpio](/documentation/providers/pigpio/)
  * Pro
    * Provides all types of communication: DigitalInput, DigitalOutput, PWM, I2C, SPI, Serial
    * Can be used remotely
  * Contra
    * Needs to run as `sudo`
    * 03/22/2024 Does not support Raspberry Pi 5

## Check Loaded Providers

After creating the `Context` the following code will print the currently loaded provider for each I/O type.
```
    System.out.println("-------------------------------------------------");
    System.out.println("PI4J PROVIDERS");
    System.out.println("-------------------------------------------------");
    pi4j.providers().describe().print(System.out);
    System.out.println("-------------------------------------------------");
```
