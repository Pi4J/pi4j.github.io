---
title: Joystick
weight: 210
tags: ["Joystick"]
---
### Description
The [Joystick](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog) (src/main/java/com/pi4j/catalog) is a template class, that you can use in your own Java-project.
The template is created for a digital joystick with 4 directions (up, right, down, left) and as an option additionally with a push button in direction down.
A suitable hardware component is the arcade joystick in the picture bellow. But any joystick with switching contacts will meet the requirements.

The template class allows to query the individual joystick positions and can trigger a simple event when the joystick swings out in a direction or when it returns to the center position.

### Layout
![Joystick Layout](/assets/documentation/device-examples/components/Layout-Joystick.png)

{{< gallery >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/JoystickDigitalBreadboard.png" caption="Joystick Digital Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/JoystickDigitalTopView.png" caption="Joystick Digital Top View" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/JoystickDigitalBackViewAllAxis.png" caption="Joystick Digital Back View All Axis" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/JoystickDigitalBackViewOneAxis.png" caption="Joystick Digital Back View One Axis" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/JoystickDigitalWiringBack.png" caption="Joystick Digital Wiring Back" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/JoystickDigitalWiringBackCorner.png" caption="Joystick Digital Wiring Back Corner" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code
A simple example on how to use the Joystick-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```java
//Initzalize the joystick component
final var joystick = new Joystick(pi4j, PIN.D5, PIN.D6, PIN.PWM13, PIN.PWM19, PIN.D26);

//Register event handlers to print a message when pressed (onDown) and (onUp)
joystick.onNorth(() -> System.out.println("Start Pressing joystick button North"));
joystick.whileNorth(1000, () -> System.out.println("Pressing joystick button North"));

joystick.onWest(() -> System.out.println("Start Pressing joystick button West"));
joystick.whileWest(1000, () -> System.out.println("Pressing joystick button West"));

joystick.onSouth(() -> System.out.println("Start Pressing joystick button South"));
joystick.whileSouth(1000, () -> System.out.println("Pressing joystick button South"));

joystick.onEast(() -> System.out.println(" Start Pressing joystick button East"));
joystick.whileEast(1000, () -> System.out.println("Pressing joystick button East"));

joystick.onPushDown(() -> System.out.println("Start Pressing joystick button PUSH"));
joystick.onPushUp(() -> System.out.println("Stop pressing joystick button PUSH"));

// Wait for 15 seconds while handling events before exiting
System.out.println("Press the button to see it in action!");
delay(15000);

// Unregister all event handlers to exit this application in a clean way
joystick.deRegisterAll();
```

### Further application
The class is not yet implemented in a project.

### Further project ideas
- Realize the popular arcade game Street Fighter on your own Raspberry Pi.
- Create a claw crane game machine, the hit at every party.