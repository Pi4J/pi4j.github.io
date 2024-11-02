---
title: Install Java and Tools
weight: 18
---

Our Raspberry Pi has started for the first time and we are now ready to add some Java to it!

## Add Missing Dependencies

Let's start with some helper tools that will be useful later.

```shell
sudo apt install -y i2c-tools vim git java-common libxi6 libxrender1 libxtst6
```

## Install Java

There are many ways you can install Java. The easiest way to make Java available for both normal use and as root user (`sudo`), is the following approach:

### For 64-bit Operating System

```shell
cd ~/Downloads
wget https://cdn.azul.com/zulu/bin/zulu21.38.21-ca-jdk21.0.5-linux_arm64.deb
sudo dpkg -i zulu21.38.21-ca-jdk21.0.5-linux_arm64.deb
```

### For 32-bit Operating System

To be used when you selected a 32-bit version of the Operating System in the Imager tool

```shell
mkdir -p ~/Downloads
cd ~/Downloads
wget https://cdn.azul.com/zulu-embedded/bin/zulu17.52.17-ca-jdk17.0.12-c2-linux_aarch32hf.tar.gz
TODO
```

### Test Java Installation

Now you should be able to check the Java version with the following command:

```shell
$ java -version
openjdk version "21.0.5" 2024-10-15 LTS
OpenJDK Runtime Environment Zulu21.38+21-CA (build 21.0.5+11-LTS)
OpenJDK 64-Bit Server VM Zulu21.38+21-CA (build 21.0.5+11-LTS, mixed mode, sharing)
```

## Install JavaFX

TODO

## Install SDKMAN and Other Tools

For some of the examples, [Maven](https://maven.apache.org/) and/or [JBang](https://www.jbang.dev/) are used. The easiest way to install these, is by using [SDKMAN](https://sdkman.io/):

```shell
# Instal SDKMAN
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
script: 5.18.2
native: 0.4.6

$ mvn -v
Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
Maven home: /home/pi4j/.sdkman/candidates/maven/current
Java version: 21.0.5, vendor: Azul Systems, Inc., runtime: /usr/lib/jvm/zulu-21-arm64
Default locale: en_GB, platform encoding: UTF-8
OS name: "linux", version: "6.6.51+rpt-rpi-v8", arch: "aarch64", family: "unix"

$ jbang --version
0.119.0
```

