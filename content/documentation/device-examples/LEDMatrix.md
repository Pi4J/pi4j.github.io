---
title: LEDMatrix
weight: 207
tags: ["LEDMatrix"]
---
### Description
The [LEDMatrix](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
It is an extension of the class [LEDStrip](/documentation/device-examples/ledstrip). You can use many Neopixel-LED-Strips, cut them in between the LEDs, and sold them back together with wires.
Like this, you can generate a matrix on your own, with many strips wired together.

{{% notice note %}}
Make sure to check if SPI is enabled in your RaspberryPI.
Check the SPI Address. Default is "SPI0 MOSI" Pin (#19).
{{% /notice %}}

### Layout
![LEDStrip Layout](/assets/documentation/device-examples/Layout-LEDStrip.png)

### Code
A simple example on how to use the LEDMatrix-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
int Rows = 3;
int Columns = 3;
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
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas
- A Suit with LED-Strips sewn on, where you can display animations on the strips. the strips are now all serial, in the same matrix
- A RGB-Strip, where you stream your Display on, to use it as ambient light