---
title: "Interview Nick Gritsenko"
date: 2026-01-01
tags: ["FFM API"]
---

2026-??-?? by Frank Delporte

## Pi4J Goes Beyond Raspberry Pi with Java 22's FFM API

*Nick Gritsenko (aka [DigitalSmile](https://www.linkedin.com/in/nick-gritsenko/)) joined the Pi4J project recently with an interesting plugin that uses Java 22's Foreign Function & Memory API. His work could open up Pi4J to run on a significantly wider range of hardware than just Raspberry Pi.*

---

### About Nick

<img src="/assets/about/team/nick.jpg" style="float: left; margin: 0 15px 10px 0; max-width: 200px; max-height: 250px;">

**Frank:** Thanks for joining the Pi4J community! What's your background?

**Nick:** I work at Yandex in the infrastructure department. One of my tasks is to monitor the evolutions in compuer infrastructure. We're actually discussing moving from classic x86/AMD64 systems to ARM or even RISC-V in our data centers. The hardware landscape is changing fast, and I think RISC-V will make serious progress in the next 10 years.

**Frank:** What brought you to Pi4J?

**Nick:** I was already working on an [FFM API-based GPIO library for Raspberry Pi](https://github.com/DigitalSmile/gpio), and it seemed like a perfect fit to become a Pi4J plugin. The thing is, with FFM we can make Pi4J work on any hardware that runs Linux... Orange Pi, RISC-V system-on-chips, whatever. The FFM API basically lifts the hardware abstraction above the Linux ecosystem level.

### What is the FFM API

**Frank:** Can you explain what the FFM API is for readers who haven't heard of it?

**Nick:** The Foreign Function & Memory API is part of the [OpenJDK Project Panama](https://openjdk.org/projects/panama/), which actually started way back in 2014. The big difference between FFM and traditional approaches like JNI, JNA, or JNR is huge: **you don't need to know C or C++**. As Java developers, why should we have to become C++ experts just to talk to native code?

The traditional approaches have two main problems. First, writing production-ready C++ code requires deep expertise - you can't learn that from some "C++ in 21 days" book. Second, all those abstraction layers create serious runtime overhead with multiple layers the JVM has to handle.

**Frank:** How is FFM different?

**Nick:** With FFM, you stay in pure Java. Not a single line of C or C++ in your application. You describe C structures using Java, and FFM handles the conversion. Since it's pure Java bytecode, the JIT compiler can optimize it properly, so you can use it safely in, for example, high-load Spring applications.

### How it Works with Pi4J

**Frank:** How does this work in practice?

**Nick:** If you look, for example, at the [sources of the GPIO package structures](https://github.com/Pi4J/pi4j/tree/develop/plugins/pi4j-plugin-ffm/src/main/java/com/pi4j/plugin/ffm/common/gpio/structs) I've created, you'll see that they're Java representations of the C structures that describe how GPIO functionality works in Linux. You're building the same model that represents the C world, but in Java terms.

When you want to change a digital output state, you're calling `ioctl` directly from Java to the kernel. FFM automatically handles converting between Java objects and the native C world.

**Frank:** What about performance?

**Nick:** I've done measurements comparing the FFM implementation with existing Pi4J approaches. The results are impressive, as the removal of all the steps inbetween with JNI and JNA shows a big difference between the "old" implementation and the FFM plugin. Removing the abstraction layers brings big performance improvements.

```text
Benchmark                                                  Mode  Cnt     Score    Error  Units
GPIOPerformanceTest.testFFMInputRoundTrip                  avgt    5     0.173 ±  0.003  ms/op
GPIOPerformanceTest.testGpioDInputRoundTrip                avgt    5    10.537 ±  6.196  ms/op
GPIOPerformanceTest.testLinuxFsInputRoundTrip              avgt    5   111.781 ± 42.199  ms/op

Benchmark                                                  Mode  Cnt     Score    Error  Units
GPIOPerformanceTest.testFFMInputWithListenerRoundTrip      avgt    5     1.594 ±  5.830  ms/op
GPIOPerformanceTest.testGpioDInputWithListenerRoundTrip    avgt    5     9.015 ± 12.139  ms/op
GPIOPerformanceTest.testLinuxFsInputWithListenerRoundTrip  avgt    5   110.115 ± 18.796  ms/op

Benchmark                                                  Mode  Cnt     Score    Error  Units
GPIOPerformanceTest.testFFMOutputRoundTrip                 avgt    5     0.042 ±  0.001  ms/op
GPIOPerformanceTest.testGpioDOutputRoundTrip               avgt    5     0.110 ±  0.002  ms/op
GPIOPerformanceTest.testLinuxFsOutputRoundTrip             avgt    5   108.306 ± 12.490  ms/op
```

### Challenges

**Frank:** Are there any downsides to FFM?

**Nick:** The main issue is crash handling. If something in the native code throws an exception, your entire JVM crashes - not just your application. This isn't unique to FFM though. The potential solution would be sandboxing, where native crashes wouldn't kill the whole JVM, but I haven't seen concrete plans for that yet.

**Frank:** How do you handle different hardware requirements?

**Nick:** This is important - I'm strictly against putting any Raspberry Pi-specific code directly in the FFM implementation. Everything should go through plugins. Pi4J already has a plugin system for providers, but I think we should extend this to hardware-specific things... plugins for Raspberry Pi, Orange Pi, RISC-V chips, etc.

The beauty of FFM is that it works with any hardware running Linux. We're not abandoning Raspberry Pi, but we can expand to other platforms much easier. So we probably won't need to do any changes to Pi4J itself to have it working on other boards.

### Future Vision

**Frank:** Where do you see this going?

**Nick:** This opens up completely new possibilities. At work, we're already seeing the industry move toward ARM and RISC-V because Java runs much more efficiently on ARM than x86. With FFM, Pi4J can be part of that future across all these platforms.

The goal is making Pi4J truly platform-agnostic while keeping the ease of use Java developers expect. No more dealing with native libraries, compilation issues, or platform-specific builds.

When the previous plugins would be removed from Pi4J, and only the FFM plugin would remain, the Pi4J codebase would become much smaller, easier to maintain. Also, custom Docker builds for the native compilations of the JNI/JNA dependencies for those plugins could be removed, further simplifying the Pi4J code base.

**Frank:** Advice for developers who want to contribute?

**Nick:** The FFM learning curve isn't as steep as you might think. Once you understand the byte mathematics and how to map structures between Java and native worlds, it becomes straightforward - though I won't say it's just "copy and paste"!

I'd say about 70-80% of my time was spent understanding how FFM works. Once that clicked in my brain, development speeded up significantly.

### Getting Involved

**Frank:** How can the community help?

**Nick:** Testing is crucial. I've been working with a Raspberry Pi 5, and basic functionality like digital outputs works well. But we need testing across all providers to identify corner cases that only show up in real-world usage. We also need feedback from developers trying different hardware platforms. The more diverse our testing, the more robust the implementation becomes.

---

*Nick's work integrating Java 22's FFM API represents a big step forward for Pi4J, potentially opening doors to a much broader ecosystem of single-board computers and IoT devices. Try it out and let us know how it works!*

*Want to learn more about Pi4J or contribute? Check out the [GitHub repository](https://github.com/Pi4J/pi4j) or visit the [Pi4J website](https://www.pi4j.com).*