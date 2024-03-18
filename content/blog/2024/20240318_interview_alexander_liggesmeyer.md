---
title: "Interview with Alexander Liggesmeyer"
date: 2024-03-18
tags: ["Interview", "Pi4J"]
---

2024-03-18, by Frank Delporte

Today, [version 2.5.0 of Pi4J got released with many changes, fixes and improvements](/about/release-notes/). The most important one being support for the [Raspberry Pi 5](https://www.raspberrypi.com/products/raspberry-pi-5/). Short after the release of this new board, [several issues were raised on GitHub](https://github.com/Pi4J/pi4j-v2/issues/321) as Pi4J was not compatible. The Raspberry Pi 5 uses a completely new way to interact with the GPIOs: the [RP1 chip](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html). Thanks to this chip, GPIO, SPI, I2C, USB, ethernet,... are seperated from the SoC to make it easier to develop newer boards and support. But this new approach wasn't supported by the PiGpio library used in Pi4J V2... Until Alexander Liggesmeyer took up the challenge to find a solution!

_Thanks Alexander for your amazing work! Can you introduce yourself?_

I'm Alexander, and I'm currently doing a PhD at [Saarland University's HCI Lab](https://hci.cs.uni-saarland.de/). The research chair is working in the area of human computer interaction, which also very often involves prototyping hardware.

_What is your interest in the Pi4J project and how are you using it?_

I first used it to develop a [Cocktail mixing machine](https://pi4j.com/featured-projects/cocktail-maker-by-alex9849/), whose software is based on Spring Boot. Spring boot is a well known Java Framework for developing APIs. Pi4J allows me to control the RaspberryPi's GPIO interfaces directly from Java.

_When you discovered that Pi4J wasn’t compatible with this new chip, what made you decide to dive into the problem and add a new provider?_

I got the new RaspberryPi 5 and ran a few applications on it. I saw that the CocktailPi application that could take about 60 seconds to start on a RaspberryPi 4, can now starts on less then 15 seconds. So I wanted to use the new Raspberry. Sadly Pi4J wasn't compatible with the new platform. I also saw that nobody was actively working on changing that, so I thought why shouldn't I do that by myself? I'm actively using this library and wanted a feature that it didn't got yet. The library is open source and one of the advantages of that is that everybody can contribute. So why don't do that? In the end everybody profits.

_This new provider is backwards compatible with earlier Raspberry Pi boards, how did you achieve this?_

The new provider interfaces with LibGpioD. LibGpioD is the library that directly interacts with the Gpio devices. I didn't dig into how it actually manipulates the gpiochip device files, but I don't think that these largely differ (if they differ at all)  between the Raspberry Pi versions. This is more something on the operating system level. The only thing that the provider needs to do is finding the correct gpiochip device. On the Raspberry Pi, this device always contains the name `pinctrl` in its name, so finding it is straight forward.

_An OOS-project can only improve thanks to contributions of the community. Was it easy to understand how to add functionality to the Pi4J project? How can the code or website be improved to attract more contributors?_

I think Pi4J is documented very well. Adding a new provider was a bit tricky, since I needed some libraries that were not part of the builder Docker images in the beginning. But this could be solved by also [cloning and updating the builders](https://github.com/Pi4J/pi4j-docker). The only thing that I see that could be improved is, that the link to slack could be made more present.

_How do you see the future of Java on embedded devices like the Raspberry Pi?_

It depends on what a person want to archive. I personally like to use Python to develop small prototypes. For larger projects I like type safe programming languages more, since they already prevent most type errors at compile time. Java forces the developer to add the type of variable every time it is initialized. This adds readability. Python on the other hand doesn't force the developer to add type hints, which leads developers not adding them in many cases. This makes refactoring code harder and more prone to adding errors.