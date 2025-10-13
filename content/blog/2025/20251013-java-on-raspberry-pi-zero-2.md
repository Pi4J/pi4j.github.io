---
title: "Java 21+ on RPi Zero 2"
date: 2025-10-13
tags: ["Zero 2"]
---

2025-10-13, by Frank Delporte

As described before on [Java 21+ Not Working on Zero 2](/blog/2025/20250625-java-21-not-working-on-zero-2/), a problem appeared to execute Java code on the Raspberry Pi Zero 2 with OpenJDK 21 or higher. Reason: in OpenJDK 21 the Just-In-Time (JIT) compiler has been improved, but this change doesn’t work correctly on the ARM Cortex-A53 processor as used in the Zero 2. It's another type of processor compared to, for instance, the Raspberry Pi 4 (Cortex-A72) and 5 (Cortex-A76).

A bug was reported in the OpenJDK project: [[AArch64] Incorrect result of VectorizedHashCode intrinsic on Cortex-A53](https://bugs.openjdk.org/browse/JDK-8353237) with a solution to become available in a future release. 

Let's check with the latest releases of OpenJDK 21 and 25 if the problem is solved.

## Reproducing The Problem

I prepared a Raspberry Pi Zero 2 for the previous blog post, so took it out of my "experimentation box" to reproduce the problem. With the Java 24 version, installed at that time, the problem still exists. You can run `java` to get its version, but it throws an error when you try to execute any Java code.

```shell
$ java -version
openjdk version "24.0.2" 2025-07-15
OpenJDK Runtime Environment Zulu24.32+13-CA (build 24.0.2+12)
OpenJDK 64-Bit Server VM Zulu24.32+13-CA (build 24.0.2+12, mixed mode, sharing)

$ java HelloWorld.java
An exception has occurred in the compiler ((version info not available)). Please file a bug against the Java compiler via the Java bug reporting page (https://bugreport.java.com) after checking the Bug Database (https://bugs.java.com) for duplicates. Include your program, the following diagnostic, and the parameters passed to the Java compiler in your report. Thank you.
java.lang.NoClassDefFoundError: com/sun/tools/javac/jvm/ClassReader$AttributeReader
	at jdk.compiler/com.sun.tools.javac.jvm.ClassReader.initAttributeReaders(ClassReader.java:886)
	...
```

I also tried the previous version of Zulu 21 (based on OpenJDK 21.0.7, released on April 15, 2025). It has the same problem:

```shell
$ sdk install java 21.0.8-zulu

$ java -version
openjdk version "21.0.7" 2025-04-15 LTS
OpenJDK Runtime Environment Zulu21.42+19-CA (build 21.0.7+6-LTS)
OpenJDK 64-Bit Server VM Zulu21.42+19-CA (build 21.0.7+6-LTS, mixed mode, sharing)

$ java HelloWorld.java
An exception has occurred in the compiler ((version info not available)). Please file a bug against the Java compiler via the Java bug reporting page (https://bugreport.java.com) after checking the Bug Database (https://bugs.java.com) for duplicates. Include your program, the following diagnostic, and the parameters passed to the Java compiler in your report. Thank you.
java.lang.NoClassDefFoundError: com/sun/tools/javac/jvm/ClassReader$AttributeReader
	at jdk.compiler/com.sun.tools.javac.jvm.ClassReader.initAttributeReaders(ClassReader.java:841)
	...
```

## Fixed with Latest OpenJDK 21 and 25

With the latest builds of Zulu 21 (based on OpenJDK 21.0.8, released on July 15, 2025) and Zulu 25 (based on OpenJDK 25.0.0, released on September 16, 2025), the problem is solved!

```shell
$ sdk install java 21.0.8-zulu

$ java -version
openjdk version "21.0.8" 2025-07-15 LTS
OpenJDK Runtime Environment Zulu21.44+17-CA (build 21.0.8+9-LTS)
OpenJDK 64-Bit Server VM Zulu21.44+17-CA (build 21.0.8+9-LTS, mixed mode, sharing)

$ java HelloWorld.java
Hello, World!

$ sdk install java 25-zulu

$ java -version
openjdk version "25" 2025-09-16 LTS
OpenJDK Runtime Environment Zulu25.28+85-CA (build 25+36-LTS)
OpenJDK 64-Bit Server VM Zulu25.28+85-CA (build 25+36-LTS, mixed mode, sharing)

$ java HelloWorld.java
Hello, World!
```

## Conclusion

Switching to the latest version of an OpenJDK build not only brings you security and performance improvements. It can also solve other problems, for instance, this one which is related to the hardware running your application. 
