---
title: Java Development
weight: 40
tags: ["Visual Studio Code"]
---

## Java on the Raspberry Pi

{{% notice info %}}
Please check the [Prepare a Raspberry Pi](/prepare/install-java/) and [Install Java and Tools](/prepare/install-java/) instructions. 
{{% /notice %}}

You need Java 21 or newer to use Pi4J V3+. On a board with ARMv7 or ARMv8 you will get this result:

```shell
$ java -version
openjdk version "21.0.5" 2024-10-15 LTS
OpenJDK Runtime Environment Zulu21.38+21-CA (build 21.0.5+11-LTS)
OpenJDK 64-Bit Server VM Zulu21.38+21-CA (build 21.0.5+11-LTS, mixed mode, sharing)
```

Keep in mind this version is **only compatible with ARMv7 or higher** and doesn't support all
Raspberry Pi board versions. If you have a Raspberry Pi A (version 3), B (version 2 or higher),
or Compute (version 3 or higher), you are good to go! For all other boards, or if you get the error below, 
you will need some additional steps that are described on [Java for ARMv6/7/8](/documentation/java-installation/).

```shell
$ java -version
Error occurred during initialization of VM
Server VM is only supported on ARMv7+ VFP
```

## Maven

{{% notice info %}}
If you followed the steps described on [Prepare a Raspberry Pi](/prepare/install-java/) and [Install Java and Tools](/prepare/install-java/), 
you already have Mave installed.
{{% /notice %}}

Pi4J is using Maven as build tool, this allows you to compile your code with the required modules 
into JAR-file thanks to the `pom.xml` configuration file which you can find in the root of a project. 
We need to install Maven and can do this with a single command, after which we can immediately check the installation by requesting the version:

```shell
$ sudo apt install maven
$ mvn -v
Apache Maven 3.6.0
Maven home: /usr/share/maven
```

## Visual Studio Code

Please check [Prepare a Raspberry Pi > Install Visual Studio Code](/prepare/install-vsc-ide) for more info if you want to develop Java code directly on the Raspberry Pi.

