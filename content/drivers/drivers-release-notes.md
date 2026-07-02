---
title: 'Drivers Release Notes'
weight: 20
---

All releases of the Pi4J Drivers library are listed on [github.com/Pi4J/pi4j-drivers/releases](https://github.com/Pi4J/pi4j-drivers/releases).

The Pi4J Drivers library is available on [Maven Central](https://central.sonatype.com/artifact/com.pi4j/pi4j-drivers).

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
