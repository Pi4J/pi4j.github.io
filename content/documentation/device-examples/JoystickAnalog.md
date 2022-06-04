---
title: Joystick Analog
weight: 208
tags: ["Joystick analog"]
---
### Description
The [analog Joystick](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
The template class is created for an analog joystick, for example KY-023, with two potentiometers one each for the X-axis and the Y-axis. Additionally a button can be attached to the class.

The basic functions of the template class are:
* return of a normalized value, optionally between 0 and 1 or between -1 and 1, of the x-axis and the y-axis
* creation of simple events at a value change of the x-axis or the y-axis, simple event handlers for button preaaed, button depressed, while button is pressed
* calibration of the center position of the joystick (center position 0.5 at a normalized value between 0 and 1, center position 0 at a normalized value between -1 and 1)

### Layout
![Joystick Layout](/assets/documentation/device-examples/Layout-JoystickAnalog.png)

### Code
A simple example on how to use the Joystick-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
System.out.println("Joystick test started ...");

ADS1115 ads1115 = new ADS1115(pi4j, 0x01, ADS1115.GAIN.GAIN_4_096V, ADS1115.ADDRESS.GND, 4);

//joystick with normalized axis from 0 to 1
JoystickAnalog joystick = new JoystickAnalog(pi4j, ads1115, 0, 1, 3.3, true, PIN.D26);

//joystick with normalized axis form -1 to 1
//JoystickAnalog joystick = new JoystickAnalog(pi4j, ads1115, 0, 1, 3.3, false, PIN.D26);

//register event handlers
joystick.xOnMove((value) -> {
    System.out.println("Current value of joystick x axis is: " + String.format("%.3f", value));
});
joystick.yOnMove((value) -> {
    System.out.println("Current value of joystick y axis is: " + String.format("%.3f", value));
});

joystick.pushOnDown(() -> logInfo("Pressing the Button"));
joystick.pushOnUp(() -> logInfo("Stopped pressing."));
joystick.pushWhilePressed(() -> logInfo("Button is still pressed."), 1000);

joystick.calibrateJoystick();

//start continious reading with single shot in this mode you can connect up to 4 devices to the analog module
joystick.start(0.05, 10);

//wait while handling events before exiting
System.out.println("Move the joystick to see it in action!");

delay(30_000);

//stop continious reading
joystick.stop();

//deregister all event handlers
joystick.deregisterAll();

System.out.println("Joystick test done");
```

### Further application
The class is implemented in the sample project [Theremin](https://github.com/DieterHolz/RaspPiTheremin).

### Further projetct ideas

- create your own PlayStation controller
- use the joystick to control the position of servo motors steplessly
