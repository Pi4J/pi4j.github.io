---
title: Joystick
weight: 210
tags: ["Joystick"]
---

### Description

The [Joystick](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/Joystick.java) is a template class, that you can use in your own Java-project.
The template is created for a digital joystick with 4 directions (up, right, down, left) and as an option additionally with a push button in direction down.
A suitable hardware component is the arcade joystick in the picture bellow. But any joystick with switching contacts will meet the requirements.

The template class allows to query the individual joystick positions and can trigger a simple event when the joystick swings out in a direction or when it returns to the center position.

### Layout

![Joystick Layout](/assets/examples/components/components/Layout-Joystick-New.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickDigitalBreadboard.png" caption="Joystick Digital Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickDigitalDetail.jpg" caption="Joystick Digital Breadboard Detail" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickDigitalTopView.png" caption="Joystick Digital Top View" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickDigitalBackViewAllAxis.png" caption="Joystick Digital Back View All Axis" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickDigitalBackViewOneAxis.png" caption="Joystick Digital Back View One Axis" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickDigitalWiringBack.png" caption="Joystick Digital Wiring Back" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/JoystickDigitalWiringBackCorner.png" caption="Joystick Digital Wiring Back Corner" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the Joystick-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
//Initialize the joystick component
final var joystick = new Joystick(pi4j, PIN.D5, PIN.D6, PIN.PWM13, PIN.PWM19, PIN.D26);

//Register all event handlers
joystick.onNorth(() -> System.out.println("Start NORTH"));
joystick.whileNorth(() -> System.out.println("Still NORTH"),
Duration.ofSeconds(1));

joystick.onWest(() -> System.out.println("Start WEST"));
joystick.whileWest(() -> System.out.println("Still WEST"),
Duration.ofSeconds(1));

joystick.onSouth(() -> System.out.println("Start SOUTH"));
joystick.whileSouth(() -> System.out.println("Still SOUTH"),
Duration.ofSeconds(1));

joystick.onEast(() -> System.out.println(" Start EAST"));
joystick.whileEast(() -> System.out.println("Still EAST"),
Duration.ofSeconds(1));

joystick.onPushDown(() -> System.out.println("Start PUSH"));
joystick.onPushUp(() -> System.out.println("Still PUSHing"));

// Wait for 15 seconds while handling events before exiting
System.out.println("Move the joystick and push it's button to see it in action!");
delay(Duration.ofSeconds(15));

// cleanup
joystick.reset();
```

### Further application

The class is not yet implemented in a project.

### Further project ideas

- Realize the popular arcade game Street Fighter on your own Raspberry Pi.
- Create a claw crane game machine, the hit at every party.