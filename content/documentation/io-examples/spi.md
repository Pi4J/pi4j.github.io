---
title: Serial Peripheral Interface (SPI)
weight: 240
tags: ["SPI", "MAX7219"]
---

## What is it?

The Serial Peripheral Interface, abbreviated to SPI, is a bus system which enables 
communication between a main device (called “master”) and one or more secondary devices 
(called “slave”). A direct communication between all participants is not possible here, 
much more the master can choose at any time with which slave he would like to exchange data.

In order to address only one slave, a total of 3 signal lines are required, two of which 
are used for bidirectional data transmission and one as a clock generator for serial 
transmission. If further slaves are to be addressed, additional signal lines are required 
depending on the desired topology.

## Uses

In addition to communication between microcontrollers, SPI is also used to address 
numerous sensors and actuators. Similar to I²C, a large number of control commands and 
data can be transmitted in both directions with a relatively high clock rate over 3 lines. 
A particular advantage here is the support for “full duplex”, ie the simultaneous 
transmission of data in both directions.

The technical implementation is very simple and is also used, for example, to communicate 
with SD cards. The Nintendo Game Boy already used this protocol to connect several game 
consoles via the Game Boy Link Cable.

## Addressing

As already mentioned in the first section, multiple slaves can also be connected to SPI. 
The number available depends on the hardware used. On the Raspberry Pi, the standard SPI0
with two different slaves use what is called Chip Select Pins is controlled.

Command line to list interfaces:
```
root@rp5:~# ls -l /dev/*spi*
ls: cannot access '/dev/*spi*': No such file or directory
root@rp5:~# 
```

If none show up:
```
root@rp5:~# raspi-config
    Interface Options
        SPI
            Would you like the SPI interface to be enabled?
            Yes
```

```
root@rp5:~# ls -l /dev/*spi*
crw-rw---- 1 root spi 153, 0 Sep 11 09:58 /dev/spidev0.0
root@rp5:~#
```

Here is 1 interface that can be accessed 2 ways:
```
/dev/spidev0.0 drives CE0 Low
/dev/spidev0.1 drives CE1 Low
```


## Additional Information

- [Wikipedia SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface)
- [SPI pinout for Raspberry Pi](https://pinout.xyz/pinout/spi#)

## Code example 

Initialize the Pi4J Context with a provider which supports SPI fully, e.g. the PiGpioSpiProvider. The minimal example 
would be:

```java
var piGpio = PiGpio.newNativeInstance();
var pi4j = Pi4J.newContextBuilder()
    .noAutoDetect()
    .add(
        PiGpioSpiProvider.newInstance(piGpio)
    )
    .build();
```

Depending on the type of GPIOs you need in your project this could be further extended to e.g.:

```java
var piGpio = PiGpio.newNativeInstance();
var pi4j = Pi4J.newContextBuilder()
    .noAutoDetect()
    .add(
        PiGpioDigitalInputProvider.newInstance(piGpio),
        PiGpioDigitalOutputProvider.newInstance(piGpio),
        PiGpioPwmProvider.newInstance(piGpio),
        PiGpioI2CProvider.newInstance(piGpio),
        PiGpioSerialProvider.newInstance(piGpio),
        PiGpioSpiProvider.newInstance(piGpio)
    )
    .build();
```

The following example is an extract of the [CrowPi example project](/getting-started/crowpi/) which includes
a component to control an 8x8 LED matrix display with an MAX7219 driver chip which is controlled via SPI.

```java
public class MAX7219 extends Component {
    // MAX7219: Internal Commands
    private static final byte CMD_SET_FIRST_ROW = 0x01;
    private static final byte CMD_DECODE_MODE = 0x09;
    private static final byte CMD_INTENSITY = 0x0A;
    private static final byte CMD_SCAN_LIMIT = 0x0B;
    private static final byte CMD_SHUTDOWN = 0x0C;
    private static final byte CMD_DISPLAY_TEST = 0x0F;

    /**
     * Width of MAX7219 LED matrix
     */
    public static final int WIDTH = 8;

    /**
     * Height of MAX7219 LED matrix
     */
    public static final int HEIGHT = 8;

    /**
     * Internal buffer to store the 8x8 matrix
     * A byte[] array is used as each of the 8 bits is used to represent a column
     */
    protected final byte[] buffer = new byte[HEIGHT];

    /**
     * Pi4J SPI instance
     */
    protected final Spi spi;

    /**
     * Creates a new MAX7219 instance using the given SPI instance from Pi4J.
     *
     * @param spi SPI instance
     */
    public MAX7219(Spi spi) {
        this.spi = spi;
    }

    /**
     * Clears the internal buffer without refreshing the display.
     * This means that the current contents of the displays are still being shown until {@link #refresh()} is called.
     */
    public void clear() {
        Arrays.fill(buffer, (byte) 0);
    }

    /**
     * Flushes the internal buffer for all rows to the chip, causing it to be displayed.
     * The contents of the buffer will be preserved by this command.
     */
    public void refresh() {
        for (int row = 0; row < HEIGHT; row++) {
            refreshRow(row);
        }
    }

    /**
     * Flushes the internal buffer for a single row to the chip, causing it to be displayed.
     * The contents of the buffer will be preserved by this command.
     *
     * @param row Row to be flushed
     */
    protected void refreshRow(int row) {
        if (row < 0 || row >= HEIGHT) {
            throw new IllegalArgumentException("Row must be an integer in the range 0-" + HEIGHT);
        }

        execute((byte) (CMD_SET_FIRST_ROW + row), buffer[row]);
    }

    /**
     * Specifies if the LED matrix should be enabled or disabled.
     * This will also setup the proper decoding mode and scan limit when enabling the chip.
     *
     * @param enabled LED matrix state (true = ON, false = OFF)
     */
    public void setEnabled(boolean enabled) {
        if (enabled) {
            execute(CMD_SHUTDOWN, (byte) 0x01);
            execute(CMD_DECODE_MODE, (byte) 0x00);
            execute(CMD_SCAN_LIMIT, (byte) 0x07);
        } else {
            execute(CMD_SHUTDOWN, (byte) 0x00);
        }
    }

    /**
     * Enables or disables the testing mode of the LED matrix.
     * When enabled, all other options (including {@link #setEnabled(boolean)} are ignored and all LEDs are turned on.
     * To actually control the chip, the test mode MUST be disabled.
     *
     * @param enabled Test mode state (true = ON, false = OFF)
     */
    public void setTestMode(boolean enabled) {
        execute(CMD_DISPLAY_TEST, (byte) (enabled ? 0x01 : 0x00));
    }

    /**
     * Changes the desired brightness for the LED matrix.
     * This method expects an integer value within the range 0-15, with 0 being the dimmest and 15 the brightest possible value.
     * The whole display is affected by this command which gets immediately applied.
     *
     * @param brightness Desired brightness from 0-15
     */
    public void setBrightness(int brightness) {
        if (brightness < 0 || brightness > 15) {
            throw new IllegalArgumentException("Brightness must be an integer in the range 0-15");
        }
        execute(CMD_INTENSITY, (byte) brightness);
    }

    /**
     * Enables or disables the pixel at the given X/Y position within the internal buffer.
     * This change will not be visible until {@link #refresh()} or {@link #refreshRow(int)} gets called.
     *
     * @param x       X position to change
     * @param y       Y position to change
     * @param enabled Desired pixel state (true = ON, false = OFF)
     */
    public void setPixel(int x, int y, boolean enabled) {
        // Ensure coordinates are within boundaries
        checkPixelBounds(x, y);

        // Generate bitmask and set/unset specific bit
        final byte mask = (byte) (1 << (WIDTH - 1 - x));
        if (enabled) {
            buffer[y] |= mask;
        } else {
            buffer[y] &= ~mask;
        }
    }

    /**
     * Retrieves the pixel at the given X/Y position within the internal buffer.
     *
     * @param x X position to change
     * @param y Y position to change
     * @return Current state of specified pixel (true = ON, false = OFF)
     */
    public boolean getPixel(int x, int y) {
        // Ensure coordinates are within boundaries
        checkPixelBounds(x, y);

        // Generate bitmask and retrieve specific bit
        final byte mask = (byte) (1 << (WIDTH - 1 - x));
        return (buffer[y] & mask) != 0;
    }

    /**
     * Ensures the given X and Y coordinates are within the boundaries of this LED matrix.
     * An {@link IllegalArgumentException} will be thrown if outside.
     *
     * @param x X coordinate to check
     * @param y Y coordinate to check
     */
    private void checkPixelBounds(int x, int y) {
        if (x < 0 || x >= WIDTH) {
            throw new IllegalArgumentException("X must be an integer in the range 0-" + WIDTH);
        }
        if (y < 0 || y >= WIDTH) {
            throw new IllegalArgumentException("Y must be an integer in the range 0-" + HEIGHT);
        }
    }

    /**
     * Helper method for sending a command to the MAX7219 chip with data. Communication happens over SPI by simply sending two pieces of
     * data, more specifically the desired command as a byte value, followed by the data as another byte value.
     *
     * @param command Command to be executed
     * @param data    Data for the given command
     */
    private void execute(byte command, byte data) {
        spi.write(command, data);
    }
}
```
