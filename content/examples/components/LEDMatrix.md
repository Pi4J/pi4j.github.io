---
title: LED Matrix
weight: 210
tags: ["LEDMatrix"]
---

### Description

The [LEDMatrix](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j//catalog/components/LEDMatrix.java) is a template class, that you can use in your own Java-project.
It is an extension of the class [LEDStrip](/examples/components/components/ledstrip). An LED matrix can be built from one LED strip. To do this, separate the LED strip at the desired point and place the individual strips under each other or next to each other. The individual ends can then be connected to each other with a wire.
The constructor can be passed either as a rectangular matrix or a user-defined matrix with different numbers of LEDs in the individual strips. A software compatible LED strip is for example the WS28xx-chip set LED Strip.

{{% notice note %}}
Make sure to check if SPI is enabled in your RaspberryPI.
Check the SPI Address. Default is "SPI0 MOSI" Pin (#19).
{{% /notice %}}

### Layout

![LEDMatrix Layout](/assets/examples/components/components/Layout-LEDMatrix.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/LED-MatrixBreadboard.png" caption="LED Matrix Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/LED-Matrix.png" caption="LED Matrix" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the LEDMatrix-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
int Rows = 3;
int Columns = 4;
double brightness = 0.5;

System.out.println("Initialising the matrix");
LEDMatrix ledMatrix = new LEDMatrix(pi4j, Rows, Columns, brightness);

System.out.println("Setting all LEDs to Red.");
ledMatrix.setMatrixColor(LEDStrip.PixelColor.RED);
ledMatrix.render();
delay(3000);

System.out.println("setting the second strip to green");
ledMatrix.setStripColor(1, LEDStrip.PixelColor.GREEN);
ledMatrix.render();
delay(3000);

System.out.println("Setting the third led of the third strip to Yellow");
ledMatrix.setPixelColor(2, 2, LEDStrip.PixelColor.YELLOW);
ledMatrix.render();
delay(3000);

ledMatrix.close();
```

### Further application

The class is not yet implemented in a project.

### Further project ideas

- A suit with a sewn-on LED matrix, which can be used to display images and animations.
- A LED-strip which can be used as a backlight of a screen. The color and brightness can change to the volume and mood of the displayed images.