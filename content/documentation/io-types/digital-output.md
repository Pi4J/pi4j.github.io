---
title: Digital Output (GPIO)
weight: 200
tags: ["Digital Output"]
aliases:
  - /documentation/io-examples/digital-output/
---

A digital output translates a false/true (or 0/1) to an output value of 0V or 3.3V. This
means you can control any type of device which works with max 3.3V to off or on. The most
basic example is a LED. Always check which is the correct input voltage for your device! 
For a LED you will need to put a resistor with the correct value between the GPIO and the LED,
you can find a lot of examples and calculators online, for example on
[circuitdigest.com/calculators/led-resistor-calculator](https://circuitdigest.com/calculators/led-resistor-calculator).

The following example shows the minimal code to configure the `BCM_LED` pin number 
as an output pin and change the state with different methods which are provided by the Pi4J library.
This implementation will operate with a Pi4j [provider](/documentation/providers/) that accesses the GPIO hardware.

```java
// Connect a LED to PIN 18 = BCM 24
int BCM_LED = 24;

// Initialize Pi4J with an auto context
// An auto context includes AUTO-DETECT BINDINGS enabled
// which will load all detected Pi4J extension libraries
// (Platforms and Providers) in the class path
var pi4j = Pi4J.newAutoContext();

// Create a digital output config and object
var ledConfig = DigitalOutput.newConfigBuilder(pi4j)
    .id("led")
    .name("LED Flasher")
    .bcm(BCM_LED)
    .shutdown(DigitalState.LOW)
    .initial(DigitalState.LOW);

var led = pi4j.create(ledConfig);

// Lets invoke some changes on the digital output
for (int i = 0; i < 10; i++) {
    if (led.equals(DigitalState.HIGH)) {
        led.low();
    } else {
        led.high();
    }
    Thread.sleep(500);
}

// Shutdown Pi4J
pi4j.shutdown();
``` 