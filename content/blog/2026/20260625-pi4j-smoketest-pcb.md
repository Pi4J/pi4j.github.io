---
title: "Smoke test PCB for Pi4J"
date: 2026-06-25
tags: ["Hardware Testing"]
canonical: https://webtechie.be/post/2026-06-25-pi4j-smoketest-pcb/
---

2026-06-25 by Frank Delporte

## From breadboard chaos to a real PCB: designing the Pi4J smoke test board

Testing a Java I/O library properly means testing it on real hardware: no mocks, no stubs, just actual pins doing actual things. For Pi4J that means running the [smoke test](https://www.pi4j.com/hardware-testing/hardware-testing/), a setup with two BMP/BME280 sensors and a tangle of GPIO-to-GPIO jumper wires that has to be rebuilt by hand every session. That last part is what finally pushed us to design a proper PCB.

In a [new blog post on webtechie.be](https://webtechie.be/post/2026-06-25-pi4j-smoketest-pcb/), Frank Delporte tells the story of board number `0001`:

* **Why a board?** A breadboard setup is fine for a quick experiment, but it changes shape every time you rebuild it, which works against the whole point of a smoke test: a fast, repeatable answer to "does this still work?".
* **Designed with EasyEDA Pro**, with help from Jan, a coach at the Ieper CoderDojo, turning the smoke test wiring tables into a clean schematic using net labels, a fine-tuned layout, and a 3D preview before ordering.
* **What's on the board:** a 40-pin GPIO header, LEDs and SMD resistors grouped by the pin ranges of each GPIO test, I2C and SPI sensor connectors, mounting holes, and extra headers for hooking up a logic analyser.
* **Ordered at JLCPCB** (with a few confusing moments in the ordering software), and the first board passed all of the smoke tests cleanly, on a Raspberry Pi 5, with the LEDs blinking through each test group.

The EasyEDA design files are now available in the [Pi4J repository](https://github.com/Pi4J/pi4j/tree/develop/pi4j-test/pcb), and the board has been added to the [Pi4J hardware testing documentation](https://www.pi4j.com/hardware-testing/smoke-test-pcb/), so you can order it yourself or modify the design. It could even grow into an official Pi4J testing accessory. Got feedback or ideas for a future revision? Open a discussion on the [Pi4J GitHub](https://github.com/Pi4J/pi4j/discussions) or find us on [Slack](https://join.slack.com/t/pi4j/shared_invite/zt-1ttqt8wgj-E6t69qaLrNuCMPLiYnBCsg).

Read the full story, including the schematic, PCB views, and photos of the boards arriving: [From breadboard chaos to a real PCB: designing the Pi4J smoke test board](https://webtechie.be/post/2026-06-25-pi4j-smoketest-pcb/).
