---
title: '2025 Devoxx Talk FFM API'
tags: ["Video"]
---

## The Wait is Over: Foreign Function & Memory FFM API brings modern Java to the Raspberry Pi

**20251009 - Recording of the talk at Devoxx Belgium by Frank Delporte**

All the links of the presentation are available [on this blog post](https://webtechie.be/post/2025-10-08-devoxx-talk-ffmapi-on-raspberrypi/).

{{< youtube 2BcWWWkb8ac >}}

Since 2012, Pi4J has enabled Java to control electronic components connected to the Raspberry Pi's GPIO pins. However, both Java and the Raspberry Pi have evolved significantly since then. Supporting new hardware has been a challenge, requiring multiple implementations in the Pi4J library with complex code based on the Java Native Interface (JNI) and Java Native Access (JNA). 

The Foreign Function & Memory (FFM) API, finalized in Java 22, promised to make such integrations with native code a lot easier. With Java reaching a new Long Term Support version, it’s time to bump the Pi4J project to Java 25 and make full use of FFM! 

In this talk, you’ll learn how this FFM implementation is much easier to support and achieves high performance due to less memory copying and less interop code. It will also help improve the Pi4J project: fewer dependencies, a smaller JAR footprint, support for more protocols, and compatibility with more SoCs, among other benefits. Through live demos, you will learn how to control LEDs, read buttons, interface with LCD displays, and gather sensor data using JBang single-file example applications. You'll see how FFM makes hardware interaction as natural as regular Java programming, and you will be ready to start your own experiments as soon as you arrive home. 

Target audience: Java developers interested in IoT, embedded systems, and hardware programming. Basic Java knowledge is required, but no prior experience with Pi4J or electronics is needed.
