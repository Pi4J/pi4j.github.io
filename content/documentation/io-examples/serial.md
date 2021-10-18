---
title: Serial (UART/RS232)
weight: 250
tags: ["Serial"]
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-example-serial/](https://github.com/Pi4J/pi4j-example-serial/)
{{% /notice %}}

## What is it?

Serial communication can be used to transfer data between different boards, devices, etc. Data is transfered bit-by-bit
in a sequence, through a single wire from a transmitter (= TX) to a receiver (= RX). On the receiver side the bits are
combined to bytes.

When you need two-way communication, two wires are needed between RX and TX from both sides:

![Two-way serial communication](/assets/documentation/serial-two-devices.jpg)

The communication between these two devices can happen in different ways:

* simplex: one direction only without a message back to confirm the receiving
* half-duplex: devices can only send or receive at once
* full-duplex: both devices can send and receive at the same time

Serial communication is done at a predefined speed which needs to be known on both sides, as both the sender and receiver 
need to handle the data at the same speed. This speed is called the "baud rate" with a value indicating the number of 
bits per second (bps). The most used speed is 9600 bps, but you can use lower (1200, 2400, 4800) or 
higher (19200, 38400, 57600, 115200) speeds, depending on the speed which can be handled reliably by the device.

The Pi has two built-in connections to GPIOs BCM number 14 (TX) and 15 (RX). Identical to the other GPIOs, they use 
3.3V so make sure, when you connect other devices, the same voltage is used.

## Code example

The following example demonstrates how you can connect to a GPS module to read the data. This example is based on an 
example from the book ["The Definitive Guide to Modern Java Clients with JavaFX" by Stephen Chin, Johan Vos and James Weaver](https://www.apress.com/gp/book/9781484249253).
That example uses V1 of Pi4J with a listener provided by the library. In V2 this listener is no longer provided but can 
easily be achieved with a Thread to handle the incoming data.

### Wiring

The GPS module used in this example: NEO-7M.

| NEO-7M    | Raspberry Pi            |
| :---      | :---                    |
| VCC       | Power 5V (e.g. pin 2)   |
| GND       | Ground (e.g. pin 6)     |
| RX        | UART TX, GPIO 15        |
| TX        | UART RX, GPIO 16        |

In the readme of the coding example, you can find the description how you can test the GPS module in the terminal 
with `gpsd.socket`.

### Initialize the serial port

First Pi4J needs to be initialized. Within this context we can then configure and open the serial port. As long as the
serial port is open, we run a thread to handle the incoming data.

``` java
var console = new Console();
var pi4j = Pi4J.newAutoContext();

var serial = pi4j.create(Serial.newConfigBuilder(pi4j)
        .use_9600_N81()
        .dataBits_8()
        .parity(Parity.NONE)
        .stopBits(StopBits._1)
        .flowControl(FlowControl.NONE)
        .id("my-serial")
        .device(SERIAL_ADDRESS)
        .provider("pigpio-serial")
        .build());
serial.open();

// Wait till the serial port is open
console.print("Waiting till serial port is open");
while (!serial.isOpen()) {
    Thread.sleep(250);
}

// Start a thread to handle the incoming data from the serial port
SerialReader serialReader = new SerialReader(console, serial);
Thread serialReaderThread = new Thread(serialReader, "SerialReader");
serialReaderThread.setDaemon(true);
serialReaderThread.start();

while (serial.isOpen()) {
    Thread.sleep(500);
}

serialReader.stopReading();
```

### Serial reader

The reader itself implements a Runnable and waits till data is available from the serial port. As the GPS module sends
its data as readable String lines seperated by a line separator, we only need to handle the bytes which are higher than 
32 (see the [ASCII code table](https://en.wikipedia.org/wiki/ASCII#Printable_characters)). All lower values are handled
as line separators.

``` java
public class SerialReader implements Runnable {

    private final Console console;
    private final Serial serial;

    private boolean continueReading = true;

    public SerialReader(Console console, Serial serial) {
        this.console = console;
        this.serial = serial;
    }

    public void stopReading() {
        continueReading = false;
    }

    @Override
    public void run() {
        // We use a buffered reader to handle the data received from the serial port
        BufferedReader br = new BufferedReader(new InputStreamReader(serial.getInputStream()));

        try {
            // Data from the GPS is recieved in lines
            String line = "";

            // Read data until the flag is false
            while (continueReading) {
                // First we need to check if there is data available to read.
                // The read() command for pigio-serial is a NON-BLOCKING call, 
                // in contrast to typical java input streams.
                var available = serial.available();
                if (available > 0) {
                    for (int i = 0; i < available; i++) {
                        byte b = (byte) br.read();
                        if (b < 32) {
                            // All non-string bytes are handled as line breaks
                            if (!line.isEmpty()) {
                                // Here we should add code to parse the data to a GPS data object
                                console.println("Data: '" + line + "'");
                                line = "";
                            }
                        } else {
                            line += (char) b;
                        }
                    } 
                } else {
                    Thread.sleep(10);
                }
            }
        } catch (Exception e) {
            console.println("Error reading data from serial: " + e.getMessage());
            System.out.println(e.getStackTrace());
        }
    }
}
```

### Running the application on Raspberry Pi

You can get the full working example from GitHub and run on a Raspberry Pi after you correctly connected a GPS module. 
As you can see in the output, each data line (starting with `$GP...`) is logged.

``` shell
$ git clone https://github.com/Pi4J/pi4j-example-serial.git
$ cd https://github.com/Pi4J/pi4j-example-serial.git
$ mvn package
$ cd target/distribution
$ sudo ./run.sh

[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console -                   <-- The Pi4J Project -->                  
[main] INFO com.pi4j.util.Console -                    Serial Example project                   
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - ************************************************************
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.Pi4J - New auto context
[main] INFO com.pi4j.Pi4J - New context builder
[main] INFO com.pi4j.platform.impl.DefaultRuntimePlatforms - adding platform to managed platform map [id=raspberrypi; name=RaspberryPi Platform; priority=5; class=com.pi4j.plugin.raspberrypi.platform.RaspberryPiPlatform]
...
[main] INFO com.pi4j.util.Console - Waiting till serial port is open
[main] INFO com.pi4j.util.Console - 
[main] INFO com.pi4j.util.Console - Serial port is open
...
[SerialReader] INFO com.pi4j.util.Console - Data: '$GPVTG,,T,,M,2.349,N,4.351,K,A*2C'
[SerialReader] INFO com.pi4j.util.Console - Data: '$GPGGA,143723.00,5054.02265,N,00301.10531,E,1,04,10.46,86.2,M,45.9,M,,*5C'
[SerialReader] INFO com.pi4j.util.Console - Data: '$GPGSA,A,3,09,16,05,07,,,,,,,,,17.19,10.46,13.64*33'
[SerialReader] INFO com.pi4j.util.Console - Data: '$GPGSV,2,1,06,05,33,304,20,07,67,101,21,09,39,079,29,11,38,228,20*7E'
[SerialReader] INFO com.pi4j.util.Console - Data: '$GPGSV,2,2,06,16,11,030,24,20,63,283,*73'
[SerialReader] INFO com.pi4j.util.Console - Data: '$GPGLL,5054.02265,N,00301.10531,E,143723.00,A,A*6A'
```