---
title: Joystick
weight: 202
tags: ["Joystick"]
---
### Description
The [Joystick](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
The template is created for a digital joystick with 4 directions (up, right, down, left) and as an option additionally with a push button in direction down.
A suitable hardware component is: [Joystick](https://www.reichelt.com/ch/de/entwicklerboards-arcade-knopf-joystick-kit-debo-arcade-kit-p256436.html?PROVID=2808&gclid=CjwKCAiAgvKQBhBbEiwAaPQw3MO3WLBqcT6DHMUkYO6i48psAwyXVe3VInKECFcebdgTe-iKTppDCxoC_uEQAvD_BwE)

The template class allows to query the individual joystick positions and can trigger a simple event when the joystick swings out in a direction or when it returns to the center position.

### Layout
![Joystick Layout](/assets/documentation/device-examples/Layout-Joystick.png)

### Code
A simple example on how to use the Joystick-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
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

### Further projetct ideas
- Realize the popular arcade game Street Fighter on your own Raspberry Pi.
- Create a claw crane game machine, the hit at every party.