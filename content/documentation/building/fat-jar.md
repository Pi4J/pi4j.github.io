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
com.pi4j.plugin.ffm.FFMPlugin
```

When running this application we can indeed see the loaded provider plugins in the logs:

```
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - |  Pi4J PROVIDERS  |
[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - 
PROVIDERS: [5] "I/O Providers" <com.pi4j.provider.impl.DefaultProviders> 
├─SPI: [1] <com.pi4j.io.spi.SpiProvider> 
│ └─PROVIDER: "FFM SPI Provider" {ffm-spi} <com.pi4j.plugin.ffm.providers.spi.FFMSpiProviderImpl> 
├─DIGITAL_INPUT: [1] <com.pi4j.io.gpio.digital.DigitalInputProvider> 
│ └─PROVIDER: "FFM Digital Input (GPIO) Provider" {ffm-digital-input} <com.pi4j.plugin.ffm.providers.gpio.FFMDigitalInputProviderImpl> 
├─I2C: [1] <com.pi4j.io.i2c.I2CProvider> 
│ └─PROVIDER: "FFM I2C Provider" {ffm-i2c} <com.pi4j.plugin.ffm.providers.i2c.FFMI2CProviderImpl> 
├─DIGITAL_OUTPUT: [1] <com.pi4j.io.gpio.digital.DigitalOutputProvider> 
│ └─PROVIDER: "FFM Digital Output (GPIO) Provider" {ffm-digital-output} <com.pi4j.plugin.ffm.providers.gpio.FFMDigitalOutputProviderImpl> 
└─PWM: [1] <com.pi4j.io.pwm.PwmProvider> 
  └─PROVIDER: "FFM PWM Provider" {ffm-pwm} <com.pi4j.plugin.ffm.providers.pwm.FFMPwmProviderImpl> 
[main] INFO com.pi4j.util.Console - 
```

{{% notice tip %}}
Add the `pi4j-plugin-mock` dependency (and use `autoDetectMockPlugins()`, see [Mock Provider](/documentation/providers/mock/)) if you also want to see the Mock providers listed here.
{{% /notice %}}