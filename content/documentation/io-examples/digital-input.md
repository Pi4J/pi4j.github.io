---
title: Digital Input (GPIO)
weight: 210
tags: ["Digital Input"]
---

Similar to a digital output pin, a digital input translates an input value of 0V or 3.3V to the value false/true. This
means any type of device which can toggle between 3.3V and 0V, can generate an input value to the Raspberry Pi. Here the 
most basic example is a toggle button. If you use other components, always check which is the voltage provided by the device.
Or if you use a power pin from the Raspberry Pi itself, to use a 3.3V pin and not a 5V pin.

V.2 provides a declarative style of configuration for I/O provisioning instead of the hard-coded approach offered in V.1.

Examples of the various methods and approaches which can be used to provision the I/O needs [are available in the examples project](
https://github.com/Pi4J/pi4j-v2-examples/tree/master/src/main/java/com/pi4j/example/gpio/digital/input).

```java
Properties properties = new Properties();
properties.put("id", "my_digital_input");
properties.put("address", DIGITAL_INPUT_PIN);
properties.put("pull", "UP");
properties.put("name", "MY-DIGITAL-INPUT");

var config = DigitalInput.newConfigBuilder(pi4j)
        .load(properties)
        .build();

var input = pi4j.din().create(config);
```  
s
Once an input has been initialized, a listener can be attached to execute code on state changes of the input.

```java
input.addListener(e -> {
    if (e.state() == DigitalState.HIGH) {
        console.println("Button is pressed");
    }
});
```