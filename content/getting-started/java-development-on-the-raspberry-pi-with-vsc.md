---
title: Java development with VSC
weight: 40
---

## Java on the Raspberry Pi

To use Pi4J V2 you'll need Java 11 or newer. Luckily this version is included in the current version of Raspbian OS. 
In the release notes of Raspbian you can see that the version of 2019-06-20 includes OpenJDK Java 11:

```
2019-06-20:
Based on Debian Buster
Oracle Java 7 and 8 replaced with OpenJDK 11
```

But you will need to keep in mind this version is only compatible with ARMv7 or higher and doesn't support all 
Raspberry Pi board versions. If you have a Raspberry Pi A (version 3), B (version 2 or higher), 
or Compute (version 3 or higher), you are good to go! For all other boards you will need some additional steps 
that are described on ["Java installation"](/documentation/java-installation/).

If you prepared a microSD card with the latest version of Raspbian OS (full version), as described on 
["Set up a new Raspberry Pi"](/getting-started/set-up-a-new-raspberry-pi/), you can check the installed Java version 
in the terminal. On a board with ARMv7 or ARMv8 you will get this result:

```
$ java -version
openjdk version "11.0.3" 2019-04-16
OpenJDK Runtime Environment (build 11.0.3+7-post-Raspbian-5)
OpenJDK Server VM (build 11.0.3+7-post-Raspbian-5, mixed mode)
```

If you get an error like below, you'll need to follow the steps described on ["Java installation"](/documentation/java-installation/).

```
$ java -version
Error occurred during initialization of VM
Server VM is only supported on ARMv7+ VFP
```

## Maven

TODO describe maven installation

## Visual Studio Code

Visual Studio Code (VSC) is the free IDE (Integrated Developer Environment) by Microsoft. It's designed as a universal
tool which you can use for multiple programming languages with extensions. On your Raspberry Pi open a webbrowser,
go to the ["VSC Download page (code.visualstudio.com/Download)"](https://code.visualstudio.com/Download) and 
select the "Linux .deb ARM" version.

{{< gallery >}}
{{< figure link="/assets/getting-started/vsc/visualstudiocode-download.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/vsc/visualstudiocode-32bit.png" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/vsc/" caption="" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

When the download is finished, open a terminal, go to the Download directory and install the downloaded deb-file like this:

```
$ cd /home/pi/Downloads
$ sudo apt install ./code_1.53.0-1612367698_armhf.deb 
```

TODO add screenshot VSC in programming section
TODO add screenshot VSC with Java extensions.