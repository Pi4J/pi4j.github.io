---
title: Java development on the Raspberry Pi with Visual Studio Code
weight: 40
---

To use Pi4J V2 you'll need Java 11 or newer. Luckily this version is included in the current version of Raspbian OS. In the release notes of Raspbian you can see that the version of 2019-06-20 includes OpenJDK Java 11:

```
2019-06-20:
Based on Debian Buster
Oracle Java 7 and 8 replaced with OpenJDK 11
```

But you will need to keep in mind this version is only compatible with ARMv7 or higher and doesn't support all Rapberry Pi board versions.

Boards with ARMv6 processor:

*     Raspberry Pi 1 A and A+
*     Raspberry Pi 1 B and B+
*     Compute Module 1
*     Zero 1.2, 1.3 and W

Boards with ARMv7 or ARMv8 processor:

*     Model A+, version 3
*     Model B, version 2, 3 and 4
*     Compute Module, version 3

### Check the installed Java version

If you prepared a microSD card with the latest version of Raspbian OS (full version), you can check the installed Java version in the terminal. On a board with ARMv7 or ARMv8 you will get this result:

```
$ java -version
openjdk version "11.0.3" 2019-04-16
OpenJDK Runtime Environment (build 11.0.3+7-post-Raspbian-5)
OpenJDK Server VM (build 11.0.3+7-post-Raspbian-5, mixed mode)
```

On an ARMv6 version, you will get an error:

```
$ java -version
Error occurred during initialization of VM
Server VM is only supported on ARMv7+ VFP
```

### Check your board version

If you are not sure which type of board you have, you can check this in the terminal with “cat /proc/cpuinfo”, for instance for a Raspberry Pi B+ 1.2:

```
$ cat /proc/cpuinfo

processor	: 0
model name	: ARMv6-compatible processor rev 7 (v6l)
BogoMIPS	: 697.95
Features	: half thumb fastmult vfp edsp java tls 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x0
CPU part	: 0xb76
CPU revision	: 7

Hardware	: BCM2835
Revision	: 0010
Serial		: 000000005f9ba615
Model		: Raspberry Pi Model B Plus Rev 1.2
```

### Install Java 11 on ARMv6

The sources for Java are available as open-source on [OpenJDK](https://openjdk.java.net/), which means, if you can't find the correct version for a specific board, it is possible to compile it yourself. Luckily there are different suppliers providing ready-made packages of the JDK for multiple platforms. But only Azul seems to have one which is a perfect fit for Raspberry Pi's with an ARMv6: [the Zulu community edition of JDK 11](https://www.azul.com/downloads/zulu-community/?version=java-11-lts&os=linux&architecture=arm-32-bit-hf&package=jdk).

To get started with Zulu JDK, download and uncompress it to your board:

```
$ cd /usr/lib/jvm
$ sudo wget https://cdn.azul.com/zulu-embedded/bin/zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf.tar.gz
$ sudo tar -xzvf zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf.tar.gz
$ sudo rm zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf.tar.gz
$ ls -l
total 12
lrwxrwxrwx  1 root root   21 Jul 23 15:58 java-1.11.0-openjdk-armhf -> java-11-openjdk-armhf
drwxr-xr-x  9 root root 4096 Aug 20 11:41 java-11-openjdk-armhf
drwxr-xr-x  2 root root 4096 Aug 20 11:41 openjdk-11
drwxrwxr-x 10  111  122 4096 Jul 10 16:50 zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf
```

Now we have the JDK11 ready to be used, but it still needs to be configured so the OS is aware of it.

```
$ sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf/bin/java 1
$ sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf/bin/javac 1
```

At this moment we can select the new JDK to link it to the “java” and “javac” command.

```
$ sudo update-alternatives --config java
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                                             Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-armhf/bin/java                       1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-armhf/bin/java                       1111      manual mode
  2            /usr/lib/jvm/zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf/bin/java   1         manual mode

Press <enter> to keep the current choice[*], or type selection number: 2
update-alternatives: using /usr/lib/jvm/zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf/bin/java to provide /usr/bin/java (java) in manual mode

$ sudo update-alternatives --config javac
There are 2 choices for the alternative javac (providing /usr/bin/javac).

  Selection    Path                                                              Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-armhf/bin/javac                       1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-armhf/bin/javac                       1111      manual mode
  2            /usr/lib/jvm/zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf/bin/javac   1         manual mode

Press <enter> to keep the current choice[*], or type selection number: 2
update-alternatives: using /usr/lib/jvm/zulu11.41.75-ca-jdk11.0.8-linux_aarch32hf/bin/javac to provide /usr/bin/javac (javac) in manual mode
```

Now let's check the Java version:

```
$ java -version
openjdk version "11.0.8" 2020-07-14 LTS
OpenJDK Runtime Environment Zulu11.41+75-CA (build 11.0.8+10-LTS)
OpenJDK Client VM Zulu11.41+75-CA (build 11.0.8+10-LTS, mixed mode)
```

OK, ready to run Java 11 applications on the Raspberry Pi with ARMv6!

### More info

If you want more info, or use JavaFX, check these blog posts:

* [Installing Java and JavaFX on the Raspberry Pi (for ARMv7+)](https://webtechie.be/post/2020-04-08-installing-java-and-javafx-on-raspberry-pi/)
* [How to install and use Java 11 and JavaFX 11 on Raspberry Pi boards with ARMv6 processor](https://webtechie.be/post/2020-08-27-azul-zulu-java-11-and-gluon-javafx-11-on-armv6-raspberry-pi/)

