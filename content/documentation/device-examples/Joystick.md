---
title: Joystick
weight: 202
tags: ["Joystick"]
---
### Description
The [Joystick](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
The template is created for a digital joystick with 4 directions (up, right, down, left) and as an option additionally with a push button in direction down.
A suitable hardware component is: : [Joystick](https://www.reichelt.com/ch/de/entwicklerboards-arcade-knopf-joystick-kit-debo-arcade-kit-p256436.html?PROVID=2808&gclid=CjwKCAiAgvKQBhBbEiwAaPQw3MO3WLBqcT6DHMUkYO6i48psAwyXVe3VInKECFcebdgTe-iKTppDCxoC_uEQAvD_BwE)

The template class allows to query the individual joystick positions and can trigger a simple event when the joystick swings out in a direction or when it returns to the center position.
The class implements the simpleInput template.

### Layout
![Joystick Layout](/assets/documentation/device-examples/Layout-Joystick.png)

### Code
A simple example on how to use the Joystick-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
//Initzalize the joystick component
final var joystick = new Joystick(pi4j, 5,6,13,19,26);

//Register event handlers to print a message when pressed (onDown) and (onUp)
joystick.buttonUpOnDown(() -> System.out.println("Pressing joystick button UP"));
joystick.buttonUpOnUp(() -> System.out.println("Stop pressing joystick button UP"));

joystick.buttonLeftOnDown(() -> System.out.println("Pressing joystick button LEFT"));
joystick.buttonLeftOnUp(() -> System.out.println("Stop pressing joystick button LEFT"));

joystick.buttonDownOnDown(() -> System.out.println("Pressing joystick button DOWN"));
joystick.buttonDownOnUp(() -> System.out.println("Stop pressing joystick button DOWN"));

joystick.buttonRightOnDown(() -> System.out.println("Pressing joystick button RIGHT"));
joystick.buttonRightOnUp(() -> System.out.println("Stop pressing joystick button RIGHT"));

joystick.buttonPushOnDown(() -> System.out.println("Pressing joystick button PUSH"));
joystick.buttonPushOnUp(() -> System.out.println("Stop pressing joystick button PUSH"));

// Wait for 15 seconds while handling events before exiting
System.out.println("Press the button to see it in action!");
sleep(15000);

// Unregister all event handlers to exit this application in a clean way
joystick.buttonUpOnDown(null);
joystick.buttonUpOnUp(null);

joystick.buttonLeftOnDown(null);
joystick.buttonLeftOnUp(null);

joystick.buttonDownOnDown(null);
joystick.buttonDownOnUp(null);

joystick.buttonRightOnDown(null);
joystick.buttonRightOnUp(null);

joystick.buttonPushOnDown(null);
joystick.buttonPushOnUp(null);

joystick.buttonUpOnDown(null);
joystick.buttonUpOnUp(null);
```

### Further application
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth]().

### Further projetct ideas

- Realize the popular arcade game Street Fighter on your own Raspberry Pi.
- Create a crane claws game, the hit at every party.