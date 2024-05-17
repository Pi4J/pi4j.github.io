---
title: "Bosch sensor gas measurement"
date: 2024-04-25
tags: ["BME280", "BMP280", "BME680", "BME688"]
---

2024-05-17, by Frank Delporte

Bosch has several sensors which are extremely small to measure temperature, humidity, pressure, and gas. We also have several example implementations documented on the Pi4J website:

* [BME280 Sensor (temp, humidity, pressure) via Pi4J, I2C, and JBang](/examples/jbang/bme280_temperature_humidity_pressure/).
* [BMP280 Sensor](/examples/communityimplementation/bmp280/), example implementation by Thomas Aarts.
* [LED Matrix with SPI MAX7219](/blog/2024/20240417_led_matrix_max7219_spi_web/), work-in-progress for a weather station.
* [Sensor drivers](/featured-projects/sensor-drivers/), project by Juraj Veverka.

You can find easy-to-use boards with such a sensor, for instance, on:

* [Adafruit](https://www.adafruit.com/product/2652)
* [SparkFun](https://learn.sparkfun.com/tutorials/sparkfun-bme280-breakout-hookup-guide/all)

## Important Information Regarding Gas Measurements

On the [Pi4J GitHub Discussion page, there is an interesting discussion going on about the BME688 gas sensor](https://github.com/Pi4J/pi4j-v2/discussions/353) that I want to share here... [**crogialli**](https://github.com/crogialli) shared the following info:

_I've been using BME680 in my application for a year, and I am also implementing BME 688.
It is entirely possible to read Temp, Pressure, Humidity and gas resistances from plain Java code (I do it, and I can submit my code for that, albeit I have an abstraction layer between the BME68X management and Pi4J so that the code could be not immediately usable). Readings for temp, pressure and humidity from BME68X are astonishingly accurate and quick._

_However, I want you to know that it is not possible to get sensible air-quality (gas) estimations in that way. You can get a gas sensor resistance reading, but it is entirely meaningless and random, as a matter of fact. It cannot be reconnected to any air quality measure without the Bosh Sensortec Libraries (see below)._

_Moreover, I've been reading a BME680 gas sensor "manually" every 5 seconds by setting arbitrary heating patterns for a couple of years now. I'm pretty sure I have damaged the BME 680 MEMS gas sensor since current resistance readings are now very low (1..3K), whilst at the beginning, they used to be relatively higher (15K ...150K). The sensor has always been in the same protected ambient (a boiler room with some natural ventilation hosting a diesel-fueled burner)._

_To get a correct gas estimation and preserve the sensor's life, the only way I know is to integrate BSEC 2.4.0.0 libraries from Bosch, which implement a few adaptive algorithms for sampling the gas estimates with specific (AI-Calibrated) sensor heating patterns and at specific instants, thus providing reliable indexes and safeguarding the MEMS device._

_Integrating BSEC libraries poses a few challenges:_

1. _The library, written in C, is Bosch proprietary_
1. _The source is not available; BSEC 2.4.0.0 is provided as a C binary library, statically linked_
1. _It is unclear at the moment if they provide a 64bit binary for Raspberry Pi4 (I want to run on Rasbian 64)_
1. _A Python wrapper exists, but not a Java one._

_I'm looking into developing a Java (or Groovy) wrapper for integrating BSEC 2.4.0.0 into my app. Should I be unable to wrap it in Java, I will likely implement a call to external C or Python code (disgusting but likely functional, provided that a solution to run on 64-bit Raspbian exists)._

_BME68X sensors give exceptional results for their price. I advise avoiding messing with air quality if you don't need it; if you do, you shall find a way to integrate BSEC libraries._