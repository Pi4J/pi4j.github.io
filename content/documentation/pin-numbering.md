---
title: Pin numbering
weight: 40
---

Pi4J V.1 took a pretty opinionated approach to pin numbering as the scheme was based on the underlying WiringPi.
This scheme was incompatibility with other pin diagrams and pin numbering used by other development platforms and libraries.
   
As Pi4J V.2 is build as a "pass thru library", and uses [PiGpio](http://abyz.me.uk/rpi/pigpio/index.html) as the underlying framework,
the more well-known BCM numbering is being used now.

This drawing shows the different numbers for WiringPi and BCM in a 40-pins Raspberry Pi header:

![40-pins header](/assets/documentation/headerpins_in_header.png)