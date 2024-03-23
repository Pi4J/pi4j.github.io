---
title: Choosing an I/O Provider
weight: 90
tags: ["LinuxFS", "PiGpio"]
---

Providers are extensible service modules responsible for the concrete implementation of a specific I/O type.
The providers also allow to separate the internal logic of the Pi4J core from the concrete implementation of the board
on which they are used.

Pi4J 2.0 - 2.4: Multiple providers for the same I/O type can be loaded into a Pi4J context concurrently. For example a 
"RaspberryPi-DigitalInputProvider" and "GertBoard-DigitalInputProvider" could both be loaded and both providing digital 
inputs at the same time.

As of Pi4J 2.5 multiple providers for the same I/O type is no longer supported. During the Context initialization it will
ensure only a single provider for an I/O type is loaded.



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
    * 03/22/2024 Does not support Pi5

Possible future providers:

* RemoteProvider to control the I/O from a remote device e.g. through websockets

Pi4J 2.5 ensuring a single provider for an I/O type is loaded may result in the provider your code references not being found.
Below is an example to specifically load the PiGpio providers.  There also is  example code to pretty print the
Providers that were loaded.

* Ensure single provider for a I/O type
```java
  Context pi4j = Pi4J.newAutoContext();
```
* Specifically load PiGpio providers
 ```java
    PiGpio piGpio = PiGpio.newNativeInstance();
    Context pi4j = Pi4J.newContextBuilder().add(
        PiGpioI2CProvider.newInstance(piGpio),
        PiGpioDigitalInputProvider.newInstance(piGpio),
        PiGpioDigitalOutputProvider.newInstance(piGpio)).build();
```
* PrettyPrint loaded providers
```java
    System.out.println("-------------------------------------------------");
    System.out.println("PI4J PROVIDERS");
    System.out.println("-------------------------------------------------");
    pi4j.providers().describe().print(System.out);
    System.out.println("-------------------------------------------------");
```