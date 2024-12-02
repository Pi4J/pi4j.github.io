---
title: Choosing an I/O Provider
weight: 90
tags: ["GpioD", "LinuxFS", "PiGpio"]
---

Providers are extensible service modules responsible for the concrete implementation of a specific I/O type.
The providers also allow to separate the internal logic of the Pi4J core from the concrete implementation of the board
on which they are used.

Pi4J 2.0 - 2.4: Multiple providers for the same I/O type can be loaded into a Pi4J context concurrently. For example a 
"RaspberryPi-DigitalInputProvider" and "GertBoard-DigitalInputProvider" could both be loaded and both providing digital 
inputs at the same time.

As of Pi4J 2.5 multiple providers for the same I/O type is no longer supported. During the Context initialization it will
ensure only a single provider for an I/O type is loaded. In addition the Mock Providers are not loaded unless 
expressly requested when creating the Context.  [See Create Context](../create-context/)

Current supported providers:

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
    * Supports I2C, and PWM Hardware
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

Possible future providers:
* Pi5 SPI, under construction. 
* Pi5 Serial. At present the intent is no Pi4j Serial provider on Pi5. As an alternative see [jSerialComm](http://fazecast.github.io/jSerialComm/).
* RemoteProvider to control the I/O from a remote device e.g. through websockets

Pi4J 2.5 Provider not found
* Pi4J 2.5 ensuring a single provider for an I/O type is loaded may result in the provider your code references not being 
found because it was replaced by a higher priority provider.
If you encounter this case, you can remove the unwanted provider plugin from your pom.xml file dependencies. Then after a clean 
and rebuild of your program the unwanted provider will no longer be loaded.
 

* PrettyPrint loaded providers. After creating the Context the following code will print the currently loaded provider for each I/O type.
```
    System.out.println("-------------------------------------------------");
    System.out.println("PI4J PROVIDERS");
    System.out.println("-------------------------------------------------");
    pi4j.providers().describe().print(System.out);
    System.out.println("-------------------------------------------------");
```
