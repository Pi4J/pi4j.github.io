---
title: 'History & Versions'
weight: 5
---

## A Brief History of Pi4J

**The Pi4J Project** was started in **2012**, the same year the Raspberry Pi was introduced,
as a tool to provide Java developers a simple and familiar object-oriented interface library
to access the low-level I/O capabilities of the Raspberry Pi including **GPIO**, **I2C**,
**SPI**, **PWM** and **Serial** communications.

The Pi4J project has evolved over all these years as the whole Java eco-system and Raspberry Pi systems have been evolving. This resulted in the following main versions:

* [V1.X](/about/info-v1): Deprecated, based on Java 8, later Java 11.
* [V2.X.X](/about/info-v2): Completely reworked code base, based on Java 11.
  * In 2.5.0, support for the Raspberry Pi 5 was added. Because of the new [GPIO chip RP1](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html), a new GPIO Provider was needed. See [this interview](/blog/2024/20240318_interview_alexander_liggesmeyer/).
* [V3.X.X](/about/info-v3): Based on Pi4J 2.8.0 and Java 21.
  * Please [read this blog post for more info](/blog/2025/20250211-welcome-java-21/).
* [V4.X.X](/about/info-v4): Based on Pi4J 3.0.3 and Java 25, introducing the [FFM plugin](/documentation/providers/ffm/).
    * Please [read this interview with Nick Gritsenko (aka DigitalSmile) for more info](/blog/2026/2026-interview-nick-ffm/).

In February 2026, **Pi4J was accepted into the [Commonhaus Foundation](https://www.commonhaus.org/)** to ensure the continuity of the project. Read more about it in [this blog post](/blog/2026/20260227-pi4j-commonhaus).
