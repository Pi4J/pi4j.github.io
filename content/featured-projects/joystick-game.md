---
title: 'JMonkeyEngine with Joystick'
weight: 75
---

[Pavl G.](https://www.linkedin.com/in/pavl-g-420b81228/) created a Java Gradle library to control a car in a [JMonkeyEngine](https://jmonkeyengine.org/) game with an arduino joystick module connected to a Raspberry Pi4 model B, using GPIO digital pins and SPI interfacing through MCP3008 ADC (Analog~Digital Converter).

## Requirements : 
- Raspberry Pi with arm processor (pi3, pi4, piZero) with a working java8 (preferred).
- Female-to-male jumper wires.
- Breadboard.
- Arduino Joystick module.
- MCP3008 IC (ADC -- other adcs may work too, but we are covering only MCP3008 here).
- Some patience and time.

## Difference between Analog and Digital signals ? 
![image](https://user-images.githubusercontent.com/60224159/157847529-3b46c3e9-8d39-428c-91a1-f3018cb9f9e3.png)
- An analog signal is a continuously variable voltage between 0 and Vmax over time, examples : Temparature sensor output, Potentiometers (joysticks)....
- A digital signal is rather a discrete step-by-step output voltage of LOW (fall) to HIGH (rise) according to the switch position among a network of resistors.
- To convert from analog signals to digial signals, we need to encode the output voltage changing over time to some sequence of bits.
- We cannot interface analog electronics on digital devices such as (arduinos and raspberry pi w/o converting into digial signals).
 
## What's ADC ?

Let's have an example of a 3-bit Analogue to Digital Converter : 

![image](https://user-images.githubusercontent.com/60224159/157848094-2b43e3ba-8434-41bd-950c-d0847718ac24.png)
![image](https://user-images.githubusercontent.com/60224159/157848257-f9b3c795-bf30-4fdd-8a57-3e9259c35a1f.png)

### This how ADC works under the hood, Steps of converting Analog to Digital : 
1) Analog voltage goes through `Vin`, 
2) Then it's passed to a network of voltage comparators that compares its voltage to the selected reference range (Vref, which is selected at the time of wiring).
3) If `Vin` > `Vref` the comparator output would be HIGH aka (1), if `Vin` < `Vref` the comparator output would be LOW aka (0).
4) The significant of having a network of comparators is to encode the value of the analog signal into a digital sequence of bits.
5) The output of comparators `Dn` gets passed into a 3-bit priority encoder.
6) The priority encoder by definition, it encodes based on the **high priority input** and ignores **the low priority input**.
7) So, if `Vin = 3.5 to 4.0 V` then the `Comparators output = 11111111`, 
8) At last when inputting the comparator output into the priority encoder the encoder gives a value of 7 which points to D7 of comparator U7 aka the last voltage level, and that's true because our Vin is bigger than the Vref<max>.

## What's SPI ? 
![image](https://user-images.githubusercontent.com/60224159/157852097-4800a22c-c81b-4a1b-ba2b-2d1ab2b1652b.png)
- Serial Peripheral Interface (SPI) is an interface bus commonly used to send data between microcontrollers and small peripherals such as shift registers, sensors, and SD cards. It uses separate clock and data lines, along with a select line to choose the device you wish to talk to.
- Our target is to transfer the output from our priority encoder to the BCM processor of our Pi throughout the SPI protocol (Synchronously over Tx from MCP3008 to Rx of the Pi).
- To send and receive synchronous data we use `MISO` (the same as CIPO) for receving data from peripherals and `MOSI` (the same as COPI) to send data to the peripherals.
- MISO : Master-in-Slave-Out = CIPO : Controller-in-peripheral-out.
- MOSI : Master-out-Slave-In = COPI : Controller-out-Peripheral-in.
- MCP3008 is used to receive analog input, so MISO or CIPO is our common active data line.
- CS is the chip select, it's used to select which peripheral device to use.
- SCLK is the serial clock and it's used to synchronize data on a data line, to have a clear separate message per 8 clocks (8-bit message).

## Wiring Up :
![Pi4j Joystick_bb](https://user-images.githubusercontent.com/60224159/157844859-34b0373b-09e2-488e-af82-d993a2d48719.png)

Vcc : is used for powering up the IC and not to compare with VREF.
Vref : is used for controlling the maximum resolution of the input voltage (analog signal), if VREF = 5v5 (maximum voltage received by MCP3008), then the resolution of Vin is a 100%.
 
## Testing the wiring : 
Before going deeper and testing with jme vehicle, please test this code and do your conclusions : 
```java
// Define MCP3008 provider on CS0 -- Peripheral device 0
final MCP3008GpioProvider mcp3008GpioProvider = new MCP3008GpioProvider(SpiChannel.CS0);
// define analog input pins on the adc
final GpioPinAnalogInput[] gpioPinAnalogInput= new GpioPinAnalogInput[2];
gpioPinAnalogInput[0] = MCP3008Pin.CH0;
gpioPinAnalogInput[1] = MCP3008Pin.CH1;
// define the threshold analog (the minimum voltage at which the Pi can listen to).
mcp3008GpioProvider.setEventThreshold(thresholdAnalogValue, gpioPinAnalogInput);
// enable monitoring of analog values with an interval of 250 ms
mcp3008GpioProvider.setMonitorEnabled(true);
mcp3008GpioProvider.setMonitorInterval(250);
// start collecting data from the SPi connected to MCP3008 output.
final GpioController gpioController = GpioFactory.getInstance();
gpioController.addListener((GpioPinListenerAnalog) event -> {
    System.out.println("Value at CH0 : " + mcp3008GpioProvider.getValue(gpioPinAnalogInput[0]));
    System.out.println("Value at CH1 : " + mcp3008GpioProvider.getValue(gpioPinAnalogInput[1]));
}, gpioPinAnalogInput);
```

## Testing with a jmonkeyengine vehicle : 
It's very hard to give you a full overview of how to create a jmonkeyengine vehicle in this tutorial, so you could fairly refer to jme docs and examples for more : 
- Use the physics in your game and control your game via keyboard : https://wiki.jmonkeyengine.org/docs/3.4/tutorials/beginner/hello_physics.html
- A Keyboard controlled car demo : https://github.com/jMonkeyEngine/jmonkeyengine/blob/master/jme3-examples/src/main/java/jme3test/bullet/TestPhysicsCar.java
- The idea is simple, any game can be controlled using a keyboard interface (bound to jme update), so you can simply replace that with a custom `InputHandler` using a custom hardware. 
- The trick is to bind your joystick pi4j interface to jme thread (OpenGL's thread).
 
## Video of operation : 

{{< youtube 9ZvhFQSwHF0 >}}

## More at sources :
- ADC overview : https://www.electronics-tutorials.ws/combination/analogue-to-digital-converter.html
- MCP3008 ADC : https://www.microchip.com/en-us/product/MCP3008
- SPI overview : https://learn.sparkfun.com/tutorials/serial-peripheral-interface-spi/all
- Gradle lib : https://github.com/Scrappers-glitch/JoyStickModule
- Testcase : https://github.com/Scrappers-glitch/JmeCarPhysicsTestRPI


