---
title: Welcome to Pi4J
---

## Welcome to Pi4J

**Latest release: V4.0.0 (2025-??-??, see [Release Notes](/about/release-notes/)).**

This project is intended to provide **a friendly object-oriented I/O API and implementation libraries for Java Programmers** to access the **full I/O capabilities of the Raspberry Pi platform**. This project abstracts the low-level native integration and interrupt monitoring to enable Java programmers to **focus on implementing their application business logic**.

If you immediately want to "dive" into Pi4J development, check these resources:

* [Prepare a Raspberry Pi for Java development](https://www.pi4j.com/prepare/).
* Starter examples: [Creating a single file application with JBang](/examples/jbang/jbang_minimal_example).
* For experienced Java developers: [Creating an application with Maven or Gradle](/getting-started/minimal-example-application).

### Brief History

**The Pi4J Project** was started in **2012**, the same year the Raspberry Pi was introduced 
as a tool to provide Java developers a simple and familiar object-oriented interface library 
to access the low-level I/O capabilities of the Raspberry Pi including **GPIO**, **I2C**, 
**SPI**, **PWM** and **Serial** communications.

The Pi4j project has evolved in all these years as the whole Java eco-system and Raspberry Pi systems have been evolving. This resulted in the following main versions:

* [V1.X](/about/info-v1): Deprecated, based on Java 8, later Java 11.
* [V2.X.X](/about/info-v2): Completely reworked code base, based on Java 11.
  * In 2.5.0, support for the Raspberry Pi 5 was added. Because of the new [GPIO chip RP1](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html), a new GPIO Provider was needed. See the [this interview](/blog/2024/20240318_interview_alexander_liggesmeyer/).
* [V3.X.X](/about/info-v3): Based on Pi4J 2.8.0 and Java 21.
  * Please [read this blog post for more info](/blog/2025/20250211-welcome-java-21/).

### Project Mission/Goals

**The Pi4J Project's** mission is to provide a **rich and powerful, yet simple to use, 
Java-friendly API library** enabling programmatic access to the low-level hardware I/O 
capabilities of embedded platforms such as the Raspberry Pi.

![](/assets/about/home/pi4j-overview.jpg)

