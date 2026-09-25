---
title: Building with javac
weight: 161
tags: ["Javac"]
---

You can build a Pi4J project using only java and javac.

## Wiring

No wiring is needed for this minimal example as it only demonstrates how to create a minimal application which initializes
Pi4J.

## Java release

Any Java release over 21 is enough, check it with this command:

```shell
$ java -version
openjdk version "21.0.1" 2023-10-17 LTS
OpenJDK Runtime Environment Zulu21.30+15-CA (build 21.0.1+12-LTS)
OpenJDK 64-Bit Server VM Zulu21.30+15-CA (build 21.0.1+12-LTS, mixed mode, sharing)
```

## PI4J jar files

You will need to download the Pi4J distribution from the Maven repository:

[pi4j-distribution-2.1.1.zip](https://repo1.maven.org/maven2/com/pi4j/pi4j-distribution/2.1.1/pi4j-distribution-2.1.1.zip)

Expand the file:

`unzip pi4j-distribution-2.1.1.zip`

Add the lib directory to CLASSPATH by added this line to your .bashrc file:

`export CLASSPATH=$CLASSPATH:~/pi4j-2.1.1/lib/*`

## Minimal Java example file

Use your preferred editor to create this GettingStartedExample.java file:

```java
import com.pi4j.Pi4J;
import com.pi4j.io.gpio.digital.DigitalOutput;
import com.pi4j.platform.Platform;
import com.pi4j.platform.Platforms;
import com.pi4j.provider.Providers;
import com.pi4j.registry.Registry;
import com.pi4j.util.Console;

public class GettingStartedExample {

    public static void main(String[] args) throws Exception {

        final var console = new Console();

        console.title("<-- The Pi4J Project -->", "Getting Started Example");

        var pi4j = Pi4J.newAutoContext();

        Platforms platforms = pi4j.platforms();

        console.box("Pi4J PLATFORMS");
        platforms.describe().print(System.out);
        console.println();

        Platform platform = pi4j.platform();

        console.box("Pi4J DEFAULT PLATFORM");
        platform.describe().print(System.out);
        console.println();

        Providers providers = pi4j.providers();
        console.box("Pi4J PROVIDERS");
        providers.describe().print(System.out);
        console.println();

        Registry registry = pi4j.registry();

        DigitalOutput output = pi4j.dout().create(1, "my-digital-output-1");

        console.box("Pi4J REGISTRY");
        registry.describe().print(System.out);
        console.println();

        pi4j.shutdown();
    }
}
```

## Compile the example

`javac GettingStartedExample.java`

## Execute the example

`java GettingStartedExample`

If everything is OK the output must be something similar to this, depending on your configuration:

```shell
[main] INFO com.pi4j.util.Console - 

[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console -                   <-- The Pi4J Project -->                  
[main] INFO com.pi4j.util.Console -                    Getting Started Example                  
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.Pi4J - New auto context
[main] INFO com.pi4j.Pi4J - New context builder

[main] INFO com.pi4j.util.Console - --------------------
[main] INFO com.pi4j.util.Console - |  Pi4J PROVIDERS  |
[main] INFO com.pi4j.util.Console - --------------------
PROVIDERS: [5] "I/O Providers" <com.pi4j.provider.impl.DefaultProviders> 
??DIGITAL_INPUT: [1] <com.pi4j.io.gpio.digital.DigitalInputProvider> 
? ??PROVIDER: "FFM Digital Input (GPIO) Provider" {ffm-digital-input} <com.pi4j.plugin.ffm.providers.gpio.FFMDigitalInputProviderImpl> 
??PWM: [1] <com.pi4j.io.pwm.PwmProvider> 
? ??PROVIDER: "FFM PWM Provider" {ffm-pwm} <com.pi4j.plugin.ffm.providers.pwm.FFMPwmProviderImpl> 
??I2C: [1] <com.pi4j.io.i2c.I2CProvider> 
? ??PROVIDER: "FFM I2C Provider" {ffm-i2c} <com.pi4j.plugin.ffm.providers.i2c.FFMI2CProviderImpl> 
??SPI: [1] <com.pi4j.io.spi.SpiProvider> 
? ??PROVIDER: "FFM SPI Provider" {ffm-spi} <com.pi4j.plugin.ffm.providers.spi.FFMSpiProviderImpl> 
??DIGITAL_OUTPUT: [1] <com.pi4j.io.gpio.digital.DigitalOutputProvider> 
? ??PROVIDER: "FFM Digital Output (GPIO) Provider" {ffm-digital-output} <com.pi4j.plugin.ffm.providers.gpio.FFMDigitalOutputProviderImpl> 
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - -------------------
[main] INFO com.pi4j.util.Console - |  Pi4J REGISTRY  |
[main] INFO com.pi4j.util.Console - -------------------
REGISTRY: [1] "I/O Registered Instances" <com.pi4j.registry.impl.DefaultRegistry> 
??IO: "DOUT-1" {my-digital-output-1} <com.pi4j.plugin.ffm.providers.gpio.FFMDigitalOutput> {DOUT-1} 
[main] INFO com.pi4j.util.Console - 
```

---

*Thanks to Manuel de Vega Barreiro for this contribution.*