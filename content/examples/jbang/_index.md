---
title: JBang Examples
weight: 150
tags: ["JBang"]
---

{{% notice tip %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-jbang](https://github.com/Pi4J/pi4j-jbang)
{{% /notice %}}

Want to get started with Java programming on the Raspberry Pi?

JBang is a great way to create your first program to control electronic components connected to the GPIO pins.
What is JBang?

## What is JBang?

As [described on their website](https://www.jbang.dev/):

*JBang lets Students, Educators and Professional Developers create, edit and run self-contained source-only Java programs with unprecedented ease.*

* *Want to learn, explore or use Java instantly without setup?*
* *Do you like Java but use python, groovy, kotlin or similar languages for scripts, experimentation and exploration?*
* *Ever wanted to just be able to run Java from anywhere without any or very minimal setup?*
* *Ever tried out Java 11+ support for running .java files directly in your shell but felt it was a bit too cumbersome?*

*JBang lets you do all this!*

## Get Started with JBang on Raspberry Pi

### Prerequisites

* A Raspberry Pi with recent Raspberry Pi OS.
* Install JBang as described on [jbang.dev/download](https://www.jbang.dev/download/). JBang will install Java if it's not installed yet.
```shell
# Install JBang
$ curl -Ls https://sh.jbang.dev | bash -s - app setup

# Check JBang by requesting its version
$ jbang --version        
0.109.0
```
* OPTIONAL: Use [Visual Studio Code](https://code.visualstudio.com/), the free IDE.
```shell
# Install Visual Studio Code
$ sudo apt install code
```
* OPTIONAL: Install the following extensions in Visual Studio Code:
    * [Language Support for Java(TM) by Red Hat](https://marketplace.visualstudio.com/items?itemName=redhat.java)
    * [JBang](https://marketplace.visualstudio.com/items?itemName=jbangdev.jbang-vscode)

### Example scripts

The [Pi4J JBang project on GitHub](https://github.com/Pi4J/pi4j-jbang) contains several examples to demonstrate both JBang and Pi4J. Each `java`-file is a full-containing runnable JBang application. This means you don't need Maven, Gradle, or other Java build tool.

To tell JBang that it must handle the file as a Java application and do some upfront preparation work, the first line in each file is: `///usr/bin/env jbang "$0" "$@" ; exit $?`.

When an application needs dependencies, they are defined inside the file itself in a line starting with `//DEPS`. For instance, to use the Pi4J Core library: `//DEPS com.pi4j:pi4j-core:2.3.0`.

Each of the provided examples contains more information about the wiring inside the file itself and are also explained here on the Pi4J website.

### Get the Examples from GitHub

You can clone the project with the examples to your Raspberry Pi in the terminal with the following commands:

```bash
$ git clone https://github.com/Pi4J/pi4j-jbang
$ cd pi4j-jbang
```

### Explained Examples 

The examples in the GitHub project are explained on these pages:

{{% children depth="1" %}}

## Video Demo

This approach to demonstrate Pi4J with JBang has been explained and demonstrated on Voxxed Days Brussels on May 23th, 2023.

{{< youtube w4AR4hWP3Qk >}}