---
title: Running Pi4J with JBang
weight: 165
tags: ["JBang"]
---

{{% notice note %}}
JBang project website: [https://www.jbang.dev/](https://www.jbang.dev/)
{{% /notice %}}

## What is JBang?

As described on their website:

*JBang lets Students, Educators and Professional Developers create, edit and run self-contained source-only Java programs with unprecedented ease.*

*Want to learn, explore or use Java instantly without setup ?
Do you like Java but use python, groovy, kotlin or similar languages for scripts, experimentation and exploration ?
Ever wanted to just be able to run Java from anywhere without any or very minimal setup ? Ever tried out Java 11+ support 
for running .java files directly in your shell but felt it was a bit too cumbersome ?*

*JBang lets you do all this!*

## Video 

This video shows you all the steps decribed further on this page

{{< youtube 33CWAN1dQvA >}}

## Prepare a Raspberry Pi

For this manual you can use the following approach:

* Grab an SD card (minimum 8Gb)
* Use the Raspberry Pi Imager tool to write the "Raspberry Pi OS (32-bit)" to this SD card
* Push the SD card into your Raspberry Pi board 
* Power up and wait until the OS has booted (it will probably restart once to resize the partition on the SD card to the maximum available size)
* Open a terminal and confirm Java is not available yet (except if you selected the "Raspberry Pi OS Full (32-bit)" version)

```shell
$ java -version
bash: java: command not found
```

## Installing JBang

As described on [jbang.dev/download](https://www.jbang.dev/download/) installing JBang is enough to get started, 
even if you don't have Java installed already, as JBang will also take care of this.

```shell
$ curl -Ls https://sh.jbang.dev | bash -s - app setup
$ java -version
openjdk version "11.0.14" 2022-01-18
OpenJDK Runtime Environment Temurin-11.0.14+9 (build 11.0.14+9)
OpenJDK Server VM Temurin-11.0.14+9 (build 11.0.14+9, mixed mode)
```

## Minimal JBang example

A minimal JBang Java-file looks like the following code block, take note of the special first line that tricks the system
to run this as a script while still being valid Java-code.

```java
///usr/bin/env jbang "$0" "$@" ; exit $? 

class HelloWorld {
    public static void main(String[] args) {
        if(args.length==0) {
            System.out.println("Hello World!");
        } else {
            System.out.println("Hello " + args[0]);
        }
    }
}
```

By saving this file as `HelloWorld.java` it can be started with:

```shell
$ jbang HelloWorld.java
Hello World!
```

## JBang Pi4J example

If your project needs dependencies - which is the case for a Pi4J project - you can [define them in the java-file with the
following gradle-style locators format](https://www.jbang.dev/documentation/guide/latest/dependencies.html), for example:
`//DEPS com.pi4j:pi4j-core:2.1.1`.

The following example is based on the ["Minimal example application"](/getting-started/minimal-example-application/), and uses
the same wiring with a button and LED. By using JBang we can run this project with a single file without the need of a full
Maven or Gradle project, or compiling the Java code.

Create a new file `JBangPi4JExample.java` with the following content:

```java
///usr/bin/env jbang "$0" "$@" ; exit $?
//DEPS org.slf4j:slf4j-api:1.7.35
//DEPS org.slf4j:slf4j-simple:1.7.35
//DEPS com.pi4j:pi4j-core:2.1.1
//DEPS com.pi4j:pi4j-plugin-raspberrypi:2.1.1
//DEPS com.pi4j:pi4j-plugin-pigpio:2.1.1

import com.pi4j.Pi4J;
import com.pi4j.io.gpio.digital.DigitalInput;
import com.pi4j.io.gpio.digital.DigitalOutput;
import com.pi4j.io.gpio.digital.DigitalState;
import com.pi4j.io.gpio.digital.PullResistance;
import com.pi4j.util.Console;

class JBangPi4JExample {

    private static final int PIN_BUTTON = 24; // PIN 18 = BCM 24
    private static final int PIN_LED = 22; // PIN 15 = BCM 22

    private static int pressCount = 0;
    
    public static void main(String[] args) throws Exception {

        final var console = new Console();
        
        var pi4j = Pi4J.newAutoContext();
        
        var ledConfig = DigitalOutput.newConfigBuilder(pi4j)
                .id("led")
                .name("LED Flasher")
                .address(PIN_LED)
                .shutdown(DigitalState.LOW)
                .initial(DigitalState.LOW)
                .provider("pigpio-digital-output");
        var led = pi4j.create(ledConfig);

        var buttonConfig = DigitalInput.newConfigBuilder(pi4j)
                .id("button")
                .name("Press button")
                .address(PIN_BUTTON)
                .pull(PullResistance.PULL_DOWN)
                .debounce(3000L)
                .provider("pigpio-digital-input");
        var button = pi4j.create(buttonConfig);
        button.addListener(e -> {
            if (e.state() == DigitalState.LOW) {
                pressCount++;
                console.println("Button was pressed for the " + pressCount + "th time");
            }
        });

        while (pressCount < 5) {
            if (led.equals(DigitalState.HIGH)) {
                console.println("LED low");
                led.low();
            } else {
                console.println("LED high");
                led.high();
            }
            Thread.sleep(500 / (pressCount + 1));
        }
        
        pi4j.shutdown();
    }
}
```

Without the need of any further configuration, installation, dependency download, or compiling, we should now be able to run this code with:

```shell
$ jbang JBangPi4JExample.java

[jbang] Building jar...

[main] INFO com.pi4j.Pi4J - New auto context
[main] INFO com.pi4j.Pi4J - New context builder
[main] INFO com.pi4j.platform.impl.DefaultRuntimePlatforms - adding platform to managed platform map [id=raspberrypi; name=RaspberryPi Platform; priority=5; class=com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform]
[main] WARN com.pi4j.library.pigpio.impl.PiGpioNativeImpl - PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
```

Auch, an error...?! But this is a known one! At this moment, PiGpio - the underlying native library which interacts with the GPIOs -
needs to be called as `sudo`. This is not ideal, and we are investigating how we can rework this. But with some additional 
steps this can be fixed easily! 

First we need to find out where JBang is installed for our current user with `which jbang`. This full path can be used to start
JBang from that location, instead of the shortcut `jbang` that was automatically created by JBang for the `pi` user (in this case). 
As Java was installed by JBang for the `pi` user, it needs to do this again for the `sudo` user, but also this is handled 
automatically again by JBang.

```shell
$ which jbang
/home/pi/.jbang/bin/jbang

$ sudo /home/pi/.jbang/bin/jbang JBangPi4JExample.java
Downloading JDK 11. Be patient, this can take several minutes...

[main] INFO com.pi4j.Pi4J - New auto context
[main] INFO com.pi4j.Pi4J - New context builder
[main] INFO com.pi4j.platform.impl.DefaultRuntimePlatforms - adding platform to managed platform map [id=raspberrypi; name=RaspberryPi Platform; priority=5; class=com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform]
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED low
[Thread-0] INFO com.pi4j.util.Console - Button was pressed for the 1th time
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
[Thread-2] INFO com.pi4j.util.Console - Button was pressed for the 2th time
[main] INFO com.pi4j.util.Console - LED low
[main] INFO com.pi4j.util.Console - LED high
...
[main] INFO com.pi4j.util.Console - LED high
[main] INFO com.pi4j.util.Console - LED low
[Thread-8] INFO com.pi4j.util.Console - Button was pressed for the 5th time
```

Yep, we have a working example, with dependencies, without the need to compile anything!

And both commands can even be combined to make things even more easy, allowing you to start the application simply with:

```shell
$ sudo `which jbang` JBangPi4JExample.java
```

## Conclusion

JBang is a great way to run single-file Java-files, and helps you to quickly get started with Pi4J on the Raspberry Pi, 
and can be the ideal getting-started method to experiment with electronics and Java.

Thanks to [Max Rydahl Andersen](https://twitter.com/maxandersen) and the many contributors for creating JBang and to
propose the [solution how `sudo` can be combined with JBang](https://github.com/jbangdev/jbang/discussions/1229).