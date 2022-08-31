---
title: Java development with VSC
weight: 40
tags: ["Visual Studio Code"]
---

## Java on the Raspberry Pi

To use Pi4J V.2 you'll need Java 11 or newer. Luckily this version is included in the current version of Raspberry Pi OS. 
In the release notes you can see that the version of 2019-06-20 includes OpenJDK Java 11:

```shell
2019-06-20:
Based on Debian Buster
Oracle Java 7 and 8 replaced with OpenJDK 11
```

But you will need to keep in mind this version is **only compatible with ARMv7 or higher** and doesn't support all 
Raspberry Pi board versions. If you have a Raspberry Pi A (version 3), B (version 2 or higher), 
or Compute (version 3 or higher), you are good to go! For all other boards you will need some additional steps 
that are described on ["Java for ARMv6/7/8"](/documentation/java-installation/).

If you prepared a microSD card with the latest version of Raspberry Pi OS (full version), as described on 
["Set up a new Raspberry Pi"](/getting-started/set-up-a-new-raspberry-pi/), you can check the installed Java version 
in the terminal. On a board with ARMv7 or ARMv8 you will get this result:

```shell
$ java -version
openjdk version "11.0.3" 2019-04-16
OpenJDK Runtime Environment (build 11.0.3+7-post-Raspbian-5)
OpenJDK Server VM (build 11.0.3+7-post-Raspbian-5, mixed mode)
```

If you get an error like below, you'll need to follow the steps described on ["Java for ARMv6/7/8"](/documentation/java-installation/).

```shell
$ java -version
Error occurred during initialization of VM
Server VM is only supported on ARMv7+ VFP
```

## Maven

Pi4J is using Maven as build tool, this allows you to compile your code with the required modules into JAR-file thanks 
to the pom.xml configuration file which you can find in the root of a project. We need to install Maven and can do this
with a single command, after which we can immediately check the installation by requesting the version:

```shell
$ sudo apt install maven
$ mvn -v
Apache Maven 3.6.0
Maven home: /usr/share/maven
```

## Visual Studio Code

Visual Studio Code (VSC) is the free IDE (Integrated Developer Environment) by Microsoft. It's designed as a universal
tool that you can use for multiple programming languages with extensions. On your Raspberry Pi open a web browser,
go to the ["VSC Download page (code.visualstudio.com/Download)"](https://code.visualstudio.com/Download) and 
select the "Linux .deb ARM" version.

{{< gallery >}}
{{< figure link="/assets/getting-started/vsc/visualstudiocode-download.png" caption="Download page for VSC" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/vsc/programming-tools.png" caption="VSC in the list of programming tools" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/vsc/vsc-on-raspberry-pi.png" caption="VSC running on the Raspberry Pi with Maven and Java Extension Pack" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

When the download is finished, open a terminal, go to the Download directory and install the downloaded deb-file like this:

```shell
$ cd /home/pi/Downloads
$ sudo apt install ./code_1.53.0-1612367698_armhf.deb 
```

Since 02/2021 there is even an easier way, as Visual Studio Code is now available as a Raspberry Pi OS apt package. 
Use the following commands:

```shell
$ sudo apt update
$ sudo apt install code -y
```

