---
title: Prepare a Raspberry Pi
weight: 15
aliases:
  - /pi4j-os/
  - /pi4j-os/prepare-sd-with-pi4j-os/
  - /pi4j-os/test-pi4j-basic-os/
  - /pi4j-os/test-pi4j-picade-os/
  - /blog/2023/20230731_pi4j_os/
---

The Raspberry Pi is a powerful machine with many use-cases. A lot of this power is based on the 
operating system you use. In all the documentation here for Pi4J we use the official Raspberry Pi Operating System (formerly known as "Raspbian OS"). But there is a long list of other possibilities which is listed,
for example, on the ["Awesome Raspberry Pi" list on GitHub](https://github.com/thibmaek/awesome-raspberry-pi/blob/master/README.md).

## Material list

* Raspberry Pi
* Micro SD card, minimally 16Gb b
* PC (or other Raspberry Pi) with an SD card slot (maybe you will need an SD card adapter)
* Power supply (5V, 2 or 3A)
* Monitor, keyboard, mouse

## Step-by-step

First step: take your new Raspberry Pi out of the box of course :-)

Take a good look at it, what you are holding in your hands is a true master piece. A wonder of technical
engineering with a perfect mix of powerful yet inexpensive components.

But be aware! This is also a sensitive piece of electronics! It's always a good idea to first touch
the grounding pin of a power outlet to make sure your body is not electrically charged which could damage
one of the components on the board.

The following steps:

{{% children %}}

After these steps, you can continue to the [Getting Started with Pi4J](/getting-started/) section for your first experiments with Java and electronic components.

## Pi4J OS

In the past, we had our own Pi4J OS, based on Raspberry Pi OS with some extra preparations to make it easier to use with Pi4J. But because it became incompatible with the Raspberry Pi 5 and was difficult to maintain, we no longer will update that Pi4J OS.

{{% notice tip %}}
You can still find it on GitHub: [https://github.com/Pi4J/pi4j-os](https://github.com/Pi4J/pi4j-os)
{{% /notice %}}
