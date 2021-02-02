---
title: Digital Output (GPIO)
weight: 200
---

```
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