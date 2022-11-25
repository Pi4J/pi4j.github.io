---
title: LED Button
weight: 210
tags: ["LEDButton"]
---

### Description

The [LedButton](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/LedButton.java) is a template class, that you can use in your own Java-project.
You can take any Button with a LED you want to. Like for example the big button bellow in the picture gallery.

The Template Class gives you the option to check the state of the button, and to create simple events if the button is pressed or depressed, or the whole time is is being pressed. Also it lets you control the LED.

### Layout

![LEDButton Layout](/assets/examples/components/components/Layout-LEDButton.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/LedButtonBreadboard.png" caption="Led Button Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/BigButton.png" caption="Big Button" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the Button-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
        System.out.println("LED button app started ...");

// Initialize the button component
final LedButton ledButton = new LedButton(pi4j, PIN.D26, Boolean.FALSE, PIN.PWM19);

// Turn on the LED to have a defined state
ledButton.ledOn();
//see the LED for a Second
delay(1000);

// Register event handlers to print a message when pressed (onDown) and depressed (onUp)
ledButton.btnOnDown(() -> System.out.println("Pressing the Button"));
ledButton.btnOnUp(()   -> System.out.println("Stopped pressing."));

// Wait for 15 seconds while handling events before exiting
System.out.println("Press the button to see it in action!");

// Make a flashing light by toggling the LED every second
// in the meantime, the Button can still be pressed, as we only freeze the main thread
for (int i = 0; i < 15; i++) {
System.out.println(ledButton.ledToggleState());
delay(1000);
}

// Unregister all event handlers to exit this application in a clean way
ledButton.btnDeRegisterAll();
ledButton.ledOff();

System.out.println("LED button app done.");
```

### Further application

The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Photobooth](https://github.com/DieterHolz/PhotoBooth).

### Further project ideas

- An application, which includes a button. if the button is pressed, the app will order you a crate of beer from your favorite store.
- An application, where you can play "whack a mole". If the LED is on and you hit the right button, you get points.
