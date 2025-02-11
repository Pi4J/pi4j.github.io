---
title: Hardware testing
weight: 50
---

{{% notice warning %}}This is an experimental project which will need a lot of love... The new Raspberry 
Pi Pico with a lot of GPIOs for a very low price, seems even to be a better fit for this project compared to the
Arduino Due... To be further investigated!{{% /notice %}}

To minimize the required time and efforts to test a new release, V2+ aims to include an automated test which performs 
I/O testing on each I/O interface on each model of RPi. Ideally this would happen as part of the unit testing sequence 
for each code commit or at least as part of the release cycle.  

To achieve this, an Arduino Due board with lots of on board I/O capability is being used. The 
[firmware that gets loaded onto the Arduino board](https://github.com/Pi4J/pi4j/tree/master/pi4j-test-harness/src/main/arduino) 
listens on the serial port for instructions on which pins to use and what type of test to perform. The 
"Test Harness" project also includes a [Java library that is used to communicate with the Arduino and instrument tests](https://github.com/Pi4J/pi4j/tree/master/pi4j-test-harness/src/main/java).

Next, a given [I/O provider plugin](https://github.com/Pi4J/pi4j/tree/master/plugins/pi4j-plugin-pigpio/src/test/java/com/pi4j/plugin/pigpio/test) 
includes test classes that instrument the test harness and perform live I/O testing between the SBC (or other hardware) 
and the Arduino Test Harness.

To be able to fully test all board types, a custom PCB needs to be created to perform all the interconnects between 
the Raspberry Pi 26-pin/40-pin headers, and the Arduino board. This way enough test harnesses could be build for each 
Raspberry Pi model and have a permanent setup for on-demand testing. This of course is a huge effort just by itself, 
and perhaps too ambitious -- but seeking a means to reach automated testing is really needed for the long term.

![](/assets/architecture/hardware-testing.jpg)