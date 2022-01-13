---
title: Minimal example application
weight: 50
tags: ["Digital Input", "Digital Output", "Maven", "Gradle"]
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-example-minimal](https://github.com/Pi4J/pi4j-example-minimal)
{{% /notice %}}

In the ["pi4j-example-minimal" GitHub project](https://github.com/Pi4J/pi4j-example-minimal) you can 
find a project which contains the minimal code to control a digital input and output with Pi4J. The project is further 
described on this page. The application will toggle an LED on/off and each time you press the button, the toggling 
speed increases. When you have pushed the button 5 times, the application stops.

{{< vimeo 525570174 >}}

## Wiring

This minimal example application uses this wiring:

![](/assets/getting-started/minimal/led-button_bb.png)

## Building the application

The main build tool used by the Pi4J project is Maven, but for this example we provided both the Maven and Gradle approach,
so you can select the tool you prefer.

### Maven

This project can be built with Apache Maven 3.6 (or later) and Java 11 OpenJDK (or later). These prerequisites must be 
installed prior to building this project as described on the previous pages. The following command can be used to 
download all project dependencies and compile the Java module. You can build this project directly on a Raspberry Pi with Java 11+.

```
mvn clean package
```

### Gradle

You can also use the Gradle Build Tool from these same sources. Use version 6.6 (or later) and Java 11 OpenJDK (or later). 
The Gradle wrapper is used as described on [docs.gradle.org](https://docs.gradle.org/current/userguide/gradle_wrapper.html).
The Gradle configuration file [build.gradle-file](https://github.com/Pi4J/pi4j-example-minimal/blob/master/build.gradle) 
is included in the sources.

On Linux:

```
./gradlew build
```

On Windows:

```
gradlew.bat build
```

## Dependency in pom.xml

For the Maven approach, a pom.xml file defines all the dependencies, and the build process.

In this project we will be using slf4 for logging, pi4j-core and the pi4j-plugins for the Raspberry Pi and PiGPIO. To 
make the versions easy to update, we add those numbers as properties. 

```xml
<properties>
    <!-- DEPENDENCIES VERSIONS -->
    <slf4j.version>1.7.32</slf4j.version>
    <pi4j.version>2.0</pi4j.version>
</properties>
``` 
  
These are the dependencies we need:

```xml
<dependencies>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>${slf4j.version}</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-simple</artifactId>
        <version>${slf4j.version}</version>
    </dependency>

    <!-- include Pi4J Core -->
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-core</artifactId>
        <version>${pi4j.version}</version>
    </dependency>

    <!-- include Pi4J Plugins (Platforms and I/O Providers) -->
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-plugin-raspberrypi</artifactId>
        <version>${pi4j.version}</version>
    </dependency>
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-plugin-pigpio</artifactId>
        <version>${pi4j.version}</version>
    </dependency>
</dependencies>
``` 

## Pi4J code blocks which are used

### Initialization

Before you can use Pi4J you must initialize a new runtime context.

The `Pi4J` static class includes a few helper context creators for the most common use cases.  The `newAutoContext()`
method will automatically load all available Pi4J extensions found in the application's classpath which may include 
`Platforms` and `I/O Providers`.
        
```java
var pi4j = Pi4J.newAutoContext();
```

### Output Pi4J Context information

The library contains helper functions to output info about the available and used platforms and providers. To keep the 
example code clean, these are part of the `PrintInfo.java` class. For example to print the loaded platforms:

```java
Platforms platforms = pi4j.platforms();

console.box("Pi4J PLATFORMS");
console.println();
platforms.describe().print(System.out);
console.println();
```

### Handle the button presses

To handle digital input events we first need a configuration for it. With that configuration, Pi4J can create the object 
for us and the state changes can be handled.

```java
private static int pressCount = 0;
private static final int PIN_BUTTON = 24; // PIN 18 = BCM 24

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
```

### Toggle a LED

For the LED we use a similar approach with a configuration. The created led-object can be used to toggle its state.

```java
private static final int PIN_LED = 22; // PIN 15 = BCM 22

var ledConfig = DigitalOutput.newConfigBuilder(pi4j)
      .id("led")
      .name("LED Flasher")
      .address(PIN_LED)
      .shutdown(DigitalState.LOW)
      .initial(DigitalState.LOW)
      .provider("pigpio-digital-output");
      
var led = pi4j.create(ledConfig);

while (pressCount < 5) {
      if (led.equals(DigitalState.HIGH)) {
           led.low();
      } else {
           led.high();
      }
      Thread.sleep(500 / (pressCount + 1));
}
```

### Closing the application

Before the application quits, we need to call the `shutdown()` function on the Pi4J static helper class. This will ensure 
that all I/O instances are properly shutdown, released by the system and shutdown in the appropriate manner. Termination 
will also ensure that any background threads/processes are cleanly shutdown and any used memory is returned to the system.

```java
pi4j.shutdown();
``` 

## Steps to run this application on your Raspberry Pi

* Attach a LED and button as shown in the image above
* Use a recent Raspbian OS image which has Java 11. To check if you have the correct Java version in the terminal:

```shell
$ java -version
openjdk version "11.0.6" 2020-01-14
OpenJDK Runtime Environment (build 11.0.6+10-post-Raspbian-1deb10u1)
OpenJDK Server VM (build 11.0.6+10-post-Raspbian-1deb10u1, mixed mode)
``` 

* Download the project from GitHub and build it:

```shell
$ git clone https://github.com/Pi4J/pi4j-example-minimal.git
$ cd pi4j-example-minimal/
$ mvn clean package
``` 

* Change to the distribution directory where you can find the generated package and required Java-modules. Start it with 
the provided `run.sh` script:

```shell
$ cd target/distribution
$ ls -l
total 644
-rw-r--r-- 1 pi pi 364456 Jun 19 10:04 pi4j-core-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi   7243 Jun 19 10:04 pi4j-example-minimal-0.0.1.jar
-rw-r--r-- 1 pi pi 142461 Jun 19 10:04 pi4j-library-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  37302 Jun 19 10:04 pi4j-plugin-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  26917 Jun 19 10:04 pi4j-plugin-raspberrypi-2.0-SNAPSHOT.jar
-rwxr-xr-x 1 pi pi    101 Jun 19 10:04 run.sh
-rw-r--r-- 1 pi pi  52173 Jun 19 10:04 slf4j-api-2.0.0-alpha0.jar
-rw-r--r-- 1 pi pi  15372 Jun 19 10:04 slf4j-simple-2.0.0-alpha0.jar
$ sudo ./run.sh
``` 

* The output will first show you some info about the platforms and providers. Then the LED starts blinking and shows how 
many times you pushed the button:

```shell
LED high
LED low
LED high
Button was pressed for the 1th time
LED low
LED high
Button was pressed for the 2th time
LED low
LED high
LED low
LED high
Button was pressed for the 3th time
LED low
LED high
LED low
LED high
Button was pressed for the 4th time
LED low
LED high
LED low
LED high
Button was pressed for the 5th time
``` 

* If you get an error like shown below, you probably didn't start the application with `sudo`, which is (at the moment) 
required for the PiGpio native library that handles the interfacing with the GPIOs.

```shell
WARN com.pi4j.library.pigpio.impl.PiGpioNativeImpl 
    - PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failedWARN com.pi4j.library.pigpio.impl.PiGpioNativeImpl 
    - PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
```