---
title: Minimal example as FAT JAR
weight: 50
tags: ["Digital Input", "Digital Output", "FatJAR"]
---

{{% notice tip %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-example-fatjar](https://github.com/Pi4J/pi4j-example-fatjar)
{{% /notice %}}

The ["Minimal example application"](/getting-started/minimal-example-application/) uses one LED and button to demonstrate
the basic use of Pi4J. When building that project with Maven, all the required Java modules are copied to the 
`target/distribution` directory. But a lot of developers like to produce a single, executable JAR that contains
all dependencies, also known as a "FAT JAR".

The repository ["pi4j-example-fatjar" GitHub project](https://github.com/Pi4J/pi4j-example-fatjar) contains a Maven project 
with identical wiring, dependencies and build command to the "Minimal example application", but results in such a FAT JAR 
instead of separate Java modules.

## Maven Plugins

By using three build plugins the FAT JAR is created:

* [maven-compiler-plugin](https://maven.apache.org/plugins/maven-compiler-plugin/)
* [maven-jar-plugin](https://maven.apache.org/plugins/maven-jar-plugin/)
* [maven-shade-plugin](https://maven.apache.org/plugins/maven-shade-plugin/)

For the full description, take a look at the README.md in the sources and the page ["Build as a FAT JAR with Maven"](/documentation/building/fat-jar/).

## Building and Running

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
$ java -jar pi4j-example-fatjar.jar 

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
[main] INFO com.pi4j.runtime.impl.DefaultRuntime - Initializing Pi4J context/runtime...
[main] WARN com.pi4j.runtime.impl.DefaultRuntime - Replacing provider DIGITAL_OUTPUT RaspberryPi Digital Output (GPIO) Provider with priority 0 with provider GpioD Digital Output (GPIO) Provider with higher priority 150
[main] WARN com.pi4j.runtime.impl.DefaultRuntime - Replacing provider DIGITAL_INPUT RaspberryPi Digital Input (GPIO) Provider with priority 0 with provider GpioD Digital Input (GPIO) Provider with higher priority 150
[main] INFO com.pi4j.library.gpiod.internal.GpioDContext - Using chip gpiochip0 pinctrl-bcm2711
[main] INFO com.pi4j.platform.impl.DefaultRuntimePlatforms - adding platform to managed platform map [id=raspberrypi; name=RaspberryPi Platform; priority=5; class=com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform]
[main] INFO com.pi4j.runtime.impl.DefaultRuntime - Pi4J context/runtime successfully initialized.
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - |  Pi4J PLATFORMS  |
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - 
PLATFORMS: [1] "Pi4J Runtime Platforms" <com.pi4j.platform.impl.DefaultPlatforms> 
    PLATFORM: "RaspberryPi Platform" {raspberrypi} <com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform> {Pi4J Platform for the RaspberryPi series of products.} 
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
PROVIDERS: [6] "I/O Providers" <com.pi4j.provider.impl.DefaultProviders> 
    DIGITAL_INPUT: [1] <com.pi4j.io.gpio.digital.DigitalInputProvider> 
       PROVIDER: "GpioD Digital Input (GPIO) Provider" {gpiod-digital-input} <com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalInputProviderImpl> {com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalInputProviderImpl} 
    SERIAL: [1] <com.pi4j.io.serial.SerialProvider> 
       PROVIDER: "RaspberryPi Serial Provider" {raspberrypi-serial} <com.pi4j.plugin.raspberrypi.provider.serial.RpiSerialProviderImpl> {com.pi4j.plugin.raspberrypi.provider.serial.RpiSerialProviderImpl} 
    I2C: [1] <com.pi4j.io.i2c.I2CProvider> 
       PROVIDER: "RaspberryPi I2C Provider" {raspberrypi-i2c} <com.pi4j.plugin.raspberrypi.provider.i2c.RpiI2CProviderImpl> {com.pi4j.plugin.raspberrypi.provider.i2c.RpiI2CProviderImpl} 
    DIGITAL_OUTPUT: [1] <com.pi4j.io.gpio.digital.DigitalOutputProvider> 
       PROVIDER: "GpioD Digital Output (GPIO) Provider" {gpiod-digital-output} <com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalOutputProviderImpl> {com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalOutputProviderImpl} 
    SPI: [1] <com.pi4j.io.spi.SpiProvider> 
       PROVIDER: "RaspberryPi SPI Provider" {raspberrypi-spi} <com.pi4j.plugin.raspberrypi.provider.spi.RpiSpiProviderImpl> {com.pi4j.plugin.raspberrypi.provider.spi.RpiSpiProviderImpl} 
    ANALOG_OUTPUT: [0] <com.pi4j.io.gpio.analog.AnalogOutputProvider> 
    ANALOG_INPUT: [0] <com.pi4j.io.gpio.analog.AnalogInputProvider> 
    PWM: [1] <com.pi4j.io.pwm.PwmProvider> 
      PROVIDER: "RaspberryPi PWM Provider" {raspberrypi-pwm} <com.pi4j.plugin.raspberrypi.provider.pwm.RpiPwmProviderImpl> {com.pi4j.plugin.raspberrypi.provider.pwm.RpiPwmProviderImpl} 
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - -------------------
[main] INFO com.pi4j.util.Console - |  Pi4J REGISTRY  |
[main] INFO com.pi4j.util.Console - -------------------
[main] INFO com.pi4j.util.Console - 
REGISTRY: [2] "I/O Registered Instances" <com.pi4j.registry.impl.DefaultRegistry> 
    IO: "Press button" {button} <com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalInput> {DIN-24} 
    IO: "DOUT-22" {DOUT-22} <com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalOutput> {DOUT-22} 
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[Pi4J.RUNTIME-1] INFO com.pi4j.util.Console - Button was pressed for the 1th time
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[Pi4J.RUNTIME-1] INFO com.pi4j.util.Console - Button was pressed for the 2th time
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[Pi4J.RUNTIME-1] INFO com.pi4j.util.Console - Button was pressed for the 3th time
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[Pi4J.RUNTIME-1] INFO com.pi4j.util.Console - Button was pressed for the 4th time
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[Pi4J.RUNTIME-1] INFO com.pi4j.util.Console - Button was pressed for the 5th time
[main] INFO com.pi4j.runtime.impl.DefaultRuntime - Shutting down Pi4J context/runtime...
[main] INFO com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalInput - Shutdown input listener for button
[main] INFO com.pi4j.util.ExecutorPool - Shutting down executor pool Pi4J.RUNTIME
[main] INFO com.pi4j.runtime.impl.DefaultRuntime - Pi4J context/runtime successfully shutdown. Dispatching shutdown event.
```