---
title: Electrical Engineering
weight: 40
aliases:
  - /getting-started/electricalengeneering/
---

The goal of the Pi4J project is to combine sofware (Java) with hardware (electronic components). On this page we give you some tips and tricks for the electronics part.

## Breadboard

A breadboard is the basic for each experiment. It allows you to easily connect several components to each other and the Raspberry Pi. Here is a video that explains the basics of breadboards:

{{< youtube 6WReFkfrUIk >}}

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/breadboard.jpeg" caption="Breadboard" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

{{% notice note %}}
The red and blue lines on the side show which pins are connected. Be aware that red and blue can also be swapped, because not all suppliers use them in the same position.<br>
On some boards these lines are interrupted in the middle (see picture breadboard).
This means at this point, the pins are interrupted and not electrically connected.
{{% /notice %}}

## Resistor Dimensioning

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

### Voltage Divider

If components have a lower operating voltage than the 3.3V of the Raspberry Pi, a voltage divider can be used to achieve the desired voltage.
For example, a red LED has an operating voltage of 1.8V. This means that 1.5V must drop across a second load. If we assume that the LED needs 20mA of current, this means that we should connect a resistor of 75 Ohm in series to the LED.

If the required current and the required voltage of the load are known, the exact required resistance can be calculated [here](https://ledcalculator.net/). 

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/voltageDivider.png" caption="Voltage Divider Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/voltageDividerCircuit.png" caption="Voltage Divider electrical drawing" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### 3.3V <--> 5V Level Shifter

To protect the Pi from 5V devices, a level shift/conversion can be done with the "Adafruit TXB0104 Bi-Directional Level Shifter" component. The bi-directional level shifter works for an I2C bus, 
for a TTL serial connection, for a slow <2MHz SPI connection and any other digital interface both uni- and bidirectional. 

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/TXB0104logicLevelConverter.jpeg" caption="Logic Level Converter" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Additional Power Supply

If one or more large loads are required for the project, it may be necessary to use an additional power supply. A solution for this is the Mini Power Supply Module 
HW-131 Breadboard Power Module which provides two voltages 3.3V and 5V and a maximum output current of 700mA.

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/miniPowerSupplyModule.jpeg" caption="Mini Power Supply Module" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/miniPowerSupplyModuleFrontBack.jpeg" caption="Mini Power Supply Module Front Back" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

{{% notice warning %}}
Do not use the USB port of the computer to power the electronics. Errors in the wiring can destroy the USB port of the computer.
{{% /notice %}}

{{% notice note %}}
In case of an additional power supply, the ground of the Raspberry Pi and the ground of the power supply must be connected to each other.
{{% /notice %}}

## Soldering Tutorial

A video that explains the basics of soldering:

{{< youtube Qps9woUGkvI >}}

A video that explains how to remove solder:

{{< youtube bG7yW9FigJA >}}

{{% notice note %}}
If a breakout with two pin headers like the TXB0104 is used, the pin headers can be mounted on the breadboard first, then the breakout is placed on the pin headers and finally 
everything can be soldered. So the pin headers are mounted exactly in 90° angle to the breakout and can be mounted on the breadboard without any problem.
{{% /notice %}}

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/solderingTwoPins1.png" caption="Soldering Two Pins Part 1" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/solderingTwoPins2.png" caption="Soldering Two Pins Part 2" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Automatic Wire Stripper

A video that explains how the automatic wire stripper works:

{{< youtube dvFS_ZEzwKg >}}

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/automaticWireStripper.png" caption="Automatic Wire Stripper" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Crimping Tutorial

A video that explains the basics of crimping wires:

{{< youtube WFvEeWHDt1E >}}

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimping.png" caption="Crimping Tool" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

{{% notice note %}}
If the crimp connection does not hold, the following measures can lead to a better connection:
<br> - Strip wire to double length, lay on top of each other and twist (see picture below)
<br> - The crimping tool is too short, crimp the sleeve twice in different places (see picture below)
{{% /notice %}}

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/stripDoubleLength.png" caption="Strip double length" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimpingStep1.png" caption="Crimping step 1" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimpingStep2.png" caption="Crimping step 2" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimpingStep3.png" caption="Crimping step 3" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimpingStep4.png" caption="Crimping step 4" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Crimping Ferrules Tutorial

A video that explains the basics of crimping ferrules to wires:

{{< youtube bJk0mzaATI4 >}}

{{< gallery >}}
{{< figure link="/assets/getting-started/electricalEngineering/crimpingFerrules.png" caption="Crimping Ferrules Tool" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}


