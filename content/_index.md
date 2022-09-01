---
title: Welcome to Pi4J
---

## Welcome to Pi4J

**Latest release: V2.2.0 (2022-08-30, see [Release Notes](/about/release-notes/)).**

This project is intended to provide **a friendly object-oriented I/O API and implementation libraries 
for Java Programmers** to access the **full I/O capabilities of the Raspberry Pi platform**. This project 
abstracts the low-level native integration and interrupt monitoring to enable Java programmers to 
**focus on implementing their application business logic**.

### Brief History

**The Pi4J Project** was started in **2012**, the same year the Raspberry Pi was introduced 
as a tool to provide Java developers a simple and familiar object-oriented interface library 
to access the low-level I/O capabilities of the Raspberry Pi including **GPIO**, **I2C**, 
**SPI**, **PWM** and **Serial** communications.

### Project Mission/Goals

**The Pi4J Project's** mission is to provide a **rich and powerful, yet simple to use, 
Java-friendly API library** enabling programmatic access to the low-level hardware I/O 
capabilities of embedded platforms such as the Raspberry Pi.

![](/assets/about/home/pi4j-overview.jpg)

### Project Status Summary

The Pi4j project has evolved in all these years as the whole Java eco-system and Raspberry Pi systems
have been evolving.

This resulted in two main versions.

#### Version 1

The original library which started in 2012 and got a last release in 2021. Up till **version 1.3 the
library targets Java 8**, while **version 1.4 relies on Java 11**. More info is provided on 
["Previous versions (V.1)"](/about/previous-version-v1/).

#### Version 2

As of Version 2.0, Pi4J will **no longer include support for peripheral devices and
add-on chipsets/boards** as part of the core project. A new plugin model has been introduced
in version 2.0 that should help enable third-party development and support third-party
add-ons which may be developed and maintained independently of the core Pi4J project.

Read more on ["What's New (V.2)"](/about/new-in-v2/).
