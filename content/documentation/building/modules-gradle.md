---
title: Build Java modules with Gradle
weight: 164
tags: ["Gradle"]
---

{{% notice tip %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-example-minimal](https://github.com/Pi4J/pi4j-example-minimal)
{{% /notice %}}

The Pi4J project itself uses Maven and most example projects also use this build tool. But if you prefer to use Gradle,
you can start with a copy of the ["Minimal example application"](/getting-started/minimal-example-application/) which includes
all the required files to build with Gradle.

Use Gradle version 6.6 (or later) and Java 21 OpenJDK (or later). The Gradle wrapper is used as described on 
[docs.gradle.org](https://docs.gradle.org/current/userguide/gradle_wrapper.html). The Gradle configuration file 
[build.gradle-file](https://github.com/Pi4J/pi4j-example-minimal/blob/master/build.gradle) is included in the sources.

## Build with Gradle

On Linux:

`./gradlew build`

On Windows:

`gradlew.bat build`

## Build result

Once the build is complete and was successful, you can find the compiled `build` (Gradle) folder. Specifically
all dependency modules (JARs) and a simple `run.sh` bash script will be located in the `build/distribution` (Gradle) folder.

These are all the required files needed to distribute (copy) to your Raspberry Pi to run this project.  If you are using 
the native bindings running locally on the Raspberry Pi, then you make have to run the program using `sudo`
to gain the necessary access permissions to the hardware I/O.

This is the list of files created by the build process of this example application:

* pi4j-core
* pi4j-example-minimal
* pi4j-library-pigpio
* pi4j-plugin-pigpio
* pi4j-plugin-raspberrypi
* slf4j-api
* slf4j-simple
* run.sh --> this is the actual start file which will run pi4j-example-minimal

## Run on Raspberry Pi

Make the run script executable and start it like this:

```shell
$ chmod +x run.sh
$ sudo ./run.sh
```