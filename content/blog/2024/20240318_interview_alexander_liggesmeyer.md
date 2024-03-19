---
title: "Alexander Liggesmeyer and RPi5"
date: 2024-03-18
tags: ["Interview", "Pi4J"]
---

2024-03-18, by Frank Delporte

## Interview with Alexander Liggesmeyer about Pi4J for Raspberry Pi 5

Today, [version 2.5.0 of Pi4J got released with many changes, fixes and improvements](/about/release-notes/). The most important one being support for the [Raspberry Pi 5](https://www.raspberrypi.com/products/raspberry-pi-5/). Short after the release of this new board, [several issues were raised on GitHub](https://github.com/Pi4J/pi4j-v2/issues/321) as Pi4J was not compatible. The Raspberry Pi 5 uses a completely new way to interact with the GPIOs: the [RP1 chip](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html). Thanks to this chip, GPIO, SPI, I2C, USB, ethernet,... are seperated from the SoC to make it easier to develop newer boards. But this new approach wasn't supported by the PiGpio library used in Pi4J V2... Until Alexander Liggesmeyer took up the challenge to find a solution!

_Thanks Alexander for your amazing work! Can you introduce yourself?_

I’m Alexander, and I’m currently doing a PhD at [Saarland University’s HCI Lab](https://hci.cs.uni-saarland.de/). The research chair is working in the area of human computer interaction, which also often involves prototyping hardware.

_What is your interest in the Pi4J project and how are you using it?_

I first used it to develop a [Cocktail mixing machine](https://pi4j.com/featured-projects/cocktail-maker-by-alex9849/), whose software is based on Spring Boot. Spring Boot is a well-known Java framework for developing APIs. Pi4J allows me to control the Raspberry Pi's GPIO interfaces directly from Java.

_When you discovered that Pi4J wasn’t compatible with this new chip, what made you decide to dive into the problem and add a new provider?_

I got the new Raspberry Pi 5 and ran a few applications on it. I saw that the CocktailPi application which could take about 60 seconds to start on a Raspberry Pi 4, can now start in less than 15 seconds. So I wanted to use the new Raspberry. Unfortunately, Pi4J wasn't yet compatible with the new platform. I also saw that nobody was actively working on changing this, so I thought, why shouldn't I do that myself? I'm actively using this library and wanted a feature that it hasn't got yet. The library is open source and one of the advantages of that is that everybody can contribute. So why not do that? In the end, everybody profits.

_This new provider is backwards compatible with earlier Raspberry Pi boards, how did you achieve this?_

The new provider interfaces with LibGpioD, the library directly interacting with Gpio devices. I didn't dig into how it actually manipulates the gpiochip device files, but I don't think that they differ significantly (if at all) between Raspberry Pi versions. This is more something on the operating system level. The only thing the provider needs to do is find the correct gpiochip device. On the Raspberry Pi, this device always contains the name `pinctrl` in its name, so finding it is straightforward.

_An OOS-project can only improve thanks to contributions of the community. Was it easy to understand how to add functionality to the Pi4J project? How can the code or website be improved to attract more contributors?_

I think Pi4J is very well documented. Adding a new provider was a bit tricky, since I needed some libraries that were not part of the builder Docker images initially. But this could be solved by [cloning and updating the builders](https://github.com/Pi4J/pi4j-docker) as well. The only thing that I see could be improved is making the link to Slack more prominent.

_How do you see the future of Java on embedded devices like the Raspberry Pi?_

It depends on what a person wants to achieve. I personally like to use Python to develop small prototypes. For larger projects, I prefer type-safe programming languages because they already prevent most type errors at compile time. Java requires the developer to add the type of a variable every time it is defined, which adds to readability. On the other hand, Python does not force the developer to add type hints, leading to many developers not adding them. This makes refactoring code harder and more prone to errors.
