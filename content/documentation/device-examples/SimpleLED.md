---
title: Simple LED
weight: 201
tags: ["Simple LED"]
---
### Description
The simpleLED is a template class, that you can use in your own Java-project.
You can take any LED you want to. Like for example this one: [LED](https://www.berrybase.de/bauelemente/aktive-bauelemente/leds/led-sortimente/5mm-led-set-70-st-252-ck)
The Template Class gives you the option to switch off, switch on or toggle the state of the LED.

### Layout
![Simple LED Layout](/assets/documentation/Devices/Layout-SimpleLED.png)

### Code
A simple example on how to use the LED-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
// Create a new SimpleLED component
SimpleLED led = new SimpleLED(pi4j, 17);

// Turn on the LED to have a defined state
led.setStateOn();
sleep(1000);

// Make a flashing light by toggling the LED every second
for (int i = 0; i < 10; i++) {
    System.out.println(led.toggleState());
    sleep(1000);
}

// That's all so turn off the relay and quit
led.setStateOff();
System.out.println("off");
sleep(2000);
```

### Further application / project ideas
- Use an infrared LED to establish communication with an infrared receiver.
- Use several red LEDs to recreate the running lights of KITT, the car from Knight Rider.