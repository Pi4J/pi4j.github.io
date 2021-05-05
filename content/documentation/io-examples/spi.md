---
title: Serial Peripheral Interface (SPI)
weight: 240
tags: ["SPI"]
---

## What is it?

The Serial Peripheral Interface, abbreviated to SPI, is a bus system which enables 
communication between a main device (called “master”) and one or more secondary devices 
(called “slave”). A direct communication between all participants is not possible here, 
much more the master can choose at any time with which slave he would like to exchange data.

In order to address only one slave, a total of 3 signal lines are required, two of which 
are used for bidirectional data transmission and one as a clock generator for serial 
transmission. If further slaves are to be addressed, additional signal lines are required 
depending on the desired topology.

## Uses

In addition to communication between microcontrollers, SPI is also used to address 
numerous sensors and actuators. Similar to I²C, a large number of control commands and 
data can be transmitted in both directions with a relatively high clock rate over 3 lines. 
A particular advantage here is the support for “full duplex”, ie the simultaneous 
transmission of data in both directions.

The technical implementation is very simple and is also used, for example, to communicate 
with SD cards. The Nintendo Game Boy already used this protocol to connect several game 
consoles via the Game Boy Link Cable.

## Addressing

As already mentioned in the first section, multiple slaves can also be connected to SPI. 
The number available depends on the hardware used. On the Raspberry Pi, the standard SPI0
with two different slaves use what is called Chip Select Pins is controlled.

# Additional Information

- [Wikipedia SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface)
- [SPI pinout for Raspberry Pi](https://pinout.xyz/pinout/spi#)