---
title: LED Strip
weight: 210
tags: ["LED Strip"]
---

### Description

The [LedStrip](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/LedStrip.java) is a template class, that you can use in your own Java-project.
You can take a LED Strip with the WS28xx-chip set.

The Template Class gives you the option to set the LED's of the strip to a desired RGB-Color.
If you have many strips, you can use the [LEDMatrix](https://pi4j.com/examples/components/ledmatrix/)

{{% notice note %}}
Make sure to check if SPI is enabled in your RaspberryPI.
Check the SPI Address. Default is "SPI0 MOSI" Pin (#19).
{{% /notice %}}

### Layout

![LEDStrip Layout](/assets/examples/components/components/Layout-LEDStrip.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/LED-Strip4-LED-Breadboard.png" caption="LED Strip 4 LED Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/LED-Strip4-LED.png" caption="LED Strip 4 LED" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the LEDStrip-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
System.out.println("LED strip app started ...");
// Initialize the RGB
int pixels = 4;
final LedStrip ledStrip = new LedStrip(pi4j, pixels, 0.5);

//set them all off, so nothing is shining
System.out.println("Starting with setting all leds off");
ledStrip.allOff();

System.out.println("setting the LEDs to RED");
ledStrip.setStripColor(LedStrip.PixelColor.RED);
ledStrip.render();
delay(3000);

System.out.println("setting the LEDs to Light Blue");
ledStrip.setStripColor(LedStrip.PixelColor.LIGHT_BLUE);
ledStrip.render();
delay(3000);

System.out.println("setting the first led to Purple");
ledStrip.setPixelColor(0, LedStrip.PixelColor.PURPLE);
ledStrip.render();
delay(3000);

System.out.println("setting the brightness to full and just show the first led as White");
ledStrip.allOff();
ledStrip.setBrightness(1);
ledStrip.setPixelColor(0, LedStrip.PixelColor.WHITE);
ledStrip.render();
delay(3000);

//finishing and closing
ledStrip.close();
System.out.println("closing the app");
System.out.println("Color "+ ledStrip.getPixelColor(0));

System.out.println("LED strip app done.");
```

### Further application

The class is implemented in the sample project [Photobooth](https://github.com/DieterHolz/PhotoBooth).

### Further project ideas

- A suit with LED-Strips sewn on, on which different animations can run.
- A LED-strip which can be used as a backlight of a screen. The color and brightness can change to the volume and mood of the displayed images.
