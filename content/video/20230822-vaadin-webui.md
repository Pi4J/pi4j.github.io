---
title: '2023 Vaadin WebUI'
date: 2023-08-22
tags: ["Video"]
---

## Controlling Electronics with Java and Pi4J through a web interface

**20230822 - J-Spring, The Netherlands**

{{< youtube FXKsBKKB_Xg >}}

Java is not only the server language running on heavy machines! You can do amazing stuff with it on a small single-board computer and gain new knowledge simultaneously, like controlling electronic components and different communication protocols.

A Raspberry Pi is a full Linux PC with a small form factor and a low price of between 12 and 98€. And, of course, you can run Java on it. The same kind of JVM applications you know, love, and use on heavy machines can also be used on the Raspberry Pi. "Write once, run everywhere"? Ah yes, that's the promise of Java! But this small board has some additional possibilities you will not find on that fancy server you are running somewhere in the cloud. All Raspberry Pis have those 40 magical pins to connect an unlimited choice of electronic components. Measuring temperatures and distances, toggling LEDs and relays, controlling the content on a LED matrix or LCD display, playing the Star Wars tune on a buzzer,... the only limit is your imagination!

In this talk, we'll look at the current state of Pi4J (www.pi4j.com) and dive into the code of a few examples. We'll experiment with Java on a CrowPi - a Raspberry Pi-based laptop - to interact with electronic components. And let's add Spring Boot and Vaadin into the mix to build a web interface to expose the data of those components. Maybe, if the wifi-conference-Gods are with us, it may even be possible to have everyone in the room interact with the application running on this mini-computer.
