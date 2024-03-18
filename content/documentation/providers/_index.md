---
title: Choosing an I/O Provider
weight: 90
tags: ["LinuxFS", "PiGpio"]
---

Providers are extensible service modules responsible for the concrete implementation of a specific I/O type. 
Multiple providers for the same I/O type can be loaded into a Pi4J context concurrently. For example a 
"RaspberryPi-DigitalInputProvider" and "GertBoard-DigitalInputProvider" could both be loaded and both providing digital 
inputs at the same time.

The providers also allow to separate the internal logic of the Pi4J core from the concrete implementation of the board 
on which they are used.

Current supported providers:

* [GpioD]()
  * Was introduced in Pi4J 2.5.0
  * Pro
    * Works on Raspberry Pi 5
    * Doesn't need sudo
  * Contra 
    * Only provides DigitalInput and DigitalOutput
* [LinuxFS](/documentation/providers/linuxfs/)
  * Pro
    * Generic for any SoC supporting LinuxFS
    * Doesn't need `sudo`
  * Contra
    * Doesn't provide serial and SPI 
    * Latency (? - still to be tested)
* [PiGpio](/documentation/providers/pigpio/)
  * Pro
    * Provides all types of communication: DigitalInput, DigitalOutput, PWM, I2C, SPI, Serial
    * Can be used remotely
  * Contra
    * Needs to run as `sudo`

Possible future providers:

* RemoteProvider to control the I/O from a remote device e.g. through websockets