---
title: BME280 (temp, humidity, pressure) via Pi4J, SPI, and JBang
date: 2023-07-15

---

2023-07-19, by Frank Delporte and Tom Aarts

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-jbang](https://github.com/Pi4J/pi4j-jbang)
{{% /notice %}}

## Intro

This is an example project to demonstrate how to read the temperature, humidity and pressure from a BME280 sensor, installed on an Adafruit board that can be controlled via I2C and SPI. Such a sensor itself, is a very tiny device, that can be integrated in phones and many other types of devices. 

Typically when you want to integrate such a device in a project, you'll need to dive into the [Data Sheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf) to find out how it needs to be controlled. If you want to better understand the code from this example, you can check the Data Sheet as the register read-outs and calculations are based on the example code you can find in that document.

// TODO add pictures sensor

## Wiring

Make the following connections between the BME280 and a Raspberry Pi:

* Vin to 3.3V</li>
* GND to GND</li>
* SDI to MOSI (BCM10, pin 19)
* SDO to MISO (BCM9, pin 21)
* SCK to SCLK (BCM11, pin 23)
* CS to BCM21 (pin 40)

In the wiring diagram, another brand of board ([Sparkfun](https://www.sparkfun.com/products/13676)) is used, which has the I2C and SPI connections on different sides, but to align it with the pictures, the same connections are used as are available on the Adafruit board.

{{< gallery >}}
{{< figure link="/assets/blogs/2023/bme280_wiring_spi_overview.jpg" caption="BME280 SPI wiring" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/2023/bme280_wiring_spi.jpg" caption="BME280 SPI wiring" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/2023/bme280_wiring_spi_rpi.jpg" caption="BME280 SPI wiring" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/2023/bme280_wiring_i2c_breadboard.png" caption="BME280 SPI wiring" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Application

Because we are using JBang for this demo, all code is included in a single file.

First we need to start with an extra line to instruct JBang to handle it as a Java application, and download the dependencies.

```java
///usr/bin/env jbang "$0" "$@" ; exit $?

//DEPS org.slf4j:slf4j-api:1.7.35
//DEPS org.slf4j:slf4j-simple:1.7.35
//DEPS com.pi4j:pi4j-core:2.3.0
//DEPS com.pi4j:pi4j-plugin-raspberrypi:2.3.0
//DEPS com.pi4j:pi4j-plugin-linuxfs:2.3.0
//DEPS com.pi4j:pi4j-plugin-pigpio:2.3.0
```

Then we can define the imports as we would do in any Java file:

```java
import com.pi4j.Pi4J;
import com.pi4j.io.gpio.digital.DigitalOutput;
import com.pi4j.io.gpio.digital.DigitalState;
import com.pi4j.io.spi.*;
import com.pi4j.util.Console;
import java.text.DecimalFormat;
```

The main method initializes the sensor, and loops 10 times to the process of resetting the sensor, reading the values, and pauzing.

```java

```

The reset and value readout is inspired by the Adafruit CircuitPython library and is [fully available in the sources on GitHub](https://github.com/Pi4J/pi4j-jbang/Pi4JTempHumPress.java). It's a combination of setting and reading registers, with different calculations. For example, for the temperature:

```java

```

### Running the Application

Because JBang can download the dependencies and compile the code, we just need the Java-file to execute it:

```shell
$ sudo `which jbang` Pi4JTempHumPressSpi.java


[jbang] Resolving dependencies...
[jbang]    org.slf4j:slf4j-api:1.7.35
[jbang]    org.slf4j:slf4j-simple:1.7.35
[jbang]    com.pi4j:pi4j-core:2.3.0
[jbang]    com.pi4j:pi4j-plugin-raspberrypi:2.3.0
[jbang]    com.pi4j:pi4j-plugin-pigpio:2.3.0
[jbang]    com.pi4j:pi4j-plugin-linuxfs:2.3.0
[jbang]    com.pi4j:pi4j-plugin-pigpio:2.3.0
[jbang] Dependencies resolved
[jbang] Building jar...
[main] INFO com.pi4j.Pi4J - New auto context
[main] INFO com.pi4j.Pi4J - New context builder
[main] INFO com.pi4j.platform.impl.DefaultRuntimePlatforms - adding platform to managed platform map [id=raspberrypi; name=RaspberryPi Platform; priority=5; class=com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform]
[main] INFO com.pi4j.util.Console - Initializing the sensor via SPI
[main] INFO com.pi4j.util.Console - **************************************
[main] INFO com.pi4j.util.Console - Reading values, loop 1
[main] INFO com.pi4j.util.Console - Measure temperature: 24.533°C
[main] INFO com.pi4j.util.Console - Pressure: 100606.095 Pa
[main] INFO com.pi4j.util.Console - Pressure: 1.006 bar
[main] INFO com.pi4j.util.Console - Pressure: 0.993 atm
[main] INFO com.pi4j.util.Console - Humidity: 0.0%
[main] INFO com.pi4j.util.Console - **************************************
[main] INFO com.pi4j.util.Console - Reading values, loop 2
...
[main] INFO com.pi4j.util.Console - **************************************
[main] INFO com.pi4j.util.Console - Finished
```

## Conclusion

Once again, JBang proves to be the perfect companion to experiment with Pi4J and an electronics component! 

## Read More 

The following sources have been used for this example:

* [Pi4J_V2-TemperatureSensor example code by Tom Aarts](https://github.com/Pi4J/pi4j-example-devices/blob/master/src/main/java/com/pi4j/devices/bmp280/README.md)
* [Bosch BMP280 Data Sheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bmp280-ds001.pdf)
* [Bosch BME280 Data Sheet](https://www.bosch-sensortec.com/media/boschsensortec/downloads/datasheets/bst-bme280-ds002.pdf)
* [Product page: "Adafruit BME280 I2C or SPI Temperature Humidity Pressure Sensor - STEMMA QT"](https://www.adafruit.com/product/2652)
* [Tutorial with Arduino code: "Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout"](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/pinouts)
* [Adafruit_CircuitPython_BME280 library source code](https://github.com/adafruit/Adafruit_CircuitPython_BME280/blob/main/adafruit_bme280/basic.py#L248)
