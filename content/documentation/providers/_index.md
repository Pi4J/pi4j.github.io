---
title: Choosing an I/O Provider
weight: 90
---

Providers are extensible service modules responsible for the concrete implementation of a specific I/O type. 
Multiple providers for the same I/O type can be loaded into a Pi4J context concurrently. For example a 
"RaspberryPi-DigitalInputProvider" and "GertBoard-DigitalInputProvider" could both be loaded and both providing digital 
inputs at the same time.

The providers also allow to seperate the internal logic of the Pi4J core from the concrete implementation of the board 
on which they are used.

Current supported providers:

* [PiGpio](/documentation/providers/pigpio/)
* [LinuxFS](/documentation/providers/linuxfs/)

Possible future providers:

* LinuxFileSystemProvider: e.g. to use native Linux serial interfaces
* RemoteProvider to control the I/O from a remote device e.g. through websockets