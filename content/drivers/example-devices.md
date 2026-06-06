---
title: 'Example Implementations'
weight: 20
tags: ["1602A", "ADS1256", "BME280", "BMP280", "DAC8552", "DHT22", "IS31FL3731", "MCP23008", "MCP23017", "MCP3008", "MCP4725", "MPL3115A2", "NeoPixel", "SN74HC595", "SSD1306", "TCA9548", "VL53L0X"]
---

The [pi4j-examples](https://github.com/Pi4J/pi4j-examples) repository contains complete example applications that use the Pi4J Drivers library. Each example shows how to wire up a specific component and use the corresponding driver in a Java application.

## Getting the examples

Clone the repository to your Raspberry Pi or development machine:

```shell
git clone https://github.com/Pi4J/pi4j-examples
```

Each subdirectory contains a self-contained Maven project for a specific device.

## Available examples

| Device | Description | Interface |
|:---|:---|:---|
| 1602A LCD HD44780U | 16x2 character LCD, direct GPIO control | GPIO |
| 1602A LCD via PCF8574A | 16x2 character LCD over I2C expander | I2C |
| 1602A LCD via MCP23017 | 16x2 character LCD over 16-bit I2C expander | I2C |
| ADS1256 | 24-bit analog-to-digital converter | SPI |
| AT24C512 | Serial EEPROM read/write | I2C |
| BME280 | Temperature, humidity, and pressure sensor | I2C |
| BMP280 | Temperature and pressure sensor | I2C |
| DAC8552 | 16-bit digital-to-analog converter | SPI |
| DHT22 | Temperature and humidity sensor | GPIO |
| IS31FL3731 | LED matrix controller | I2C |
| MCP23008 | 8-bit GPIO expander — drive and read chip GPIOs | I2C |
| MCP23008 + MCP23017 | Pin monitoring example | I2C |
| MCP23017 | 16-bit GPIO expander — drive and read chip GPIOs | I2C |
| MCP3008 | 10-bit analog-to-digital converter | SPI |
| MCP4725 | 12-bit digital-to-analog converter | I2C |
| MPL3115A2 | Altitude, pressure, and temperature sensor | I2C |
| NeoPixel LED strip | WS2812B addressable RGB LEDs | SPI |
| Rotary Encoder (KY-040 / 5880) | Rotary encoder with integrated push button | GPIO |
| SN74HC595 | 8-bit shift register | SPI |
| SSD1306 | 128x64 OLED display | I2C |
| TCA9548 | 1-to-8 I2C multiplexer switch | I2C |
| VL53L0X | Time-of-flight distance sensor | I2C |

## Contributing

Found a device not yet covered? Contributions are welcome. Open an issue or pull request in [github.com/Pi4J/pi4j-examples](https://github.com/Pi4J/pi4j-examples) to share your implementation with the community.

