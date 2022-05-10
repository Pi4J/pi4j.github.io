---
title: LEDStrip
weight: 206
tags: ["LEDStrip"]
---
### Description
The [ledstrip](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
You can take a LED Strip with the WS28xx-chip set. Like for example this one: [LEDStrip](https://www.berrybase.de/sensoren-module/led/ws2812-13-neopixel/stripes/adafruit-neopixel-led-streifen-starter-pack-30-led/meter-schwarz-1m)
The Template Class gives you the option to set the LED's of the strip to a desired RGB-Color.

### Layout
![LEDStrip Layout](/assets/documentation/device-examples/Layout-LEDStrip.png)

### Code
A simple example on how to use the LEDStrip-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
// Initialize the RGB
int pixels = 8;
final var ledstrip = new RGBLed(pi4j, PIN.D26, pixels, 127);

//set them all off, so nothing is shining
logger.info("Starting with setting all leds off");
ledstrip.allOff();

for(int i = 0; i < 5; i++){

	//increment red value
	logger.info("setting the leds to a shade of red");
	int red = 0;
	for (int j = 0; j < pixels; j++) {
		ledstrip.setPixelColor(j, red);
		red += 255 / pixels;
	}
	//show it on the strip
	ledstrip.render();
	delay(2000);

	//increment green value
	logger.info("setting the leds to a shade of green");
	int green = 0;
	for (int j = 0; j < pixels; j++) {
		ledstrip.setPixelColor(j, green);
		green += 255 / pixels;
	}
	//show it on the strip
	ledstrip.render();
	delay(2000);

	//increment blue value
	logger.info("setting the leds to a shade of blue");
	int blue = 0;
	for (int j = 0; j < pixels; j++) {
		ledstrip.setPixelColor(j, blue);
		blue += 255 / pixels;
	}
	//show it on the strip
	ledstrip.render();
	delay(2000);
}

logger.info("setting the leds to purple");
ledstrip.setStripColor(PixelColor.PURPLE);
ledstrip.render();
delay(3000);

//finishing and closing
ledstrip.close();
logger.info("closing the app");
```

### Further application
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas
- A Suit with LED-Strips sewn on, where you can display animations on the strips
- A RGB-Strip, where you stream your Display on, to use it as ambient light
