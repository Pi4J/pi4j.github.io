---
title: '2026 Pi4J Smoke Tests with Pi4J'
date: 2026-03-30
tags: ["Video", "FFM", "Ikalogic"]
---

## Validating Pi4J V4 on real hardware, catching bugs, and exploring the Ikalogic logic analyser

**20260330 - Video with Tom Aarts**

{{< youtube uy3oWn9iIWs >}}

Pi4J contributor Tom Aarts joins Frank Delporte for a hands-on session focused on hardware testing in Pi4J V4. Tom has been a long-time contributor to the Pi4J ecosystem. He added example devices, improved core code by finding gaps through real-world usage, and most recently designed the Pi4J Smoke Test hardware setup that makes integration testing on real Raspberry Pi hardware practical and repeatable.

This video covers the design philosophy behind the smoke tests, a live demo of how they were used to reproduce a real bug (virtual thread pinning in the FFM plugin causing only 4 of 8 button listeners to fire on a 4-core Raspberry Pi), and a first look at using the affordable Ikalogic SE254 logic analyser to visualise PWM and SPI signals directly on the wires.

We also talk about the upcoming Pi4J drivers library, Tom's planned example rework, and an honest look at what AI-assisted coding with GitHub Copilot and Claude actually feels like in practice — including the risk of taking on too many parallel sessions at once.

* [Pi4J website](https://www.pi4j.com/)
* [What's new in Pi4J V4](https://www.pi4j.com/about/info-v4/)
* [FFM plugin interview with Nick Gritsenko](https://www.pi4j.com/blog/2026/20260220-interview-nick-ffm/)
* [Pi4J Smoke Test documentation](https://www.pi4j.com/hardware-testing/hardware-testing/)
* [Smoke Test source and README](https://github.com/Pi4J/pi4j/blob/develop/pi4j-test/README.md)
* [Bug report: issue #622](https://github.com/Pi4J/pi4j/issues/622)
* [Bug fix: PR #623](https://github.com/Pi4J/pi4j/pull/623)
* [Ikalogic SE254 logic analyser](https://ikalogic.com/logic-analyzers/se254/intro/)
* [Ikalogic ScanaStudio software](https://ikalogic.com/logic-analyzers/se254/software/)
* [Pi4J example devices (Tom's repository)](https://github.com/Pi4J/pi4j-example-devices)