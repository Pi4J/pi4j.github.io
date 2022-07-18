---
title: LED Strip
weight: 210
tags: ["LEDStrip"]
---
### Description
The [ledstrip](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/components) (src/main/java/com/pi4j/components) is a template class, that you can use in your own Java-project.
You can take a LED Strip with the WS28xx-chip set.

The Template Class gives you the option to set the LED's of the strip to a desired RGB-Color.
If you have many strips, you can use the [LEDMatrix](/documentation/device-examples/ledmatrix)

{{% notice note %}}
Make sure to check if SPI is enabled in your RaspberryPI.
Check the SPI Address. Default is "SPI0 MOSI" Pin (#19).
{{% /notice %}}

### Layout
![LEDStrip Layout](/assets/documentation/device-examples/components/Layout-LEDStrip.png)

{{< gallery >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/LED-Strip4-LED-Breadboard.png" caption="LED Strip 4 LED Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/LED-Strip4-LED.png" caption="LED Strip 4 LED" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code
A simple example on how to use the LEDStrip-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
// Initialize the RGB
int pixels = 4;
final var ledstrip = new LEDStrip(pi4j, pixels, 0.5);

//set them all off, so nothing is shining
System.out.println("Starting with setting all leds off");
ledstrip.allOff();

System.out.println("setting the LEDs to RED");
ledstrip.setStripColor(LEDStrip.PixelColor.RED);
ledstrip.render();
delay(3000);

System.out.println("setting the LEDs to Light Blue");
ledstrip.setStripColor(LEDStrip.PixelColor.LIGHT_BLUE);
ledstrip.render();
delay(3000);

System.out.println("setting the first led to Purple");
ledstrip.setPixelColor(0, LEDStrip.PixelColor.PURPLE);
ledstrip.render();
delay(3000);

System.out.println("setting the brightness to full and just show the first led as White");
ledstrip.allOff();
ledstrip.setBrightness(1);
ledstrip.setPixelColor(0, LEDStrip.PixelColor.WHITE);
ledstrip.render();
delay(3000);

//finishing and closing
ledstrip.close();
System.out.println("closing the app");
System.out.println("Color "+ ledstrip.getPixelColor(0));
```

### Further application
The class is implemented in the sample project [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further project ideas
- A suit with LED-Strips sewn on, on which different animations can run.
- A LED-strip which can be used as a backlight of a screen. The color and brightness can change to the volume and mood of the displayed images.
