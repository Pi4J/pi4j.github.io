---
title: Electrical Engineering
weight: 40
---

## Resistor dimensioning

Resistors can be used for different effects. One application is to improve the stability of the application with PullUp and PullDown resistors. Another application is to use resistors to protect the PI against voltage peaks or short circuit currents.


### PullUp PullDown
In electronic logic circuits, a pull-up resistor or pull-down resistor is a resistor used to ensure a known state for a signal. It is typically used in combination with components
such as switches and transistors, which physically interrupt the connection of subsequent components to ground or to VCC. Closing the switch creates a direct connection to ground or VCC,
but when the switch is open, the rest of the circuit would be left floating (i.e., it would have an indeterminate voltage).

For a switch that is used to connect a circuit to VCC (e.g., if the switch or button is used to transmit a "high" signal), a pull-down resistor connected between the circuit and ground 
ensures a well-defined ground voltage (i.e. logical low) across the remainder of the circuit when the switch is open. For a switch that is used to connect a circuit to ground, a pull-up 
resistor (connected between the circuit and VCC) ensures a well-defined voltage (i.e. VCC, or logical high) when the switch is open. 

The size of the resistor can vary between 1kOhm and 100kOhm. Here it is necessary to weigh what is useful for the application. The closer the resistor is to 0, the stronger the level is defined, but the greater the current 
consumption in the open state. The higher the resistance, the less current is consumed in the off state, but the more unstable the signal becomes. For a start value PullUp and PullDown resistors with 10kOhm are to be used.

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/pullUpPullDown.png" caption="PullUp Pull Down Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/pullUpCircuit.png" caption="PullUp electrical drawing" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/pullDownCircuit.png" caption="PullDown electrical drawing" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}


### Voltage divider
If components have a lower operating voltage than the 3.3V of the Raspberry Pi, a voltage divider can be used to achieve the desired voltage.
For example, a red LED has an operating voltage of 1.8V. This means that 1.5V must drop across a second load. If we assume that the LED needs 20mA of current, this means that we should connect a resistor of 75 Ohm in series to the LED.

If the required current and the required voltage of the load are known, the exact required resistance can be calculated [here](https://ledcalculator.net/). 

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/voltageDivider.png" caption="Voltage Divider Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/voltageDividerCircuit.png" caption="Voltage Divider electrical drawing" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### 3.3V <--> 5V level shifter
To protect the Pi from 5V devices, a level shift/conversion can be done with the "Adafruit TXB0104 Bi-Directional Level Shifter" component. The bi-directional level shifter works for an I2C bus, 
for a TTL serial connection, for a slow <2MHz SPI connection and any other digital interface both uni- and bidirectional. 

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/TXB0104logicLevelConverter.jpeg" caption="Logic Level Converter" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}


## Additional power supply
If one or more large loads are required for the project, it may be necessary to use an additional power supply. A solution for this is the Mini Power Supply Module 
HW-131 Breadboard Power Module which provides two voltages 3.3V and 5V and a maximum output current of 700mA.

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/miniPowerSupplyModule.jpeg" caption="Mini Power Supply Module" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/miniPowerSupplyModuleFrontBack.jpeg" caption="Mini Power Supply Module Front Back" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

{{% notice note %}}
In case of an additional power supply, the ground of the Raspberry Pi and the ground of the power supply must be connected to each other.
{{% /notice %}}

{{% notice note %}}
Do not use the USB port of the computer to power the electronics. Errors in the wiring can destroy the USB port of the computer.
{{% /notice %}}

## Soldering tutorial
[Here](https://www.youtube.com/watch?v=Qps9woUGkvI) is a short video that explains the basics of soldering. 

[Here](https://www.youtube.com/watch?v=bG7yW9FigJA) is a short video that explains how to remove solder. 

{{% notice note %}}
If a breakout with two pin headers like the TXB0104 is used, the pin headers can be mounted on the breadboard first, then the breakout is placed on the pin headers and finally 
everything can be soldered. So the pin headers are mounted exactly in 90° angle to the breakout and can be mounted on the breadboard without any problem.
{{% /notice %}}

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/solderingTwoPins1.png" caption="Soldering Two Pins Part 1" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/solderingTwoPins2.png" caption="Soldering Two Pins Part 2" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Automatic wire stripper
[Here](https://www.youtube.com/watch?v=dvFS_ZEzwKg) is a short video that explains how the automatic wire stripper works.

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/automaticWireStripper.png" caption="Automatic Wire Stripper" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Crimping tutorial
[Here](https://www.youtube.com/watch?v=WFvEeWHDt1E) is a short video that explains the basics of crimping wires. 

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimping.png" caption="Crimping Tool" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}


## Crimping ferrules tutorial
[Here](https://www.youtube.com/watch?v=bJk0mzaATI4) is a short video that explains the basics of crimping ferrules to wires. 

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimpingFerrules.png" caption="Crimping Ferrules Tool" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}


