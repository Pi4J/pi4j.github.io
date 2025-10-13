---
title: 1-Wire
weight: 270
tags: ["1-Wire"]
aliases:
  - /documentation/io-examples/1-wire/
---

## What is it?

Based on [Wikipedia](https://en.wikipedia.org/wiki/1-Wire): 

_1-Wire is a wired half-duplex serial bus that provides low-speed (16.3 kbit/s) data communication and supply voltage over a single conductor. It's similar in concept to I2C, but with lower data rates and longer range. It is typically used to communicate with small inexpensive devices such as digital thermometers and weather instruments._

## Receive Data

At this moment, 1-Wire is not supported by Pi4J, but there is work-in-progress, see [draft pull request #435](https://github.com/Pi4J/pi4j/pull/435/files).

A possible code-only approach is reading the kernel's relevant sys files, for example:

```java
String devicePath = "/sys/bus/w1/devices/28-0316a2791cff/w1_slave";
try (BufferedReader br = new BufferedReader(new FileReader(devicePath))) {
    String line1 = br.readLine();  // e.g. "00 00 00 00 00 ... : crc=00 YES"
    String line2 = br.readLine();  // e.g. "00 00 00 00 00 t=12345"

    // Typically you look for "t=NNNNN" to get the temperature
    // Here, parse the integer after "t="
    String tempStr = line2.split("t=")[1];
    double tempC = Double.parseDouble(tempStr) / 1000.0;
    System.out.println("Temperature: " + tempC + "°C");
} catch (IOException e) {
    e.printStackTrace();
}
```