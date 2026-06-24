---
title: "Smoke test PCB for Pi4J"
date: 2026-02-27
tags: ["Commonhaus"]
canonical: https://webtechie.be/post/2026-02-27-pi4j-commonhaus/
---

2026-06-25 by Frank Delporte

## From breadboard chaos to a real PCB: designing the Pi4J smoke test board

Testing a Java I/O library properly means testing it on real hardware. No mocks, no stubs, just actual pins doing actual things. For Pi4J, that means running the smoke test: a setup with two BMP/BME280 sensors, some GPIO-to-GPIO jumper connections, and a bunch of patience while you untangle the wires for the third time this week.

That last part is what finally pushed us to design a proper PCB. This is the story of board number `0001`.

### What is the Pi4J smoke test

The [Pi4J smoke test](https://www.pi4j.com/hardware-testing/hardware-testing/) is a test project that verifies the Pi4J library works correctly on real Raspberry Pi hardware. It covers the most important communication protocols:

- I2C: using a BMP280 or BME280 sensor for air pressure and temperature
- SPI: a second BMP/BME280 sensor over SPI
- GPIO: several pin-to-pin connections to test PWM output, digital output, digital input, and debounce behaviour

The wiring involves quite a few connections. Two sensors, a T-cobbler breakout board plugged into a breadboard, and a collection of colour-coded jumper wires connecting GPIO pins to each other. It works fine, but "works fine" and "reliable test setup" are not always the same thing.

### The problem with the breadboard

Every time someone of the Pi4J sets up the smoke test on a breadboard, something is slightly different. A wire in the wrong column. A jumper that looks seated but is not. A sensor that falls over when you move the board.

This is fine for a quick experiment. It is not great when you want to hand the setup to a contributor, or use it consistently across different hardware revisions of the Raspberry Pi. The goal of a smoke test is to give you a fast, repeatable answer to the question "does this still work". A breadboard that changes shape every session works against that goal.

So we wanted to have a "fixed solution" already for a long time...

TODO add first idea picture from Robert.

### Designing the board with EasyEDA

I used [EasyEDA Pro](https://pro.easyeda.com/editor) for the design. It is a browser-based PCB design tool with a built-in schematic editor, a large component library, and direct integration with JLCPCB for ordering. The learning curve is manageable, especially for a board this straightforward.

I did not do this alone. Jan, a coach from our my CoderDojo club in Ieper, helped me with the PCB layout and design decisions. That turned out to be the right call. There are details in PCB design, like how to connect the sensors, adding the LEDs, component placement, and clearance rules, where experience matters more than enthusiasm. Jan has a lot of hardware-design-experience and was happy to share it.

The starting point was the wiring tables from the smoke test documentation. Every connection in those tables needed to end up as a trace or a connector on the board. That gave us a clear scope and made the design process straightforward.

### What is on the board

The finished board has a few distinct sections.

The 40-pin GPIO header runs across the middle, with pin numbers printed on both rows. This connects directly to the Raspberry Pi GPIO header. Above the header, a row of SMD resistors and LEDs helps to see of the GPIO-to-GPIO tests are running. They are grouped by the pin ranges they cover: 12-16, 13-15, 16-22, 32-36, 36-37, and 38. Each group maps to one of the test cases in the smoke test wiring table.

On the left side of the board there is an I2C connector for the first BMP/BME280 sensor. On the right side there is an SPI connector for the second sensor. 

The board also has mounting holes in all four corners, which means you can actually fix it to something instead of letting it slide around on a desk. And there are two additional 20-pin headers so it's easy to connect a measuring instrument if something seems to be not working as expected.

Board number 0001 is the first one off the production run. The QR code in the top corner is the PCB manufacturer's tracking code.

### Ordering and first results

The board was manufactured by JLCPCB, which integrates directly with EasyEDA. You export the Gerber files from the editor and upload them to the order form. The turnaround time is fast and the cost for a small batch is low enough that iterating on the design is not a big deal.

The first board passed the smoke test cleanly. The connections are solid, the connectors are in the right place, and nothing falls over when you pick it up. That is exactly what you want from a test board.

### What is next

The plan is to open source the EasyEDA design files and add the board to the Pi4J hardware testing documentation. If there is interest from contributors, it could become an official Pi4J testing accessory, something you can order yourself or build from the files.

If you have feedback on the design, or ideas for what else should go on a future revision, open a discussion on the [Pi4J GitHub](https://github.com/Pi4J/pi4j/discussions) or find us on [Slack](https://join.slack.com/t/pi4j/shared_invite/zt-1ttqt8wgj-E6t69qaLrNuCMPLiYnBCsg).

And yes, CoderDojo coaches know more about PCB design than you might expect.