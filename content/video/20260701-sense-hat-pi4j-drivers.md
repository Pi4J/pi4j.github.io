---
title: '2026 Sense HAT with Pi4J'
date: 2026-07-01
youtube: w7xxDu7lJPE
tags: ["Video", "Drivers"]
---

## Using the Raspberry Pi Sense HAT with Pi4J Drivers

**20260701 - Video by Igor De Souza**

{{< youtube w7xxDu7lJPE >}}

The [Sense HAT](https://www.raspberrypi.com/products/sense-hat/) packs an 8×8 RGB LED matrix, environmental sensors (temperature, humidity, and pressure), motion sensors (accelerometer, gyroscope, and magnetometer), and a small joystick onto a single Raspberry Pi expansion board. In this video, Igor De Souza shows how Java developers can talk to all of that hardware through [Pi4J Drivers](/drivers/), the companion library to [Pi4J](https://www.pi4j.com/).

Instead of implementing the I2C communication for each sensor by hand, Pi4J Drivers wraps the Sense HAT in a clean, consistent Java API: create a `SenseHat` instance and start reading the sensors and driving the LED matrix with straightforward method calls, without manual register handling.

* [Pi4J website](https://www.pi4j.com/)
* [Pi4J Drivers](/drivers/)
* [Blog post: Sense HAT with Pi4J](/blog/2026/20260701-sense-hat-pi4j-drivers/)
* [Foojay article: Using the Raspberry Pi Sense HAT with Pi4J Drivers](https://foojay.io/today/using-the-raspberry-pi-sense-hat-with-pi4j-drivers/)
* [Pi4J Examples](https://github.com/Pi4J/pi4j-example-drivers)
* [Pi4J GitHub Discussions](https://github.com/Pi4J/pi4j/discussions)
