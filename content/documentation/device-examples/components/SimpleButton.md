---
title: Simple Button
weight: 200
tags: ["Simple Button"]
---
### Description
The [SimpleButton](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/SimpleButton.java) is a template class, that you can use in your own Java-project.

The Template Class gives you the option to check the state of the button, and to create simple events if the button is pressed, depressed or while it is being pressed.

### Layout
![Simple Button Layout](/assets/documentation/device-examples/components/Layout-SimpleButton.png)

{{< gallery >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/SimpleButtonBreadboard.png" caption="Simple Button Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/BigButton.png" caption="Big Button" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code
A simple example on how to use the Button-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```java
// Initialize the button component
final var button = new SimpleButton(pi4j, PIN.D26, Boolean.FALSE);


// Register event handlers to print a message when pressed (onDown) and depressed (onUp)
button.onDown      (() -> logInfo("Pressing the button"));
button.whilePressed(() -> logInfo("Pressing"), 1000);
button.onUp        (() -> logInfo("Stopped pressing."));

// Wait for 15 seconds while handling events before exiting
System.out.println("Press the button to see it in action!");
delay(15_000);

// Unregister all event handlers to exit this application in a clean way
button.deRegisterAll();

/*
if you want to deRegister only a single function, you can do so like this:
button.onUp(null);
*/
```

### Further application
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Photobooth](https://github.com/DieterHolz/PhotoBooth).

### Further project ideas
- An application, which includes a button. if the button is pressed, the app will order you a crate of beer from your favorite store.
- An application, which includes a buzzer and a button. If the button is pressed, the buzzer beeps.