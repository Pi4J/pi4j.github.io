---
title: Java development with VSC
weight: 40
---

## Java on the Raspberry Pi

To use Pi4J V2 you'll need Java 11 or newer. Luckily this version is included in the current version of Raspbian OS. In the release notes of Raspbian you can see that the version of 2019-06-20 includes OpenJDK Java 11:

```
2019-06-20:
Based on Debian Buster
Oracle Java 7 and 8 replaced with OpenJDK 11
```

But you will need to keep in mind this version is only compatible with ARMv7 or higher and doesn't support all Raspberry Pi board versions.
If you have a Raspberry Pi A (version 3), B (version 2 or higher), or Compute (version 3 or higher), you are good to go! For all other boards
you will need some additional steps which are described on "[Java installation](/documentation/java-installation/)"

If you prepared a microSD card with the latest version of Raspbian OS (full version), you can check the installed Java version in the terminal. On a board with ARMv7 or ARMv8 you will get this result:

```
$ java -version
openjdk version "11.0.3" 2019-04-16
OpenJDK Runtime Environment (build 11.0.3+7-post-Raspbian-5)
OpenJDK Server VM (build 11.0.3+7-post-Raspbian-5, mixed mode)
```

## Visual Studio Code

