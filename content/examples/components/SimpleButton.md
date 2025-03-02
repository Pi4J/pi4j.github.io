---
title: Simple Button
weight: 200
tags: ["Simple Button", "Button"]
---

### Description

The [SimpleButton](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/SimpleButton.java) is a template class, that you can use in your own Java-project.

The Template Class gives you the option to check the state of the button, and to create simple events if the button is pressed, depressed or while it is being pressed.

### Layout

![Simple Button Layout](/assets/examples/components/components/Layout-SimpleButton.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/SimpleButtonBreadboard.png" caption="Simple Button Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/BigButton.png" caption="Big Button" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the Button-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
// Initialize the button component
final var button = new SimpleButton(pi4j, PIN.D26, Boolean.FALSE);

 // Register event handlers to print a message when pressed (onDown) and depressed (onUp)
 button.onDown      (() -> System.out.println("Button pressed"));
 button.whilePressed(() -> System.out.println("Still pressing"), Duration.ofSeconds(1));
 button.onUp        (() -> System.out.println("Stopped pressing"));

 // Wait for 15 seconds while handling events before exiting
 System.out.println("Press the button to see it in action!");
 delay(Duration.ofSeconds(15));

 // Unregister all event handlers to exit this application in a clean way
 button.reset();
```

### Further project ideas

- An application, which includes a button. if the button is pressed, the app will order you a crate of beer from your favorite store.
- An application, which includes a buzzer and a button. If the button is pressed, the buzzer beeps.