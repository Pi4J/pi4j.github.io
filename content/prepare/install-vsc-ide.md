---
title: Install Visual Studio Code
weight: 19
---

You can develop Java applications on any computer and transfer the code or the compiled JAR-file to a Raspberry Pi to execute it. But Raspberry Pi 4 and 5 are definitely powerful enough to run an Integrated Development Environment (IDE)!

## Visual Studio Code

Visual Studio Code (VSC) is the free IDE (Integrated Developer Environment) by Microsoft. It's designed as a universal tool that you can use for multiple programming languages with extensions.

### Installing Visual Studio Code

You can download VSC directly from the website, but it's also available as a Raspberry Pi OS apt package. Use the following commands to install it from the terminal:

```shell
$ sudo apt update
$ sudo apt install code -y
```

### Adding Extensions

When VSC is installed, start it from "Start > Programming > Visual Studio Code". There are many extensions available to make it the perfect IDE for many programming languages and other tasks. Make sure to install the following ones to make it your perfect Java-companion:

* Java Extension Pack by Microsoft
* JBang

{{< gallery >}}
{{< figure link="/assets/prepare/vsc/visualstudiocode-download.png" caption="Download page for VSC" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/vsc/programming-tools.png" caption="VSC in the list of programming tools" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/vsc/vsc-on-raspberry-pi.png" caption="VSC running on the Raspberry Pi with Maven and Java Extension Pack" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}
