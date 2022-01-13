---
title: Minimal example as FAT JAR
weight: 50
tags: ["Digital Input", "Digital Output", "FatJAR"]
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-example-fatjar](https://github.com/Pi4J/pi4j-example-fatjar)
{{% /notice %}}

The ["Minimal example application"](/getting-started/minimal-example-application/) uses one LED and button to demonstrate
the basic use of Pi4J V2. When building that project with Maven, all the required Java modules are copied to the 
`target/distribution` directory. But a lot of developers like to produce a single, executable JAR that contains
all dependencies, also known as a "FAT JAR".

The repository ["pi4j-example-fatjar" GitHub project](https://github.com/Pi4J/pi4j-example-fatjar) contains a Maven project 
with identical wiring, dependencies and build command to the "Minimal example application", but results in such a FAT JAR 
instead of separate Java modules.

## Maven plugins

By using three build plugins the FAT JAR is created:

* [maven-compiler-plugin](https://maven.apache.org/plugins/maven-compiler-plugin/)
* [maven-jar-plugin](https://maven.apache.org/plugins/maven-jar-plugin/)
* [maven-shade-plugin](https://maven.apache.org/plugins/maven-shade-plugin/)

For the full description, take a look at the README.md in the sources and the page ["Build as a FAT JAR with Maven"](/documentation/building/fat-jar/).

## Building and running

Build with:

```
mvn clean package
```

Once the build is complete and was successful, you can find the compiled FAT JAR `pi4j-example-fatjar.jar` in the
`target` directory. You can build directly on your Raspberry Pi or if you are developing on a different computer, copy the file
to your Raspberry Pi with (in this example the Pi has IP 192.168.0.252):

```
scp target/pi4j-example-fatjar.jar pi@192.168.0.252://home/pi
```

On the Raspberry Pi open a terminal, or via SSH from your PC, execute this command:

```
$ sudo java -jar pi4j-example-fatjar.jar 

[main] INFO com.pi4j.util.Console - 

[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console -                   <-- The Pi4J Project -->                  
[main] INFO com.pi4j.util.Console -                    Minimal Example project                  
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.Pi4J - New auto context
[main] INFO com.pi4j.Pi4J - New context builder
[main] INFO com.pi4j.platform.impl.DefaultRuntimePlatforms - adding platform to managed platform map [id=raspberrypi; name=RaspberryPi Platform; priority=5; class=com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform]
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - |  Pi4J PLATFORMS  |
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - 
PLATFORMS: [1] "Pi4J Runtime Platforms" <com.pi4j.platform.impl.DefaultPlatforms> 
└─PLATFORM: "RaspberryPi Platform" {raspberrypi} <com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform> {Pi4J Platform for the RaspberryPi series of products.} 
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - ---------------------------
[main] INFO com.pi4j.util.Console - |  Pi4J DEFAULT PLATFORM  |
[main] INFO com.pi4j.util.Console - ---------------------------
[main] INFO com.pi4j.util.Console - 
PLATFORM: "RaspberryPi Platform" {raspberrypi} <com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform> {Pi4J Platform for the RaspberryPi series of products.} 
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - |  Pi4J PROVIDERS  |
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - 
PROVIDERS: [12] "I/O Providers" <com.pi4j.provider.impl.DefaultProviders> 
├─SPI: [2] <com.pi4j.io.spi.SpiProvider> 
│ ├─PROVIDER: "PiGpio SPI Provider" {pigpio-spi} <com.pi4j.plugin.pigpio.provider.spi.PiGpioSpiProviderImpl> {com.pi4j.plugin.pigpio.provider.spi.PiGpioSpiProviderImpl} 
│ └─PROVIDER: "RaspberryPi SPI Provider" {raspberrypi-spi} <com.pi4j.plugin.raspberrypi.provider.spi.RpiSpiProviderImpl> {com.pi4j.plugin.raspberrypi.provider.spi.RpiSpiProviderImpl} 
├─ANALOG_INPUT: [0] <com.pi4j.io.gpio.analog.AnalogInputProvider> 
├─SERIAL: [2] <com.pi4j.io.serial.SerialProvider> 
│ ├─PROVIDER: "PiGpio Serial Provider" {pigpio-serial} <com.pi4j.plugin.pigpio.provider.serial.PiGpioSerialProviderImpl> {com.pi4j.plugin.pigpio.provider.serial.PiGpioSerialProviderImpl} 
│ └─PROVIDER: "RaspberryPi Serial Provider" {raspberrypi-serial} <com.pi4j.plugin.raspberrypi.provider.serial.RpiSerialProviderImpl> {com.pi4j.plugin.raspberrypi.provider.serial.RpiSerialProviderImpl} 
├─DIGITAL_INPUT: [2] <com.pi4j.io.gpio.digital.DigitalInputProvider> 
│ ├─PROVIDER: "RaspberryPi Digital Input (GPIO) Provider" {raspberrypi-digital-input} <com.pi4j.plugin.raspberrypi.provider.gpio.digital.RpiDigitalInputProviderImpl> {com.pi4j.plugin.raspberrypi.provider.gpio.digital.RpiDigitalInputProviderImpl} 
│ └─PROVIDER: "PiGpio Digital Input (GPIO) Provider" {pigpio-digital-input} <com.pi4j.plugin.pigpio.provider.gpio.digital.PiGpioDigitalInputProviderImpl> {com.pi4j.plugin.pigpio.provider.gpio.digital.PiGpioDigitalInputProviderImpl} 
├─I2C: [2] <com.pi4j.io.i2c.I2CProvider> 
│ ├─PROVIDER: "RaspberryPi I2C Provider" {raspberrypi-i2c} <com.pi4j.plugin.raspberrypi.provider.i2c.RpiI2CProviderImpl> {com.pi4j.plugin.raspberrypi.provider.i2c.RpiI2CProviderImpl} 
│ └─PROVIDER: "PiGpio I2C Provider" {pigpio-i2c} <com.pi4j.plugin.pigpio.provider.i2c.PiGpioI2CProviderImpl> {com.pi4j.plugin.pigpio.provider.i2c.PiGpioI2CProviderImpl} 
├─ANALOG_OUTPUT: [0] <com.pi4j.io.gpio.analog.AnalogOutputProvider> 
├─DIGITAL_OUTPUT: [2] <com.pi4j.io.gpio.digital.DigitalOutputProvider> 
│ ├─PROVIDER: "RaspberryPi Digital Output (GPIO) Provider" {raspberrypi-digital-output} <com.pi4j.plugin.raspberrypi.provider.gpio.digital.RpiDigitalOutputProviderImpl> {com.pi4j.plugin.raspberrypi.provider.gpio.digital.RpiDigitalOutputProviderImpl} 
│ └─PROVIDER: "PiGpio Digital Output (GPIO) Provider" {pigpio-digital-output} <com.pi4j.plugin.pigpio.provider.gpio.digital.PiGpioDigitalOutputProviderImpl> {com.pi4j.plugin.pigpio.provider.gpio.digital.PiGpioDigitalOutputProviderImpl} 
└─PWM: [2] <com.pi4j.io.pwm.PwmProvider> 
  ├─PROVIDER: "RaspberryPi PWM Provider" {raspberrypi-pwm} <com.pi4j.plugin.raspberrypi.provider.pwm.RpiPwmProviderImpl> {com.pi4j.plugin.raspberrypi.provider.pwm.RpiPwmProviderImpl} 
  └─PROVIDER: "PiGpio PWM Provider" {pigpio-pwm} <com.pi4j.plugin.pigpio.provider.pwm.PiGpioPwmProviderImpl> {com.pi4j.plugin.pigpio.provider.pwm.PiGpioPwmProviderImpl} 
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - -------------------
[main] INFO com.pi4j.util.Console - |  Pi4J REGISTRY  |
[main] INFO com.pi4j.util.Console - -------------------
[main] INFO com.pi4j.util.Console - 
REGISTRY: [2] "I/O Registered Instances" <com.pi4j.registry.impl.DefaultRegistry> 
├─IO: "LED Flasher" {led} <com.pi4j.plugin.pigpio.provider.gpio.digital.PiGpioDigitalOutput> {DOUT-22} 
└─IO: "Press button" {button} <com.pi4j.plugin.pigpio.provider.gpio.digital.PiGpioDigitalInput> {DIN-24} 
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
...
[main] INFO com.pi4j.util.Console - LED high
[Thread-1] INFO com.pi4j.util.Console - Button was pressed for the 1th time
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[Thread-3] INFO com.pi4j.util.Console - Button was pressed for the 2th time
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
...
```