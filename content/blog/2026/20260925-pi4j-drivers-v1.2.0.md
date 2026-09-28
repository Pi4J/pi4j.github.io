---
title: "Pi4J Drivers V1.2.0"
date: 2026-09-28
tags: ["Drivers"]
description: "Pi4J Drivers V1.2.0 adds new ePaper display drivers with partial-update support, new DAC/ADC drivers, motor/robotics drivers, and LoRa support."
---

2026-09-25 by Frank Delporte

## Pi4J Drivers V1.2.0: ePaper, DAC/ADC, and More

[Pi4J Drivers](/drivers/) has reached **V1.2.0**, adding a wide range of new drivers and improvements to the growing catalog of pre-built, tested Java drivers for common electronic components.

### What's new

- **New ePaper display drivers**: a generic SSD1780 driver, a driver for the Waveshare 2.7 inch ePaper display hat v2, and a driver for the Waveshare 13.3 inch b/w 960x680 ePaper display.
- **Partial display updates**: support for partial screen updates on the SSD1680 and Waveshare 2.7 inch v2 drivers, along with fixes to reverse destination calculations and clarified display placement limitations.
- **Character/graphics display improvements**: a new `GraphicsTextAnimator` for scrolling text, display mirroring support, and cursor management pulled up into the `CharacterDisplay` interface.
- **New DAC/ADC drivers**: a `DigitalAnalogConverter` interface with reworked MCP49xx drivers, new MCP4725, MCP4921/MCP4922, and MCP4728 DAC drivers, new TI ADS111x and NAU7802 ADC drivers, and `Mcp300xDriver` split into 10-bit and 12-bit subclasses.
- **New motor/robotics drivers**: an LN298 motor driver, a ULN2003 servo driver, and a driver for the PiBorg UltraBorg.
- **LR11xx LoRa support**: a driver for the Semtech LR11xx LoRa transceivers.

### Why it matters

Every new driver in this release means one less datasheet to read and one less low-level I2C/SPI implementation to write before you can start working with your hardware. The ePaper and partial-update support in particular makes it much easier to build low-power status displays and dashboards, while the new DAC/ADC drivers extend Pi4J Drivers further into analog sensing and control.

### What's next

After this release, the drivers repository was pushed to Java 25 and Pi4J V5.0.0-SNAPSHOT so it can be aligned with the next version of the Pi4J Core and FFM plugin library.

### Thank you

Thanks to everyone who contributed to this release: Igor Souza, Matti Tahvonen, Robert von Burg, Stefan Haustein, Stephen More, and Tom Aarts.

Read the full [Drivers Release Notes](/drivers/drivers-release-notes/) for all the details, or check the [changes on GitHub](https://github.com/Pi4J/pi4j-drivers/compare/v1.1.0...v1.2.0).
