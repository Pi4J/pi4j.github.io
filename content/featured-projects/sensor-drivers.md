---
title: 'Sensor drivers'
weight: 80
tags: ["ADS1115", "BME280", "BMP180", "HTU21D", "PCF8591", "BH1750"]
---

In case you want to read the data from various I2C sensors connected to Raspberry Pi
the difficult part is usually writing a piece of code which talks to the I2C sensor.   

[rpi-drivers](https://github.com/jveverka/rpi-projects/tree/pi4j-v2/rpi-drivers)
is a Java library by **Juraj Veverka** implementing simple APIs and communication code for some
widely used I2C sensors. You can easily measure temperature, pressure and humidity,
get ambient light intensity or measure voltage in your java Raspberry Pi projects.

Supported sensors are: 

* ADS1115
* BME280
* BMP180
* HTU21D
* PCF8591
* BH1750

Simply include [rpi-drivers](https://search.maven.org/artifact/one.microproject.rpi/rpi-drivers)
dependency into your Java Gradle or Maven project, and you are good to go!

