---
title: Joystick Analog
weight: 210
tags: ["Joystick", "Analog", "ADS1115", "ADC"]
---

### Description

The [JoystickAnalog](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/JoystickAnalog.java) is a template class, that you can use in your own Java-project.
The template class is created for an analog joystick, for example the KY-023, which consists of two potentiometers, one for the X-axis and one for the Y-axis. But any joystick with two potentiometers will meet the requirements.

The basic functions of the template class are:
* return of a normalized value, optionally between 0 and 1 or between -1 and 1, of the X-axis and the Y-axis
* creation of simple events at a value change of the X-axis or the Y-axis, simple event handlers for button pressed, button depressed, while button is pressed
* calibration of the center position of the joystick (center position 0.5 at a normalized value between 0 and 1, center position 0 at a normalized value between -1 and 1)

### Layout

![Joystick Layout](/assets/examples/components/components/Layout-JoystickAnalog.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickAnalogBreadboard.png" caption="Joystick Analog Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickAnalog.png" caption="Joystick Analog" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/ADS1115-Front.png" caption="ADS1115-Front" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/ADS1115-Back.png" caption="ADS1115-Back" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the JoystickAnalog-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
// an analog joystick needs an ADC
Ads1115 ads1115 = new Ads1115(pi4j);

//joystick with normalized axis from -1 to 1
JoystickAnalog joystick = new JoystickAnalog(ads1115, Ads1115.Channel.A0, Ads1115.Channel.A1, PIN.D26, true);

//register all event handlers you need
joystick.onMove((xPos, yPos) -> System.out.printf("Current position of joystick is: %.2f, %.2f%n", xPos, yPos),
                ()           -> System.out.println("Joystick in home position"));

 joystick.onDown      (() -> System.out.println("Pressing the button"));
 joystick.onUp        (() -> System.out.println("Stopped pressing."));
 joystick.whilePressed(() -> System.out.println("Button is still pressed."), Duration.ofMillis(500));

 //start continuous reading after all ADC channels are configured
 ads1115.startContinuousReading(0.1);

 System.out.println("Move the joystick to see it in action!");

 //wait while handling events before exiting
 delay(Duration.ofSeconds(30));

 //cleanup
 joystick.reset();
```

### Further project ideas

- create your own PlayStation controller
- use the joystick to control the position of servo motors steplessly
