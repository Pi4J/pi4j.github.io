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
operating system you use. In all the documentation here for Pi4J, we use the official Raspberry Pi Operating System (formerly known as "Raspbian OS"). But there is a long list of other possibilities which is listed, for example, on the ["Awesome Raspberry Pi" list on GitHub](https://github.com/thibmaek/awesome-raspberry-pi/blob/master/README.md).

{{% notice tip %}}
Do you already have a Raspberry Pi with an up-to-date Operating System, and Java 17 or newer? Then you are good to go and can skip forward to the [Getting Started with Pi4J](/getting-started/) section! The information given in this part of our website is mainly focusing on anyone starting with Java on the Raspberry Pi.
{{% /notice %}}

## What Do We Need?

The Raspberry Pi doesn't come with a hard disk like typical computers. The operating system needs to be "burned" onto an SD Card. 

{{% notice tip %}}
Instead of an SC Card you can use an NVMe SSD disk. This requires an additional connection cable or hat, for instance, the [Raspberry Pi SSD Kit](https://www.raspberrypi.com/products/ssd-kit/). The advantage of such a system is a faster startup and disc access, but is not required for any of the examples explained on this website.
{{% /notice %}}

### Material list

This is the list of materials needed to get you started:

* Raspberry Pi (4, 5, or Pi Zero 2 is recommended, but older versions also work with Java and Pi4J!)
* Micro SD card, minimally 16Gb
* PC (or other Raspberry Pi) with an SD card slot (maybe you will need an SD card adapter)
* Power supply (5V, a Raspberry Pi 5 needs one that can provide 5A = 25W)
* Monitor, keyboard, mouse

### Step-by-step

First step: take your new Raspberry Pi out of the box of course :-)

Take a good look at it, what you are holding in your hands is a true masterpiece. A wonder of technical
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
