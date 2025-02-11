---
title: Build as a FAT JAR with Maven
weight: 162
tags: ["FatJAR"]
---

{{% notice tip %}}
EXAMPLE PROJECT: [https://github.com/Pi4J/pi4j-example-fatjar](https://github.com/Pi4J/pi4j-example-fatjar)
{{% /notice %}}

## About FAT JARs

With Pi4J V1 you can create a so-called FAT JAR, which packages all the dependencies into one jar-file. That way it is
very easy to build your project on one computer and distribute your application as a single file to one or more clients.

Because of the modular approach and how Pi4J V2+ loads it dependencies at runtime, this approach can be achieved by using
the maven-shade-plugin.

## Example FAT JAR project

Check the example project (link on top of this page) for the full README, pom.xml and sources.

### Maven plugins

Three plugins are used in pom.xml to create the FAT JAR:

```xml
<build>
    <finalName>pi4j-example-fatjar</finalName>

    <plugins>
        <!--
        https://maven.apache.org/plugins/maven-compiler-plugin/
        The Compiler Plugin is used to compile the sources of your project.
        -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>${maven-compiler-plugin.version}</version>
            <configuration>
                <release>${java.version}</release>
                <showDeprecation>true</showDeprecation>
                <showWarnings>true</showWarnings>
                <verbose>false</verbose>
            </configuration>
        </plugin>

        <!--
        https://maven.apache.org/plugins/maven-jar-plugin/
        This plugin provides the capability to build (executable) jars and is used here to set the mainClass
        which will start the application.
        -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-jar-plugin</artifactId>
            <version>${maven-jar-plugin.version}</version>
            <configuration>
                <archive>
                    <manifest>
                        <mainClass>${main.class}</mainClass>
                    </manifest>
                </archive>
            </configuration>
        </plugin>

        <!--
        https://maven.apache.org/plugins/maven-shade-plugin/
        This plugin provides the capability to package the artifact in an uber-jar, including its dependencies and
        to shade - i.e. rename - the packages of some of the dependencies. The transformer will combine the files
        in the META-INF.services directories of multiple Pi4J plugins with the same package name into one file.
        -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>${maven-shade-plugin.version}</version>
            <configuration>
                <transformers>
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
                </transformers>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>shade</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

By using `maven-shade-plugin` the correct `META-INF.services` files are generated.

As a jar-file is actually a zip-file, we can easily check the contents of the FAT JAR after it has been created with
`mvn package`:

* directories
  * com
  * lib
  * META-INF
  * org
* files
  * LICENSE.txt
  * NOTICE.txt
  * README.md

## Loading of the Pi4J modules

Pi4J V2+ uses ServiceLoader to detect which modules are available to communicate with the GPIOs. This allows to very 
dynamically extend the possibilities of the framework.

Code extract from [pi4j-core/src/.../runtime/impl/DefaultRuntime.java](https://github.com/Pi4J/pi4j/blob/develop/pi4j-core/src/main/java/com/pi4j/runtime/impl/DefaultRuntime.java#L224):

```java
// detect available Pi4J Plugins by scanning the classpath looking for plugin instances
var plugins = ServiceLoader.load(Plugin.class);
```

Thanks to the `maven-shade-plugin`, each Pi4J plugin that is part of the project, is included in 
`META-INF/services/com.pi4j.extension.Plugin`:

```
com.pi4j.plugin.raspberrypi.RaspberryPiPlugin
com.pi4j.plugin.pigpio.PiGpioPlugin
```

When running this application we can indeed see the loaded platform and provider plugins in the logs:

```
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
```