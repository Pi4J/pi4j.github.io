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

## What's SPI ? 

## Wiring Up :
![Pi4j Joystick_bb](https://user-images.githubusercontent.com/60224159/157844859-34b0373b-09e2-488e-af82-d993a2d48719.png)

## Testing the wiring : 
Before going deeper and testing with jme vehicle, please test this code and do your conclusions : 
```java
```

## Testing with a jmonkeyengine vehicle : 

## Video of operation : 

{{< youtube 9ZvhFQSwHF0 >}}

## More at sources :
- Gradle lib : https://github.com/Scrappers-glitch/JoyStickModule
- Testcase : https://github.com/Scrappers-glitch/JmeCarPhysicsTestRPI


