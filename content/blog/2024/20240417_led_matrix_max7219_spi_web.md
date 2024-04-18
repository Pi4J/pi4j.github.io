---
title: "LED Matrix with SPI MAX7219"
date: 2024-04-17
tags: ["Pi4J", "SPI", "MAX7219", "BME280"]
---

2024-04-18, by Frank Delporte

Roberto Marquez shared a project with us that uses Java to interface with a MAX7219 SPI device to control an LED matrix. It's inspired by the blog [Raspberry Pi and SPI 8×8 LED matrix example with Java and Pi4j](https://www.hackerspacetech.com/raspberry-pi-and-spi-8x8-led-matrix-example-with-java-and-pi4j/), but differs in that it is Web-enabled via Spring Boot. This project is the starting point to create a weather station in combination with the BMP280, see [BME280 Sensor (temp, humidity, pressure) via Pi4J, I2C, and JBang](https://pi4j.com/examples/jbang/bme280_temperature_humidity_pressure/).

{{< gallery >}}
{{< figure link="/assets/blogs/max7219/wiring-diagram.png" caption="Wiring diagram" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/max7219/number-8-definition.png" caption="Definition of the number 8 for the LED matrix" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

While working on his project, Roberto contributed extra LED character definitions for the [Pi4JLedMatrixSpi.java single-file application in the Pi4J V2 JBang project](https://github.com/Pi4J/pi4j-jbang/blob/main/Pi4JLedMatrixSpi.java).

## Demos

<img src="/assets/blogs/max7219/screen-recording.gif" />

<img src="/assets/blogs/max7219/matrix-demo.gif" />

## Wiring

This demo project uses:

* Raspberry Pi 2 Model B V1.1 
* 8x8 LED Matrix with Max7219 SPI

Connections:

* DIN -> blue   -> MOSI -> header 19
* CS -> purple -> CE0  -> header 24
* CLK -> white  -> SCLK -> header 23
* VCC -> 5V ->  header 2
* GND -> ground -> header 9

## Project and Code

Check the [README in the project sources of Roberto](https://github.com/onebeartoe/electronics/tree/master/single-board-computers/raspberry-pi/spi/max7219/led-matrix/8x8/web-app) for more info.