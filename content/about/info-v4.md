---
title: 'What''s New in V4'
weight: 23
tags: ["FFM API"]
---

Versions 4.0.0 is based on 3.0.3 (released on 2025-09-23), but bumps the **Java version to 25** and has a new plugin that uses the Foreign Function & Memory (FFM) API. See the [release notes](/about/release-notes/).

## FFM Plugin

The goal of this bump to V4 is to enable the use of the Foreign Function & Memory (FFM) API in Pi4J. This FFM API has been introduced in OpenJDK 22 and simplifies the use of native libraries in Java. And native libraries are "the heart" of the Pi4J project as they provide the connection between your Java code and the hardware.

Thanks to the contributions by [Nick Gritsenko (aka DigitalSmile)](https://github.com/DigitalSmile) in [pull request #458](https://github.com/Pi4J/pi4j/pull/458), a complete new plugin got added to Pi4J. Read more about the work by Nick in this [interview](/blog/2025/2025????-interview-nick-ffm/).

## Sources

The Pi4J V4 source code is available in this GitHub repository: [`pi4j/pi4j` GitHub Repository](https://github.com/Pi4J/pi4j)

```shell
git clone https://github.com/Pi4J/pi4j
```
