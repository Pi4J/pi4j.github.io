---
title: 'Smoke Test PCB'
date: 2026-06-25
weight: 20
tags: ["Hardware Testing", "PCB"]
---

Running the [Pi4J Smoke Test](https://www.pi4j.com/hardware-testing/hardware-testing/) on a breadboard works, but it is fragile: every time the setup is rebuilt, a wire ends up in the wrong column, a jumper is not fully seated, or a sensor falls over. To make the smoke test fast and repeatable, and easy to hand to a contributor, we designed a dedicated PCB that turns the whole wiring table into a single board.

The full story of how the board was designed is described in [this blog post](https://www.pi4j.com/blog/2026/20260625-pi4j-smoketest-pcb/) and the accompanying [video](https://www.pi4j.com/video/20260625-smoketest-pcb/).

![Pi4J smoke test PCB, board number 0001](https://raw.githubusercontent.com/Pi4J/pi4j/develop/pi4j-test/pcb/smoketest-pcb.jpg)

## What is on the board

The board reproduces every connection from the smoke test wiring table:

- A **40-pin GPIO header** across the middle, with the pin numbers printed on both rows, that connects directly to the Raspberry Pi GPIO header.
- A row of **SMD resistors and LEDs** above the header that light up while the GPIO-to-GPIO tests run, grouped by the pin ranges they cover (12-16, 13-15, 16-22, 32-36, 36-37, and 38). Each group maps to one of the test cases in the wiring table.
- An **I2C connector** on the left for the first BMP/BME280 sensor.
- An **SPI connector** on the right for the second BMP/BME280 sensor.
- **Mounting holes** in all four corners so the board can be fixed in place.
- Two extra **20-pin headers** so a measuring instrument such as a [logic analyser](/hardware-testing/ikalogic-analyser/) can easily be connected when something does not behave as expected.

The board was designed in [EasyEDA Pro](https://pro.easyeda.com/editor) and manufactured by [JLCPCB](https://jlcpcb.com/), which integrates directly with EasyEDA.

## Order your own board

The design files are available in the [`pi4j-test/pcb`](https://github.com/Pi4J/pi4j/tree/develop/pi4j-test/pcb) directory of the Pi4J repository, so you can order the board yourself or modify the design.

The directory contains the following files:

- [**EasyEDA Pro project**](https://github.com/Pi4J/pi4j/blob/develop/pi4j-test/pcb/ProPrj_Pi4J%20Smoke%20Test_2026-06-25.epro) (`.epro`) — the complete source design. Import it into [EasyEDA Pro](https://pro.easyeda.com/editor) to open the schematic and PCB layout, modify the board, and order it directly through the built-in JLCPCB integration (or export Gerber files to order at another manufacturer).
- [**BOM**](https://github.com/Pi4J/pi4j/blob/develop/pi4j-test/pcb/BOM_Board1_Schematic1_2026-06-25.xlsx) (`.xlsx`) — the Bill of Materials listing every component, its quantity, and the matching LCSC part number, used when having the boards assembled (PCBA).
- [**Pick & Place**](https://github.com/Pi4J/pi4j/blob/develop/pi4j-test/pcb/PickAndPlace_PCB1_2026-06-25.xlsx) (`.xlsx`) — the component positions and rotations used by the assembly machine.
- [**Schematic**](https://github.com/Pi4J/pi4j/blob/develop/pi4j-test/pcb/SCH_Schematic1_2026-06-25.pdf) (`.pdf`) — a human-readable overview of all connections.
- [**3D model**](https://github.com/Pi4J/pi4j/blob/develop/pi4j-test/pcb/3D_PCB1_2026-06-25.step) (`.step`) — a 3D export of the board, for example to design an enclosure.

{{% notice tip %}}
The minimum order quantity at JLCPCB is five boards. The 40-pin GPIO header is a through-hole part that is easy to solder yourself if it's not available, so it does not need to be included in the assembly.
{{% /notice %}}

## Feedback

If you have feedback on the design, or ideas for what should go on a future revision, open a discussion on the [Pi4J GitHub](https://github.com/Pi4J/pi4j/discussions) or find us on [Slack](https://join.slack.com/t/pi4j/shared_invite/zt-1ttqt8wgj-E6t69qaLrNuCMPLiYnBCsg).
