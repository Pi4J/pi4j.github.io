---
title: LCD Display
weight: 204
tags: ["LCD Display"]
---
### Description
The [LCD Display](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
It is used to show Numbers, Text and Symbols on a small Display.
The Class supports only LCD Displays with the PCF8574T I2C Backpack. Supported Displays are 40x2, 20x4, 20x2, 16x2, 16x1.
A suitable hardware component is: [LCD Display](https://www.berrybase.de/sensoren-module/displays/alphanumerische-displays/alphanumerisches-lcd-16x2-blau/wei-223-mit-i2c-backpack)

{{% notice note %}}
IF YOU CAN'T SEE ANYTHING WRITTEN ON THE DISPLAY, TRY TO SET THE CONTRAST BY TURNING THE CONTRAST-SCREW WITH A SCREWDRIVER
{{% /notice %}}

### Layout
![LCD Display Layout](/assets/documentation/device-examples/Layout-LCDDisplay.png)

### Code
An example on how to use the LCD Display-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components)

The PI4J-Context must add the LinuxFsI2CProvider.newInstance() Provider, which is explained under [LinuxFS](/documentation/providers/linuxfs/)
```
pi4j = Pi4J.newContextBuilder()
	.noAutoDetect()
	.add(new RaspberryPiPlatform() {
		@Override
		protected String[] getProviders() {
			return new String[]{};
		}
	})
	.add(PiGpioDigitalInputProvider.newInstance(piGpio),
			PiGpioDigitalOutputProvider.newInstance(piGpio),
			PiGpioPwmProvider.newInstance(piGpio),
			PiGpioSerialProvider.newInstance(piGpio),
			PiGpioSpiProvider.newInstance(piGpio),
			LinuxFsI2CProvider.newInstance()
	)
	.build();
```
When the right Context is loaded, you can use the Display like following:
```
//Create a Component, with amount of ROWS and COLUMNS of the Device
LCDDisplay lcd = new LCDDisplay(pi4j, 4, 20);
System.out.println("Here we go.. let's have some fun with that LCD Display!");

// Turn on the backlight makes the display appear turned on
lcd.setDisplayBacklight(true);

// Write text to the lines separate
lcd.displayText("Hello", 1);
lcd.displayText("   World!", 2);
lcd.displayText("Line 3", 3);
lcd.displayText("   Line 4", 4);

// Wait a little to have some time to read it
sleep(3000);

// Clear the display to start next parts
lcd.clearDisplay();

// To write some text there are different methods. The simplest one is this one which automatically inserts
// linebreaks if needed.
lcd.displayText("Boohoo that's so simple to use!");

// Delay again
sleep(3000);

// Of course it is also possible to write with newLine Chars
lcd.displayText("Some Big Text \n with some new Lines \n just testing");
sleep(3000);

// Of course it is also possible to write long text
lcd.displayText("Some Big Text with no new Lines, just to test how many lines will get filled");
sleep(3000);

lcd.displayText("Small Text with \nnew");
sleep(3000);

// Clear the display to start next parts
lcd.clearDisplay();

// Let's try to draw a house. To keep this method short and clean we create the characters in a separate
// method below.
createCharacters(lcd);

// Now all characters are ready. Just draw them on the right place by moving the cursor and writing the
// created characters to specific positions
lcd.writeCharacter('\1', 1, 1);
lcd.writeCharacter('\2', 2, 1);
lcd.writeCharacter('\3', 1, 2);
lcd.writeCharacter('\4', 2, 2);
delay(3000);

// Turn off the backlight makes the display appear turned off
lcd.setDisplayBacklight(false);
lcd.clearDisplay();

public void createCharacters(LCDDisplay lcd) {
// Create upper left part of the house
  lcd.createCharacter(1, new byte[]{
	0b00000,
	0b00000,
	0b00000,
	0b00001,
	0b00011,
	0b00111,
	0b01111,
	0b11111
  });

// Create upper right part of the house
  lcd.createCharacter(2, new byte[]{
	0b00000,
	0b00000,
	0b00010,
	0b10010,
	0b11010,
	0b11110,
	0b11110,
	0b11111
  });

// Create lower left part of the house
  lcd.createCharacter(3, new byte[]{
	0b11111,
	0b11111,
	0b11111,
	0b11111,
	0b10001,
	0b10001,
	0b10001,
	0b10001
  });

// Create lower right part of the house
  lcd.createCharacter(4, new byte[]{
	0b11111,
	0b11111,
	0b11111,
	0b10001,
	0b10001,
	0b10001,
	0b11111,
	0b11111
  });
}
```
Create an own [Symbol](https://www.8051projects.net/lcd-interfacing/lcd-custom-character.php)

### Further application
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas

- A Temperature Sensor hooked to a disply, where it shows how warm it is
- A Microfone, which listens what is said, and writing on the display what is said
