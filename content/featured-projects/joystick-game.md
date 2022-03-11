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
![image by com.electronicstutorials](https://user-images.githubusercontent.com/60224159/157845938-df8508cf-00aa-4f44-b830-b815414cdd23.png)
- An analog signal is a continuously variable voltage between 0 and Vmax over time.
- A digital signal is rather a discrete step-by-step output voltage of LOW (fall) to HIGH (rise) according to the switch position among a network of resistors.
- To convert from analog signals to digial signals, we need to encode the output voltage changing over time to some sequence of bits.
- We cannot interface analog electronics on digital devices such as (arduinos and raspberry pi w/o converting into digial signals).
 
## What's ADC ?
![image](https://user-images.githubusercontent.com/60224159/157847366-3a8b0f59-363a-4316-be20-a0e60832c5b3.png)


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


