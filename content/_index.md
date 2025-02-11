---
title: Welcome to Pi4J
---

## Welcome to Pi4J

{{% notice warning %}}
**Pi4J is moving to Java version 21!** Please [read this blog post for more info](/blog/2025/20250211-welcome-java-21/). 3.0.0-SNAPSHOT of Pi4J is already available for testing from the Maven Repository if you enable snapshots in your pom-file.
{{% /notice %}}

**Latest release: V2.8.0 (2025-01-28, see [Release Notes](/about/release-notes/)).**

This project is intended to provide **a friendly object-oriented I/O API and implementation libraries for Java Programmers** to access the **full I/O capabilities of the Raspberry Pi platform**. This project abstracts the low-level native integration and interrupt monitoring to enable Java programmers to **focus on implementing their application business logic**.

{{% notice note %}}
Pi4J supports the new Raspberry Pi 5 as of version 2.5.0. Because of the new [GPIO chip RP1](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html), a new GPIO Provider was needed. See the [release notes for more info](/about/release-notes/).
{{% /notice %}}

If you immediately want to "dive" into Pi4J development, check these resources:

* Starters: [Creating a single file application with JBang](/examples/jbang/jbang_minimal_example).
* Experienced Java developer: [Creating an application with Maven or Gradle](/getting-started/minimal-example-application).

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

The Pi4j project has evolved in all these years as the whole Java eco-system and Raspberry Pi systems have been evolving.

This resulted in the following main versions:

* [V1.X](/about/info-v1): Deprecated, based on Java 8, later Java 11.
* [V2.X.X](/about/info-v2): Completely reworked code base, based on Java 11.
* [V3.X.X](/about/info-v3): Based on latest V2 and Java 21.

