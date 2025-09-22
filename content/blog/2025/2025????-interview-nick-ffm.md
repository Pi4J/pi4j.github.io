---
title: "Interview Nick Gritsenko"
date: 2025-01-15
tags: ["FFM API"]
---

2025-09-17 by Frank Delporte

## Pi4J Goes Beyond Raspberry Pi with Java 22's FFM API

*Nick Gritsenko (aka [DigitalSmile](https://www.linkedin.com/in/nick-gritsenko/)) joined the Pi4J project recently with an interesting plugin that uses Java 22's Foreign Function & Memory API. His work could open up Pi4J to run on a significantly wider range of hardware than just Raspberry Pi.*

---

### About Nick

**Frank:** Thanks for joining the Pi4J community! What's your background?

**Nick:** I work at Yandex in the infrastructure department. We're actually discussing moving from classic x86 AMD64 systems to ARM or even RISC-V in our data centers. The hardware landscape is changing fast, and I think RISC-V will make serious progress in the next 10 years.

**Frank:** What brought you to Pi4J?

**Nick:** I was already working on [an FFM API-based GPIO library for Raspberry Pi](https://github.com/DigitalSmile/gpio), and it seemed like a perfect fit to become a Pi4J plugin. The thing is, with FFM we can make Pi4J work on any hardware that runs Linux... Orange Pi, RISC-V system-on-chips, whatever. The FFM API basically lifts the hardware abstraction above the Linux ecosystem level.

### What is the FFM API

**Frank:** Can you explain what the FFM API is for readers who haven't heard of it?

**Nick:** The Foreign Function & Memory API is part of Project Panama, which actually started way back in 2014. The big difference between FFM and traditional approaches like JNI, JNA, or JNR is huge: **you don't need to know C or C++**. As Java developers, why should we have to become C++ experts just to talk to native code?

The traditional approaches have two main problems. First, writing production-ready C++ code requires deep expertise - you can't learn that from some "C++ in 21 days" book. Second, all those abstraction layers create serious runtime overhead with multiple layers the JVM has to handle.

**Frank:** How is FFM different?

**Nick:** With FFM, you stay in pure Java. Not a single line of C or C++ in your application. You just describe C structures using Java, and FFM handles the conversion. Since it's pure Java bytecode, the JIT compiler can optimize it properly, so you can use it safely in high-load Spring applications.

### How it Works with Pi4J

**Frank:** How does this work in practice?

**Nick:** If you look at the GPIO package structures I've created, they're Java representations of the C structures that describe how GPIO functionality works in Linux. You're building the same model that represents the C world, but in Java terms.

When you want to change a digital output state, you're calling `ioctl` directly from Java to the kernel. FFM automatically handles converting between Java objects and the native C world.

**Frank:** What about performance?

**Nick:** I've done measurements comparing the FFM implementation with existing Pi4J approaches. The results look promising, though we need to retest with JDK 25 and across all the providers we support. The performance improvements come from removing those abstraction layers and letting the JIT compiler optimize the bytecode.

### Challenges

**Frank:** Any downsides to FFM?

**Nick:** The main issue is crash handling. If something in the native code throws an exception, your entire JVM crashes - not just your application. This isn't unique to FFM though. The potential solution would be sandboxing, where native crashes wouldn't kill the whole JVM, but I haven't seen concrete plans for that yet.

**Frank:** How do you handle different hardware requirements?

**Nick:** This is important - I'm strictly against putting any Raspberry Pi-specific code directly in the FFM implementation. Everything should go through plugins. Pi4J already has a plugin system for providers, but I think we should extend this to hardware-specific things... plugins for Raspberry Pi, Orange Pi, RISC-V chips, etc.

The beauty of FFM is that it works with any hardware running Linux. We're not abandoning Raspberry Pi, but we can expand to other platforms much easier.

### Future Vision

**Frank:** Where do you see this going?

**Nick:** This opens up completely new possibilities. At work, we're already seeing the industry move toward ARM and RISC-V because Java runs much more efficiently on ARM than x86. With FFM, Pi4J can be part of that future across all these platforms.

The goal is making Pi4J truly platform-agnostic while keeping the ease of use Java developers expect. No more dealing with native libraries, compilation issues, or platform-specific builds.

**Frank:** Advice for developers who want to contribute?

**Nick:** The FFM learning curve isn't as steep as you might think. Once you understand the byte mathematics and how to map structures between Java and native worlds, it becomes straightforward - though I won't say it's just "copy and paste"!

I'd say about 70-80% of my time was spent understanding how FFM works. Once that clicked in my brain, development accelerated significantly.

### Getting Involved

**Frank:** How can the community help?

**Nick:** Testing is crucial. I've been working with a Raspberry Pi 5, and basic functionality like digital outputs works well. But we need testing across all providers to identify corner cases that only show up in real-world usage. Contributors like Tom, who's retired and has time to test with all sorts of components, are invaluable.

We also need feedback from developers trying different hardware platforms. The more diverse our testing, the more robust the implementation becomes.

---

*Nick's work integrating Java 22's FFM API represents a big step forward for Pi4J, potentially opening doors to a much broader ecosystem of single-board computers and IoT devices. Try it out and let us know how it works!*

*Want to learn more about Pi4J or contribute? Check out the [GitHub repository](https://github.com/Pi4J/pi4j-v2) or visit the [Pi4J website](https://www.pi4j.com).*