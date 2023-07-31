---
title: Pixelblaze Output Expander
weight: 170
tags: ["JBang", "Pixelblaze", "LED Strip"]
---

{{% notice tip %}}
GITHUB PROJECT: [github.com/Pi4J/pi4j-jbang > PixelblazeOutputExpander.java](https://github.com/Pi4J/pi4j-jbang/blob/main/PixelblazeOutputExpander.java)
{{% /notice %}}

One of the most "fancy" electronic components is definitely a LED strip. It's really cool to control a long strip of lights with only a few lines of code... But, there is a problem. The timings of the signals is crucial to reliably control these strips. Both Python and Java on a Raspberry Pi can struggle with these timings as they are running on Linux, a non-real-time operating system. So pauzes in the garbage collection of the virtual machine of Java, or any hickup in the operation of the operating system can cause unexpected effects on the LED strips. That's why in most projects a microcontroller (Arduino, Raspberry Pi Pico, ESP32,...) is used to drive the LED strip. 

## Intro

This example is using such approach with the [Pixelblaze Output Expander (PBOE)](https://shop.electromage.com/products/pixelblaze-output-expander-serial-to-8x-ws2812-apa102-driver). This product was initially intended to connect more LED strips to the [Pixelblaze V3 Standard - WiFi LED Controller](https://shop.electromage.com/products/pixelblaze-v3-standard-wifi-led-controller) and [Pixelblaze V3 Pico - Tiny WiFi LED Controller](https://shop.electromage.com/products/pixelblaze-v3-pico-tiny-wifi-led-controller). But because the expander is controlled through a serial connection, we can also control it from a Raspberry Pi.

The LED strips that are used, contain LEDs of the WS2812B type, which means they have SMD 5050-LEDs with an integrated IC-driver, so they can be addressed separately. A few examples:

* [LED strip on Amazon](https://www.amazon.nl/dp/B08Y8QXTCL)
* [LED matrix on Amazon](https://www.amazon.nl/dp/B0B81R484Z)
* [Many variants on ebay](https://www.ebay.de/b/WS2812B-LEDs/bn_7005777392)

{{% notice warning %}}
Before proceeding with this example, make sure that you have a Raspberry Pi prepared to execute Java code with JBang as [explained here](https://pi4j.com/examples/jbang/).
{{% /notice %}}

## Wiring

To control the PBOE, we actually only need one wire to be connected to the Raspberry Pi (RPi) for the serial data to be sent from RPi to PBOE. But we must not forget one important fact: a LED strip with a lot of LEDs will require more power than the RPi can supply. So we need an external power supply of 5V that is dimensioned correctly to provide all the power needed for the strip when all LEDs are at maximum level.

Connections between RPi, PBOE, and power supply:

* GND PBOE to GND power supply, common with GND of RPi
* 5V PBOE to external power supply
* DAT PBOE to BCM14 on Rpi (pin 8 = UART Tx)

Connections between PBOE and LED strip:

* Din to PBOE Channel 0, Data
* 5V to PBOE Channel 0, 5V
* GND to PBOE Channel 0, GND

{{< gallery >}}
{{< figure link="/assets/examples/jbang/pixelblaze/full-setup.jpg" caption="Full setup of this project" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/jbang/pixelblaze/led-strip.jpg" caption="LED strip with three connections for power, ground, and data" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/jbang/pixelblaze/pixelblaze-output-expander.jpg" caption="Pixelblaze Output Expander" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/jbang/pixelblaze/raspberry-pi-connections.jpg" caption="Connections on the Raspberry Pi" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/jbang/pixelblaze/pixelblaze-connections.jpg" caption="Connections on the Pixelblaze Output Expander" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/jbang/pixelblaze/led-strip-connections.jpg" caption="Connections for the LED strip" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Enabling Serial 

To be able to control the serial link from software, the following steps must be followed:

* In terminal: `sudo raspi-config`
* Go to "Interface Options"
* Go to "Serial Port"
* Select "No" for "login shell"
* Select "Yes" for "hardware enabled"

### Status of the Pixelblaze Output Expander LEDs

* Fading / pulsing orange: Has not seen any valid looking data.
* Solid orange (for short time): Received expander data.
* Green LED (for short time): Received data for its channels and is drawing.

## Application

Jeff Vyduna and Ben Hencke of ElectroMage, the creators of Pixelblaze, provided example Java code for this project. The serial data format is [documented on GitHub](https://github.com/simap/pixelblaze_output_expander/tree/v3.x). What the code is doing in short:

* Open serial communication to `/dev/ttyS0`.
* Use BaudRate `2000000`, this is a hard requirement for the PBOE.
* Send a byte array of RGB values for each LED.
* Send a `drawAll` command to put the values on the LEDs.
* Send other byte array and `drawAll`.
* Before the application stops, close the serial port.

### JBang configuration

As with each JBang example, we need to define the first script line and the dependencies, one in this case:

```java
///usr/bin/env jbang "$0" "$@" ; exit $?

//DEPS com.fazecast:jSerialComm:2.10.2
```

### ExpanderDataWriteAdapter

This example project doesn't use the Pi4J serial communication, as it doesn't support this baud rate (at this moment), but the `com.fazecast:jSerialComm:2.10.2` library. An inner class is used to setup the serial communication and provide a write method.

```java
static class ExpanderDataWriteAdapter {

    private SerialPort port = null;
    private final String portPath;

    public ExpanderDataWriteAdapter (String portPath) {
        this.portPath = portPath;
    }

    private void openPort() {
        if (port != null) {
            System.out.println("Closing " + portPath);
            port.closePort();
        }
        port = null; //set to null in case getCommPort throws, port will remain null.
        port = SerialPort.getCommPort(this.portPath);
        port.setBaudRate(2000000);
        port.setComPortTimeouts(SerialPort.TIMEOUT_NONBLOCKING, 0, 0);
        port.openPort(0, 8192, 8192);
        System.out.println("Opening " + portPath);
    }

    public void closePort() {
        if (port != null) {
            System.out.println("Closing " + portPath);
            port.closePort();
        }
    }

    public void write(byte[] data) {
        int lastErrorCode = port != null ? port.getLastErrorCode() : 0;
        boolean isOpen = port != null && port.isOpen();
        if (port == null || !isOpen || lastErrorCode != 0) {
            System.out.println("Port was open:" + isOpen + ", last error:" + lastErrorCode);
            openPort();
        }
        port.writeBytes(data, data.length);
    }
}
```

### Helper methods

Check the sources of the example for the full code, here the additional helper methods are listed without the full implementation:

```java
private static void sendAllOff() {
    System.out.println("All off");
    sendWs2812(0, 3, 1, 0, 2, 0, new byte[NUMBER_OF_LEDS * 3]);
    sendDrawAll();
}

private static void sendWs2812(int channel, int bytesPerPixel, int rIndex, int gIndex, int bIndex, int wIndex, byte[] pixelData) {
    ...
}

public static void sendDrawAll() {
    ...
}

private static void writeCrc(CRC32 crc) {
    ...
}

private static void packInt(byte[] outgoing, int index, int val) {
    ...
}

private static ByteBuffer initHeaderBuffer(int size, byte channel, byte command) {
    ...
}
```

### Controlling the LEDs

With all this code in place, we can start sending color data to the LED strip. The idea is to send a byte array containing a value for each color of the LEDs.

For instance, to send these colors, when using RGB-leds:

* Red for the first LED
* Green for the second LED
* Blue for the third LED
* White for the third LED

The byte array will look like this:

```java
byte[] pixeldata = new byte[12]; // 3 colors * 4 leds

// Red = 0xff0000
byte[0] = (byte) 0xff;
byte[1] = (byte) 0x00;
byte[2] = (byte) 0x00;

// Green = 0x00ff00
byte[3] = (byte) 0x00;
byte[4] = (byte) 0xff;
byte[5] = (byte) 0x00;

// blue = 0x0000ff
byte[6] = (byte) 0x00;
byte[7] = (byte) 0x00;
byte[8] = (byte) 0xff;

// White = 0xffffff
byte[9] = (byte) 0xff;
byte[10] = (byte) 0xff;
byte[11] = (byte) 0xff;
```

#### Number of colors per LED

A LED on a strip can contain three inner LEDs for RGB, or four for RGBW. In case of RGBW, you need to adapt the script to define `bytesPerPixel = 4`, and your byte array with the color values need to include four values per LED.

```java
// 3 colors per LED, White = 0xffffff
byte[0] = (byte) 0xff;
byte[1] = (byte) 0xff;
byte[2] = (byte) 0xff;

// 4 colors per LED, White = 0x000000ff
byte[0] = (byte) 0x00;
byte[1] = (byte) 0x00;
byte[2] = (byte) 0x00;
byte[3] = (byte) 0xff;
```

#### Order of the color values

Test the red, green, blue output to define how the RGB colors are ordered in the PBOE controller and/or LED strip. You can define the relation between the colors in your byte array with the actual led strip in the `sendWs2812` method, with the `int rIndex, int gIndex, int bIndex, int wIndex` parameters. If you are using RGB-leds and 3 bytes per pixel, the `wIndex` parameter is ignored.

#### Sending color values

The example code uses multiple byte arrays to define various colors and effects to a strip with 11 LEDs, connected to the channel 0 pins of the PBOE.

```java
private static final byte CH_WS2812_DATA = 1;
private static final byte CH_DRAW_ALL = 2;
private static final byte CH_APA102_DATA = 3;
private static final byte CH_APA102_CLOCK = 4;

private static final int NUMBER_OF_LEDS = 11;

private static ExpanderDataWriteAdapter adapter;

public static void main(String[] args) throws InterruptedException {
    adapter = new ExpanderDataWriteAdapter("/dev/ttyS0");

    // All off
    sendAllOff();
    Thread.sleep(500);

    // One by one red
    System.out.println("One by one red");
    for (int i = 0; i < NUMBER_OF_LEDS; i++) {
        byte[] oneRed = new byte[NUMBER_OF_LEDS * 3];
        oneRed[i * 3] = (byte) 0xff;
        sendWs2812(0, 3, 1, 0, 2, 0, oneRed);
        sendDrawAll();
        Thread.sleep(250);
    }

    // All same color red, green, blue
    for (int color = 0; color < 3; color++) {
        System.out.println("All " + (color == 0 ? "red" : (color == 1 ? "green" : "blue")));
        byte[] allSame = new byte[NUMBER_OF_LEDS * 3];
        for (int i = 0; i < NUMBER_OF_LEDS; i++) {                
            allSame[(3 * i) + color] = (byte) 0xff;
        }
        sendWs2812(0, 3, 1, 0, 2, 0, allSame);
        sendDrawAll();

        Thread.sleep(1000);
    }

    // Fill strip with random colors        
    Random rd = new Random();
    for (int i = 0; i < 5; i++) {
        System.out.println("Random colors " + (i + 1));
        byte[] random = new byte[NUMBER_OF_LEDS * 3];
        rd.nextBytes(random);
        sendWs2812(0, 3, 1, 0, 2, 0, random);
        sendDrawAll();

        Thread.sleep(1000);
    }

    // Red alert!
    try {
        byte[] red = new byte[NUMBER_OF_LEDS * 3];
        int i;
        for (i = 0; i < NUMBER_OF_LEDS; i++) {
            red[i*3]= (byte) 0xff;
        }
        for (i = 0; i < 5; i++) {
            System.out.println("All red");
            sendWs2812(0, 3, 1, 0, 2, 0, red);
            sendDrawAll();
            Thread.sleep(100);
            sendAllOff();
            Thread.sleep(100);
        }
    } catch (Exception e) {
        System.err.println("Error during random color test: " + e.getMessage());
    }

    adapter.closePort();
}
```

## Running the Application

Serial communication with the `jSerialComm` library, can be done without the need for `sudo`, so the application can be started with:

```bash
$ jbang PixelblazeOutputExpander.java
All off
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
Port was open:false, last error:0
Opening /dev/ttyS0
One by one red
ff 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
00 00 00 ff 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
... 
All red
ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 
All green
00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 
All blue
00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 
Random colors 1
1f 43 1b 3d b1 9c 46 81 ee 2f bb ba e2 a5 f5 9f af 06 27 d8 6c 04 64 68 a4 fa 31 57 14 c5 9e 7b b9 
...
All red
ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 ff 00 00 
All off
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 
... 
Closing /dev/ttyS0
```

## Conclusion

I'm still curious to see the reliability of this serial control of LED strips in combination with other loads on the Raspberry Pi, but the Pixelblaze Output Expander is a great way to easily control such strips!