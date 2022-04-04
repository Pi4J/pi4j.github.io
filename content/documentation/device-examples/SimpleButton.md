---
title: Simple Button
weight: 200
tags: ["Simple Button"]
---
### Description
The simplebutton is a template class, that you can use in your own Java-project.
You can take any Button you want to. Like for example this one: [Arcade Button](https://www.berrybase.de/bauelemente/schalter-taster/drucktaster/arcade-button-30mm)
To Template Class gives you the option to check the state of the button, and to create simple events if the button is pressed or depressed.
The class implements the simpleInput template.

### Layout
![Simple Button Layout](/assets/documentation/Devices/Layout-SimpleButton.png)

### Code
A simple Example on how to use the Button-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
// Initialize the button component
final var button = new SimpleButton(pi4j, 26, Boolean.TRUE);

// Register event handlers to print a message when pressed (onDown) and depressed (onUp)
button.onDown(() -> System.out.println("Pressing the Button"));
button.onUp(() -> System.out.println("Stopped pressing."));

// Wait for 15 seconds while handling events before exiting
System.out.println("Press the button to see it in action!");
sleep(15000);

// Unregister all event handlers to exit this application in a clean way
button.onDown(null);
button.onUp(null);
```

### Further application / project ideas
- An application, which includes a button. if the button is pressed, the app will order you a crate of beer from your favorite store.
- An application, which includes a buzzer and a button. If the button is pressed, the buzzer beeps.