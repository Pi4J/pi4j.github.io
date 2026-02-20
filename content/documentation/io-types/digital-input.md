---
title: Digital Input (GPIO)
weight: 210
tags: ["Digital Input"]
aliases:
  - /documentation/io-examples/digital-input/
---

Similar to a digital output pin, a digital input translates an input value of 0V or 3.3V to the value false/true. This means any type of device which can toggle between 3.3V and 0V, can generate an input value to the Raspberry Pi. The most basic example is a toggle button. If you use other components, always check the voltage provided by the device. Or if you use a power pin from the Raspberry Pi itself, use a 3.3V pin and not a 5V pin.

V2+ provides a declarative style of configuration for I/O provisioning instead of the hard-coded approach offered in V1.

The following example shows the minimal code to configure the `BCM_BUTTON`  
as an input pin and monitor the pin state with by adding a Listener. The code uses methods which are 
provided by the Pi4J library. This implementation will operate with a Pi4j [provider](/documentation/providers/) that accesses the GPIO hardware.

```java
// Connect a button to PIN 15 = BCM 22
int BCM_BUTTON = 22;

var inputConfig = DigitalInput.newConfigBuilder(pi4j)
    .id("button")
    .name("Press button")
    .bcm(BCM_BUTTON)
    .pull(PullResistance.PULL_DOWN)
    .debounce(3_000L);

var input = pi4j.create(inputConfig);
```  

Once an input has been initialized, a listener can be attached to execute code on state changes of the input.

```java
input.addListener(e -> {
    if (e.state() == DigitalState.LOW){
        console.println("Button is pressed");
    }
});
```