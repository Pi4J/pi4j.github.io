---
title: Simple LED
weight: 201
tags: ["Simple LED", "LED"]
---

### Description

The [SimpleLed](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/SimpleLed.java) is a template class, that you can use in your own Java-project.

The template Class gives you the option to switch off, switch on or toggle the state of the LED.

### Layout

![Simple LED Layout](/assets/examples/components/components/Layout-SimpleLED.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/SimpleLedBreadboard.png" caption="Simple Led Breadboard" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the LED-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
System.out.println("Simple LED demo started ...");

// Create a new SimpleLED component
SimpleLed led = new SimpleLed(pi4j, PIN.D26);

// Turn on the LED to have a defined state
System.out.println("Turn on LED.");
led.on();
delay(Duration.ofSeconds(1));

// Make a flashing light by toggling the LED every second
for (int i = 0; i < 10; i++) {
    System.out.println("Current LED state is :" + led.toggle() +".");
    delay(Duration.ofSeconds(1));
}

// That's it so reset all
led.reset();
```

### Further project ideas

- Use an infrared LED to establish communication with an infrared receiver.
- Use several red LEDs to recreate the running lights of KITT, the car from Knight Rider.
