---
title: Set up a new Raspberry Pi
weight: 30
---

## Introduction

The Raspberry Pi is a powerful machine with many use-cases. A lot of this power is based on the 
operating system you use. For our "Getting Started" examples we will be using the "official Raspberry
Pi OS" (formerly known as "Raspbian OS") but there is a long list of other possibilities which is listed
for example on the["Awesome Raspberry Pi" list on GitHub](https://github.com/thibmaek/awesome-raspberry-pi/blob/master/README.md).

In this article we start with a brand new Raspberry Pi board.

## Step-by-step

First step: take your new Raspberry Pi out of the box of course :-)

Take a good look at it, what you are holding in your hands is a true master piece. A wonder of technical
engineering with a perfect mix of powerful yet inexpensive components.

But be aware! This is also some piece of sensitive electronics. It's always a good idea to first touch
the grounding pin of a power outlet to make sure your body is not electrically charged which could damage
one of the components on the board.

TODO add picture.

### Material list

* Raspberry Pi
* Micro SD card, minimally 16Gb b
* PC (or other Raspberry Pi) with an SD card slot (maybe you will need an SD card adapter)
* Power supply (5V, 2 or 3A)
* Monitor, keyboard, mouse

### SD card

The SD card will hold the operating system. On the Raspberry Pi website, [on the download page, you can
find the Imager tool](https://www.raspberrypi.org/software/). Select the version for your computer, download
and install it.

![Imager download](/assets/getting-started/setup/download-imager.png)

Start the Imager and follow these steps:

1. Click on "Operating System" > "CHOOSE OS"
2. Select "Raspberry Pi OS (other)"
3. Select "Raspberry Pi OS Full (32-bit)"

{{< gallery >}}
{{< figure link="/assets/getting-started/setup/imager-os-1.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-os-2.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-os-3.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

By selecting the "Full" edition, we will have an operating system which is preloaded with a load of additional tools,
including "OpenJDK 11", so will be able to take a quick start with Java development.

4. Put your SD card into your computer or in an SD card reader you can connect to USB
5. Click on "SD Card" > "CHOOSE SD CARD"
6. Select the SD card 

TODO add pictures

### First start-up

#### Additional Raspberry Pi OS settings

#### Check the Java version

As we have put the Full edition on the SD card, Java is already available. Open a terminal window and type in `java -version`.
Java will be started to show you the installed version.

```shell
$ java -version
openjdk version "11.0.9" 2020-10-20
OpenJDK Runtime Environment (build 11.0.9+11-post-Raspbian-1deb10u1)
OpenJDK Server VM (build 11.0.9+11-post-Raspbian-1deb10u1, mixed mode)
```

### Install Pi4J

TODO

## Keep your Raspberry Pi up-to-date

### Update to the latest version

Open a terminal and perform following commands

```shell
sudo apt update
sudo apt full-upgrade
```

Raspberry Pi OS is based on [Debian](https://www.debian.org/) - one of the largest Linux distrubutions. When running 
these commands regularly, you will keep your installation up to date for the particular major Raspberry Pi OS 
release you are using (e.g. Debian V9, aka Stretch). It will not update from one major release to another, for example, 
Stretch (V9) to Buster (V10). 
