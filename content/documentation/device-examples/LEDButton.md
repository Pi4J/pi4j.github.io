---
title: LEDButton
weight: 203
tags: ["LEDButton"]
---
### Description
The [LEDButton](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
You can take any Button with a LED you want to. Like for example this one: [LEDButton](https://www.berrybase.de/bauelemente/schalter-taster/drucktaster/massive-arcade-button-100mm-beleuchtet-40-led-12v-dc-41)

The Template Class gives you the option to check the state of the button, and to create simple events if the button is pressed or depressed, or the whole time is is being pressed. Also it lets you control the LED.

### Layout
![LEDButton Layout](/assets/documentation/device-examples/Layout-LEDButton.png)

### Code
A simple example on how to use the Button-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
// Initialize the button component
final var ledbutton = new LEDButton(pi4j, PIN.D26, Boolean.FALSE, PIN.PWM19);

// Turn on the LED to have a defined state
ledbutton.LEDsetStateOn();
//see the LED for a Second
delay(1000);

// Register event handlers to print a message when pressed (onDown) and depressed (onUp)
ledbutton.onDown(() -> logInfo("Pressing the Button"));
ledbutton.onUp(()   -> logInfo("Stopped pressing."));

// Wait for 15 seconds while handling events before exiting
System.out.println("Press the button to see it in action!");

// Make a flashing light by toggling the LED every second
// in the meantime, the Button can still be pressed, as we only freeze the main thread
for (int i = 0; i < 15; i++) {
	System.out.println(ledbutton.LEDtoggleState());
	delay(1000);
}

// Unregister all event handlers to exit this application in a clean way
ledbutton.btndeRegisterAll();
ledbutton.LEDsetStateOff();
System.out.println("Everything off");
```

### Further application
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas
- An application, which includes a button. if the button is pressed, the app will order you a crate of beer from your favorite store.
- An application, where you can play "whack a mole". If the LED is on and you hit the right button, you get points.
