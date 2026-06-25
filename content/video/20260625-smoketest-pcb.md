---
title: '2026 Designing a Smoke Test PCB for Pi4J'
date: 2026-06-25
youtube: q7SGdxQnMVc
tags: ["Video", "Hardware Testing"]
---

## From breadboard chaos to a real PCB: designing the Pi4J smoke test board

**20260625 - Video with Frank Delporte**

{{< youtube q7SGdxQnMVc >}}

Testing a Java I/O library properly means testing it on real hardware. For Pi4J that means running the smoke test: a setup with two BMP/BME280 sensors and a tangle of GPIO-to-GPIO jumper wires that has to be rebuilt by hand every session. This video tells the story of board number `0001`: turning that breadboard setup into a proper PCB.

It covers why a fixed board makes the smoke test fast and repeatable, designing the schematic and layout in EasyEDA Pro (with help from a CoderDojo coach), what ended up on the board (40-pin GPIO header, LEDs grouped per GPIO test, I2C and SPI sensor connectors, and extra headers for a logic analyser), ordering at JLCPCB, and the first successful test run on a Raspberry Pi 5.

* [Pi4J website](https://www.pi4j.com/)
* [Pi4J Smoke Test documentation](https://www.pi4j.com/hardware-testing/hardware-testing/)
* [Blog post: From breadboard chaos to a real PCB](https://webtechie.be/post/2026-06-25-pi4j-smoketest-pcb/)
* [Pi4J GitHub Discussions](https://github.com/Pi4J/pi4j/discussions)
