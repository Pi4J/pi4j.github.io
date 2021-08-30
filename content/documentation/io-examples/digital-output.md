---
title: Digital Output (GPIO)
weight: 200
tags: ["Digital Output"]
---

A digital output translates a false/true (or 0/1) to an output value of 0V or 3.3V. This
means you can control any type of device which works with max 3.3V to off or on. The most
basic example is a LED. Always check which is the correct input voltage for your device! 
For a LED you will need to put a resistor with the correct value between the GPIO and the LED,
you can find a lot of examples and calculators online, for example on
[circuitdigest.com/calculators/led-resistor-calculator](https://circuitdigest.com/calculators/led-resistor-calculator).

The following example shows the minimal code to configure the `DIGITAL_OUTPUT_PIN` pin number 
as an output pin and change the state with different methods which are provided by the Pi4J library.

```java
// Initialize Pi4J with an auto context
// An auto context includes AUTO-DETECT BINDINGS enabled
// which will load all detected Pi4J extension libraries
// (Platforms and Providers) in the class path
var pi4j = Pi4J.newAutoContext();

// create a digital output instance using the default digital output provider
var output = pi4j.dout().create(DIGITAL_OUTPUT_PIN);
output.config().shutdownState(DigitalState.HIGH);

// setup a digital output listener to listen for any state changes on the digital output
output.addListener(System.out::println);

// lets invoke some changes on the digital output
output.state(DigitalState.HIGH)
          .state(DigitalState.LOW)
          .state(DigitalState.HIGH)
          .state(DigitalState.LOW);

// lets toggle the digital output state a few times
output.toggle()
          .toggle()
          .toggle();

// another friendly method of setting output state
output.high()
          .low();

// lets read the digital output state
System.out.print("CURRENT DIGITAL OUTPUT [" + output + "] STATE IS [");
System.out.println(output.state() + "]");

// pulse to HIGH state for 3 seconds
System.out.println("PULSING OUTPUT STATE TO HIGH FOR 3 SECONDS");
output.pulse(3, TimeUnit.SECONDS, DigitalState.HIGH);
System.out.println("PULSING OUTPUT STATE COMPLETE");

// shutdown Pi4J
pi4j.shutdown();
``` 