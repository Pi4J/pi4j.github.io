---
title: "Java 21+ Not Working on Zero 2"
date: 2025-06-25
tags: ["Zero 2"]
---

2025-06-25 by Frank Delporte

**Dieter Holz** was experimenting with Pi4J V3 on a Raspberry Pi Zero 2. Because this version requires Java 21 or newer, he upgraded his OS to a newer Java version and found out that no Java code could be executed. He tried with Java 21 and 24, and neither worked correctly, although Java 17 runs without problems.

The same SD card with Java 24 that didn't work on the Zero 2 worked perfectly on a Raspberry Pi 4. So, what is happening under the hood? What is the difference between these two boards causing this problem? Let's dive in.

## Differences Between RPi Zero 2 and RPi 4

As the same SD card was used to test on two different boards, the problem has to be related to the board itself, not the software. I repeated the test as Dieter did and used the latest Azul Zulu version [24.30.13, based on OpenJDK 24.0.1](https://www.azul.com/downloads/?version=java-24&os=linux&architecture=arm-64-bit&package=jdk-fx#zulu).

On both boards, the Java version could be read without any issues:

```bash
$ java -version
openjdk version "24.0.1" 2025-04-15
OpenJDK Runtime Environment Zulu24.30+13-CA (build 24.0.1+9)
OpenJDK 64-Bit Server VM Zulu24.30+13-CA (build 24.0.1+9, mixed mode, sharing)
```

But trying to execute or compile the simplest "Hello World" code resulted in errors on the Zero 2:

```bash
$ java HelloWorld.java

An exception has occurred in the compiler ((version info not available)). Please file a bug against the Java compiler via the Java bug reporting page (https://bugreport.java.com) after checking the Bug Database (https://bugs.java.com) for duplicates. Include your program, the following diagnostic, and the parameters passed to the Java compiler in your report. Thank you.

java.lang.NoClassDefFoundError: com/sun/tools/javac/processing/JavacProcessingEnvironment$DiscoveredProcessors
	at jdk.compiler/com.sun.tools.javac.processing.JavacProcessingEnvironment.initProcessorIterator(JavacProcessingEnvironment.java:331)
	...
	
$ javac HelloWorld.java

Exception in thread "main" java.lang.InternalError: Cannot find requested resource bundle for locale en_US
	at jdk.compiler/com.sun.tools.javac.util.JavacMessages.getBundles(JavacMessages.java:145)
	...
```

Let's try to find the difference between the two boards by executing a few commands...

| Command | RPi Zero 2 | RPi 4 |
| :--- | :--- | :--- |
| `cat /proc/cpuinfo` | Raspberry Pi Zero 2 W Rev 1.0 | Raspberry Pi 4 Model B Rev 1.2 |
| `uname -a` | Linux pizero2 6.12.25+rpt-rpi-v8 ... aarch64 GNU/Linux | idem |
| `uname -m`| aarch64 | aarch64 |
| `lscpu` | ... Model name: Cortex-A53 ... | ... Model name: Cortex-A72 ... |

Bingo! `lscpu` shows a different type of ARM processor. Could this be the reason for this problem?

## Changes in Java 21

Thanks to my colleagues at **Azul**, it immediately became clear that the Cortex-A53 is indeed causing Java to fail.

In Java 21 the Just-In-Time (JIT) compiler has been improved, but this change doesn't work correctly on the ARM Cortex-A53 processor as used in the Zero 2. This is another type of processor compared to, for instance, the Raspberry Pi 4 (Cortex-A72) and 5 (Cortex-A76).

A bug has been reported in the OpenJDK project: [[AArch64] Incorrect result of VectorizedHashCode intrinsic on Cortex-A53](https://bugs.openjdk.org/browse/JDK-8353237). At this moment, it's already marked as "Resolved" and ~~will be included in the July '25 update releases for versions 21, 24, and 25~~ is expected to be included in the 25 GA release (September '25).

The issue stems from the fact that the VectorizedHashCode intrinsic was implemented with assumptions about ARM64 processors that don't hold true for the Cortex-A53 specifically. The Cortex-A53 has different microarchitectural characteristics compared to other ARM64 processors, and the vectorized hash code implementation doesn't account for these differences.

This bug causes:

* **Incorrect hash code calculations** when the VectorizedHashCode intrinsic is used.
* **ClassNotFoundException and other runtime failures** because hash codes are fundamental to how the JVM manages classes, strings, and other objects.
* **Spring Boot applications fail to start** (as shown in the bug report) because the incorrect hash codes break class loading mechanisms.

If you want to explore the details of the JIT, you can read this [technical overview of the intrinsics and vector optimization systems in the OpenJDK JIT compiler (C2)](https://deepwiki.com/openjdk/jdk21u/3.2.2-intrinsics-and-vectorization).

## Workaround

As described in [Running Java 21+ on Raspberry Pi Zero 2](/documentation/java-for-arm/#running-java-21-on-raspberry-pi-zero-2), a workaround is available to execute Java code until the fix is included in the next release:

```bash
$ java -XX:+UnlockDiagnosticVMOptions -XX:-UseVectorizedHashCodeIntrinsic HelloWorld.java
Hello World
```

## Compare Boards

To help identify these kinds of issues that behave differently on different types of Raspberry Pi boards, the Board Info Service has been extended with a [Compare view](https://api.pi4j.com/board-compare?board2=MODEL_4_B&board1=ZERO_V2) where you can easily see the differences between two boards.

![](/assets/blogs/api/compare-boards.png)