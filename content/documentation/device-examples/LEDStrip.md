---
title: LEDStrip
weight: 206
tags: ["LEDStrip"]
---
### Description
The [ledstrip](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
You can take a LED Strip with the WS28xx-chip set. Like for example this one: [LEDStrip](https://www.berrybase.de/sensoren-module/led/ws2812-13-neopixel/stripes/adafruit-neopixel-led-streifen-starter-pack-30-led/meter-schwarz-1m)

The Template Class gives you the option to set the LED's of the strip to a desired RGB-Color.
If you have many strips, you can use the [LEDMatrix](/documentation/device-examples/ledmatrix)

{{% notice note %}}
Make sure to check if SPI is enabled in your RaspberryPI.
Check the SPI Address. Default is "SPI0 MOSI" Pin (#19).
{{% /notice %}}

### Layout
![LEDStrip Layout](/assets/documentation/device-examples/Layout-LEDStrip.png)

### Code
A simple example on how to use the LEDStrip-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
// Initialize the RGB
int pixels = 10;
final var ledstrip = new LEDStrip(pi4j, pixels, 127);

//set them all off, so nothing is shining
logInfo("Starting with setting all leds off");
ledstrip.allOff();

logInfo("setting the leds to RED");
ledstrip.setStripColor(PixelColor.RED);
ledstrip.render();
delay(3000);

logInfo("setting the leds to Light Blue");
ledstrip.setStripColor(PixelColor.LIGHT_BLUE);
ledstrip.render();
delay(3000);

logInfo("setting the first led to Purple");
ledstrip.setPixelColor(0, PixelColor.PURPLE);
ledstrip.render();
delay(3000);

logInfo("setting the brightness to full and just show the first led as White");
ledstrip.allOff();
ledstrip.setBrightness(255);
ledstrip.setPixelColor(0, PixelColor.WHITE);
ledstrip.render();
delay(3000);

//finishing and closing
ledstrip.close();
```

### Further application
The class is implemented in the sample project [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas
- A suit with LED-Strips sewn on, on which different animations can run.
- A LED-strip which can be used as a backlight of a screen. The color and brightness can change to the volume and mood of the displayed images.
