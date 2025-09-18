---
title: Install Java and Tools
weight: 18
tags: ["Pi4J OS", "Java", "JavaFX", "JBang", "Maven", "SDKMAN"]
---

Our Raspberry Pi has started for the first time and we are now ready to add some Java to it!

{{% notice tip %}}
As described on the previous page "The First Boot", a script can be executed that will do all this at once: `curl -sL https://raw.githubusercontent.com/Pi4J/pi4j-os/main/script/prepare-for-java.sh | bash`.
{{% /notice %}}

## Add Missing Dependencies

Let's start with some helper tools that will be useful later.

```shell
$ sudo apt install -y i2c-tools vim git java-common libxi6 libxrender1 libxtst6
```

* `i2c-tools`: Tool to help you with I2C commands.
* `vim`: Text editor like `nano`, preferred by some, hated by others ;-) 
* `git`: Tool to interact with a Git repository, like GitHub.
* `java-common libxi6 libxrender1 libxtst6`: Dependencies of the JDK Debian package.

## Install Java

There are many ways you can install Java. The easiest way to make Java available for both normal use and as root user (`sudo`), is the following approach which downloads one of the many distributions that are available. 

With the following commands you can get Java 25 installed. Starting from Pi4J V4, this is the minimal required version. For Pi4J V3, the minimal Java version is 21. If you are using a previous version of Pi4J, you can still use Java 11.

```shell
$ wget https://cdn.azul.com/zulu/bin/zulu25.28.85-ca-fx-jdk25.0.0-linux_arm64.deb
$ sudo dpkg -i zulu25.28.85-ca-fx-jdk25.0.0-linux_arm64.deb
$ rm zulu25.28.85-ca-fx-jdk25.0.0-linux_arm64.deb
```

{{% notice warning %}}
This approach only works on a 64-bit system as you can see from the `arm64` in the file name. For more info about running Java on a 32-bit system, check [Java for ARMv6/7/8](/documentation/java-for-arm/).
{{% /notice %}}

### Test Java Installation

Now you should be able to check the Java version with the following command:

```shell
$ java -version
openjdk version "25" 2025-09-16 LTS
OpenJDK Runtime Environment Zulu25.28+85-CA (build 25+36-LTS)
OpenJDK 64-Bit Server VM Zulu25.28+85-CA (build 25+36-LTS, mixed mode, sharing)
```

## Install JavaFX

If you want to use JavaFX on your Raspberry Pi, you have a few choices:

* Install a JDK with JavaFX included from a download, e.g. [Azul Zulu](https://www.azul.com/downloads/?version=java-25&os=debian&package=jdk-fx#zulu).
* Install a JDK with JavaFX included with SDKMAN, e.g. with `sdk install java 225.fx-zulu`.
* Use a script to download the JavaFX runtime from Gluon, e.g. from the [GitHub project pi4j-example-javafx](https://github.com/Pi4J/pi4j-example-javafx/tree/main) > `download_openjfx.bat` or `download_openjfx.sh` script.

## Install SDKMAN, Maven, and JBang

For some of the examples, [Maven](https://maven.apache.org/) and/or [JBang](https://www.jbang.dev/) are used. The easiest way to install these, is by using [SDKMAN](https://sdkman.io/):

```shell
# Install SDKMAN
$ curl -s "https://get.sdkman.io" | bash
$ source "$HOME/.sdkman/bin/sdkman-init.sh"

# Install Maven
$ sdk install maven
# Install JBang
$ sdk install jbang

# Update SDKMAN to the latest version, whenever needed
sdk update

# Checked the installed versions
$ sdk version
SDKMAN!
script: 5.20.0
native: 0.7.4 (linux aarch64)

$ mvn -v
Apache Maven 3.9.10 (5f519b97e944483d878815739f519b2eade0a91d)
Maven home: /home/frank/.sdkman/candidates/maven/current
Java version: 25, vendor: Azul Systems, Inc., runtime: /usr/lib/jvm/zulu-fx-25-arm64
Default locale: en_GB, platform encoding: UTF-8
OS name: "linux", version: "6.12.34+rpt-rpi-2712", arch: "aarch64", family: "unix"

$ jbang --version
0.131.0
```

