---
title: Controlling a LED Matrix
weight: 171
tags: ["JBang", "Pixelblaze", "LED Strip"]
---

{{% notice tip %}}
GITHUB PROJECT: [github.com/Pi4J/pi4j-jbang > PixelblazeOutputExpanderImageMatrix8x32.java](https://github.com/Pi4J/pi4j-jbang/blob/main/PixelblazeOutputExpanderImageMatrix8x32.java)
{{% /notice %}}

A LED strip doesn't only exist as a single strip, the same system is also used in a LED matrix. In this example, we will control such a [8*32 LED matrix](https://www.amazon.nl/dp/B0B81R484Z).

## Intro

This example is based on the [Pixelblaze Output Expander (PBOE) JBang example](/examples/jbang/pixelblaze_output_expander/). Make sure to check out the PBOE example, so you fully understand how to set up and use JBang, and connect and control a LED strip via a PBOE.

## Application

This example uses the same `helper.PixelBlazeOutputExpanderHelper` to send commands to the PBOE. An additional shared code-file `helper.ImageHelper` is used to handle images.

### JBang Configuration and Imports

As with each JBang example, we need to define the first script line and the dependencies, one in this case, and we need to include the helper-source. This example also needs some more imports.

```java
///usr/bin/env jbang "$0" "$@" ; exit $?

//DEPS com.fazecast:jSerialComm:2.10.2
//SOURCES helper/ImageHelper.java
//SOURCES helper/PixelBlazeOutputExpanderHelper.java

import helper.PixelBlazeOutputExpanderHelper;

import java.io.IOException;
import java.util.Random;

import static helper.ImageHelper.getImageData;
import static helper.ImageHelper.imageToMatrix;
```

### Enum With Images

Within the [JBang sample project you can find a data directory](https://github.com/Pi4J/pi4j-jbang/tree/main/data). In this directory, a number of test images is available, PNGs with a size of 8 pixels height by 32 pixels width, matching the size of the matrix. By defining them in the code as an enum, we can add extra info, like the duration we want to display them. 

```java
    private enum TestImage {
        LINE_1("image_8_32_line_1.png", 250),
        LINE_2("image_8_32_line_2.png", 250),
        LINE_3("image_8_32_line_3.png", 250),
        LINE_4("image_8_32_line_4.png", 250),
        LINE_5("image_8_32_line_5.png", 250),
        LINE_6("image_8_32_line_6.png", 250),
        LINE_7("image_8_32_line_7.png", 250),
        LINE_8("image_8_32_line_8.png", 250),
        RED("image_8_32_red.png", 500),
        GREEN("image_8_32_green.png", 500),
        BLUE("image_8_32_blue.png", 500),
        STRIPES("image_8_32_stripes.png", 2000),
        STRIPES_TEST("image_8_32_stripes_test.png", 2000),
        DUKE("image_8_32_duke.png", 2000),
        RPI("image_8_32_raspberrypi.png", 2000);

        private final String fileName;
        private final int duration;

        TestImage(String fileName, int duration) {
            this.fileName = fileName;
            this.duration = duration;
        }

        public String getFileName() {
            return fileName;
        }

        public int getDuration() {
            return duration;
        }
    }
```

### Loading an Image as RGB Byte Array

As we need to send a byte array with red, green, blue values to the LED strip, we need a method to load an image file and return each pixel as three values. There are several methods available in Java to achieve this. I used `bufferedImage.getRGB(x, y)` to be able to validate the color returned from every pixel to make it easy to debug.

```java
    private static byte[] getImageData(String imagePath) throws IOException {
        byte[] imageData = new byte[NUMBER_OF_LEDS * BYTES_PER_PIXEL];

        // Open image
        File imgPath = new File(imagePath);
        BufferedImage bufferedImage = ImageIO.read(imgPath);

        // Read color values for each pixel
        int pixelCounter = 0;
        for (int y = 0; y < 8; y++) {
            for (int x = 0; x < 32; x++) {
                int color = bufferedImage.getRGB(x, y);
                imageData[pixelCounter * BYTES_PER_PIXEL] = (byte) ((color & 0xff0000) >> 16); // Red
                imageData[(pixelCounter * BYTES_PER_PIXEL) + 1] = (byte) ((color & 0xff00) >> 8); // Green
                imageData[(pixelCounter * BYTES_PER_PIXEL) + 2] = (byte) (color & 0xff); // Blue
                pixelCounter++;
            }
        }

        return imageData;
    }
```

#### Detecting the Orientation of the Strip

While working on this example, I didn't get the output I was expecting. My assumption was that the LEDs are wired in rows, which would be the easiest way to use them.

```text
Column          1   2   3   4   ...    32
Row 1   IN   >                              > OUT, connected to beginning of row 2
Row 2   IN   >                              > OUT, connected to beginning of row 3
Row 3   IN   >                              > OUT, connected to beginning of row 4
...
```

With the following code, RED is sent to each LED, one by one, from position 0 to the final LED.

```java
// Check the position of the LEDs, to identify how the LED strip is wired
System.out.println("One by one RED");
for (i = 0; i < NUMBER_OF_LEDS; i++) {
    byte[] pixelData = new byte[NUMBER_OF_LEDS * BYTES_PER_PIXEL];
    pixelData[i * BYTES_PER_PIXEL] = (byte) 0xff; // red
    helper.sendColors(CHANNEL, BYTES_PER_PIXEL, 1, 0, 2, 0, pixelData, false);
    Thread.sleep(20);
}
```

With this code, I found out the wiring, on the matrix that I use, is actually totally different

2191
```text
Column          1     2     3     4     ...    32
                IN    OUT   IN    OUT
                      TO 3        TO 5
                &#x2B07;    &#x2B06;     &#x2B07;    &#x2B06;    ...
Row 1   
Row 2   
Row 3   
...
Row 8
                &#x2B07;    &#x2B06;    &#x2B07;     &#x2B06;    ...
                OUT   IN    OUT   IN
                TO 2        TO 4
```

As it turns out the order of the LEDs doesn't match the X/Y system of an image, an extra method is needed to "flip" the X/Y into the actual ordering of the LEDs. Although this method is easy, it took me some iterations to find a correct approach...

```java
private static byte[] imageToMatrix(byte[] imageData) {
    byte[] matrixData = new byte[imageData.length];

    int indexInImage = 0;;
    for (int row = 0; row < 8; row++) {
        for (int column = 0; column < 32; column++) {
            int indexInMatrix = (column * 8) + (column % 2 == 0 ? row : 7 - row);
            //System.out.println("Row : " + row + " / column: " + column + " / index image : " + indexInImage + " / index matrix: " + indexInMatrix);
            matrixData[indexInMatrix * BYTES_PER_PIXEL] = imageData[indexInImage * BYTES_PER_PIXEL];
            matrixData[(indexInMatrix * BYTES_PER_PIXEL) + 1] = imageData[(indexInImage * BYTES_PER_PIXEL) + 1];
            matrixData[(indexInMatrix * BYTES_PER_PIXEL) + 2] = imageData[(indexInImage * BYTES_PER_PIXEL) + 2];
            indexInImage++;
        }
    }

    return matrixData;
}
```

#### Displaying the Images

With the enum and additional methods, we can now very easy display all the images for the duration that is defined in each enum value.

```java
// Output all defined images
for (TestImage testImage : TestImage.values()) {
    System.out.println("Image: " + testImage);

    // Get the bytes from the given image
    byte[] pixelData = imageToMatrix(getImageData("data/" + testImage.getFileName()));

    // Show the image on the LED matrix
    helper.sendColors(CHANNEL, BYTES_PER_PIXEL, 1, 0, 2, 1, pixelData, false);

    Thread.sleep(testImage.getDuration());
}
```

#### Other Effects

Some other effects are included in the example which are not using images.

```java
// All white to test load on power supply
System.out.println("Full RGB");
byte[] allWhite = new byte[NUMBER_OF_LEDS * BYTES_PER_PIXEL];
for (i = 0; i < NUMBER_OF_LEDS * BYTES_PER_PIXEL; i++) {
    allWhite[i] = (byte) 0xff;
}
helper.sendColors(CHANNEL, BYTES_PER_PIXEL, 1, 0, 2, 0, allWhite, false);
Thread.sleep(5000);

// Random colors
Random rd = new Random();
for (i = 0; i < 100; i++) {
    byte[] random = new byte[8 * 32 * BYTES_PER_PIXEL];
    rd.nextBytes(random);
    helper.sendColors(CHANNEL, BYTES_PER_PIXEL, 1, 0, 2, 0, random, false);
    Thread.sleep(50);
}
```

## Running the Application

No `sudo` is needed for serial communication with the `jSerialComm` library, so the application can be started with:

```bash
$ jbang PixelblazeOutputExpanderImageMatrix.java
[jbang] Building jar for PixelblazeOutputExpanderImageMatrix.java...
Initializing serial
Opening /dev/ttyS0
All off
One by one RED
Full RGB
Image: LINE_1
Image: LINE_2
Image: LINE_3
Image: LINE_4
Image: LINE_5
Image: LINE_6
Image: LINE_7
Image: LINE_8
Image: RED
Image: GREEN
Image: BLUE
Image: STRIPES
Image: STRIPES_TEST
Image: DUKE
Image: RPI
All off
Closing /dev/ttyS0
```

## Controlling an 8x8 matrix

Within the GitHub project, you can also find an example to send images to an 8x8 matrix.

{{% notice tip %}}
GITHUB PROJECT: [github.com/Pi4J/pi4j-jbang > PixelblazeOutputExpanderImageMatrix8x8.java](https://github.com/Pi4J/pi4j-jbang/blob/main/PixelblazeOutputExpanderImageMatrix8x8.java)
{{% /notice %}}

## Conclusion

By reusing the existing Pixelblaze Output Expander helper code, we are able to control a LED matrix and experiment with images.