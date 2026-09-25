---
title: 'Drivers Release Notes'
weight: 20
---

All releases of the Pi4J Drivers library are listed on [github.com/Pi4J/pi4j-drivers/releases](https://github.com/Pi4J/pi4j-drivers/releases).

The Pi4J Drivers library is available on [Maven Central](https://central.sonatype.com/artifact/com.pi4j/pi4j-drivers).

### 2026-09-25 - V1.2.0

- **New ePaper display drivers**: Added a generic SSD1780 driver, a driver for the Waveshare 2.7 inch ePaper display hat v2, and a driver for the Waveshare 13.3 inch b/w 960x680 ePaper display.
- **Partial display updates**: Added support for partial screen updates to the SSD1680 and Waveshare 2.7 inch v2 drivers, fixed reverse destination calculations for devices whose screen doesn't match the full buffer, and clarified display placement limitations.
- **Character/graphics display improvements**: Added `GraphicsTextAnimator` for scrolling text (with cleanup and daemon-thread wiring into SenseHat), added display mirroring support, and pulled cursor management up into the `CharacterDisplay` interface.
- **New DAC/ADC drivers**: Added a `DigitalAnalogConverter` interface and reworked the MCP49xx drivers around it, added the MCP4725, MCP4921/MCP4922, and MCP4728 DAC drivers, added TI ADS111x and NAU7802 ADC drivers, and split `Mcp300xDriver` into 10-bit and 12-bit subclasses.
- **ADC sensor units**: Added units for treating A/D converters as sensors.
- **New motor/robotics drivers**: Added an LN298 motor driver (with PWM fixes and convenience improvements), a ULN2003 servo driver, and a driver for the PiBorg UltraBorg.
- **LR11xx LoRa support**: Added a driver for the Semtech LR11xx LoRa transceivers.
- **SCD4x autodetection**: Added autodetection support to the SCD4x driver.
- **General cleanup**: Disabled hardware-dependent tests so the build doesn't fail off-device, added a JFrame-based utility for developing on standard hardware before moving to specialized hardware, fixed an `attachDriver` issue, and updated README/contributing documentation.

Thank you to:

- Frank Delporte ([@FDelporte](https://github.com/FDelporte))
- Igor Souza ([@igfasouza](https://github.com/igfasouza))
- Matti Tahvonen ([@mstahv](https://github.com/mstahv))
- Robert von Burg ([@eitch](https://github.com/eitch))
- Stefan Haustein [@stefanhaustein](https://github.com/stefanhaustein)
- Stephen More [@mores](https://github.com/mores
- Tom Aarts ([@taartspi](https://github.com/taartspi))
- Copilot Autofix powered by AI
- GitHub

Detailed list of all changes: https://github.com/Pi4J/pi4j-drivers/compare/v1.1.0...v1.2.0

### 2026-07-02 - V1.1.0

- **SenseHat convenience methods**:  Added helper methods for humidity, pressure, temperature, and sensor data retrieval, plus display manipulation, rotation support, and improved color handling. Sensor methods were renamed for clarity (e.g. `readMagnetometer` → `readMagneticField`).
- **MCP23017 support**:  New driver added for the MCP23017 IO expander, including a constructor taking a single I2C device parameter.
- **MCP23008 fixes**:  Added missing configuration calls.
- **IO Expander revamp**:  Consolidated the abstract classes into one, unified the driver architecture, and fixed initial state management for the MCP230xx family.
- **Convenience config methods**:  Added methods to address individual pins or sets of pins, with consistent singular/plural naming conventions.
- **PCF8574 fixes**:  Fixed the PCF8574 driver, corrected constant declarations (hex instead of binary), and ensured input is polled when no interrupt pin is connected.
- **General cleanup**:  Removed outdated test cases, brought comments and code in sync, and added Commonhaus documentation.

Thank you to [@stefanhaustein](https://github.com/stefanhaustein), [@igfasouza](https://github.com/igfasouza), [@taartspi](https://github.com/taartspi), and [@FDelporte](https://github.com/FDelporte)!

Detailed list of all changes: https://github.com/Pi4J/pi4j-drivers/compare/v1.0.0...v1.1.0

### 2026-06-06 - V1.0.0

This is the first release of the Pi4J Drivers library. It brings community-maintained device drivers back to the Pi4J ecosystem as a standalone library, compatible with **Pi4J V4+**.

The library is the result of years of community work, much of it grown from the [pi4j-examples](https://github.com/Pi4J/pi4j-examples) repository.

Detailed list of all changes: [github.com/Pi4J/pi4j-drivers/releases/tag/1.0.0](https://github.com/Pi4J/pi4j-drivers/releases/tag/1.0.0)
