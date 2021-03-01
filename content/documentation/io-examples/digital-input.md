---
title: Digital Input (GPIO)
weight: 210
tags: ["Digital Input"]
---

V.2 provides a declarative style of configuration for I/O provisioning instead of the hard-coded approach offered in V1.

Examples of the various methods and approaches which can be used to provision the I/O needs [are available in the examples project](
https://github.com/Pi4J/pi4j-v2-examples/tree/master/src/main/java/com/pi4j/example/gpio/digital/input).

```
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