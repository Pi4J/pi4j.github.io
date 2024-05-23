---
title: 'Binary Clock'
weight: 54
---

{{% notice tip %}}
GITHUB PROJECT: [github.com/taartspi/pi4j-binary-clock](https://github.com/taartspi/pi4j-binary-clock)
{{% /notice %}}

This project by Tom Aarts (published on May 15, 2024), is a binary clock created with LEDs on a breadboard. In the video below you see it incrementing to the next minute and hour.  What you see is the Hour Minute and Second displayed in BCD (Binary Coded Decimal):

<video controls width="800">
  <source src="/assets/featured-projects/binaryclock/binaryclock.mp4" />
</video>


Design document describing the LED  PCF8575 connections, and the Java implementation that drives the clock LEDs.
Note: there are two PCF8575 IC used in this design.  This IC is used as it can provide the current flow to
directly control the LED.   Alternative IC like the MCP23017 with less current capability would require a NPN
transistor in the circuit.

# Wiring

The following documents the connections for a single LED

![Single LED wiring](/assets/featured-projects/binaryclock/led_connections.png)

## LED Anode/Cathode

![Diode](/assets/featured-projects/binaryclock/diode.png)

## LED assignment
Chart of 20 LED showing color assignment.
![LED colors](/assets/featured-projects/binaryclock/led_colors.png)

## Overall LED connections
Higher level example of the twenty LED connections. This shows half of the LEDs. the same connection pattern
repeats.

![LED connections](/assets/featured-projects/binaryclock/led_connections_within_BreadBoard.png)

![LED connections across entire BreadBoard](/assets/featured-projects/binaryclock/led_connections_across_breadboard.png)


# Parts

## AITIAO  PCF8575  16 IO Expander
Since there are 20 LEDs, two ICs are required. In my case these parts I purchased do not match their documentation.  My chip has solder bridges for all three address bits, A0 A1 A2.  Also their description of a solder bridge across VCC-VDD appears to be backwards.  I think as  cautionary tale, I soldered the ICs down and lost access to their VCC-VDD bridge and couldn’t experiment.   
This companies chip functions correctly with the Chip VCC and LED anode voltage equal.

## LEDs
Cheapos.

## Prototype board
Half Size BreadBoard.  You can see in the chart ‘Overall LED Connections’ I cut paths on the planar so the LEDs
could be placed close to each other.  You can buy larger BreadBoards from ElectroCookie, called snappable.
On these boards each row, ie: A B C …  has three solder lands and each letters trace are not connected to the
next letter, so no trace cutting and there is more area for components and soldering.

![Alternate BreadBoard](/assets/featured-projects/binaryclock/alternate_breadboard.jpg)

# PCF8575  Connection Assignment

![PCF8575 pin assignment](/assets/featured-projects/binaryclock/pcf8575_pin_assignment.png)

# Pi Connectins

The PCF8575 ICs and the Diode anodes connect to the Pi 3.3v
The PCF8575 ICs connect to the Pi Ground.
The PCF8575 ICs connect to the Pi SDA and SCL (I2C).
 
# Java Implementation

The Java project uses Pi4J V2.6.0 and you can find the sources in this [GitHub repository](https://github.com/taartspi/pi4j-binary-clock)

Developed using pi4j 2.6.0-SNAPSHOT.


# Completed project

{{< gallery >}}
{{< figure link="/assets/featured-projects/binaryclock/pcf8575_breadboard.jpg" caption="PCF8575 BreadBoard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/binaryclock/led_breadboard.jpg" caption="LED BreadBoard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/binaryclock/interconnect_pcf8575.jpg" caption="PCF 8575 wired" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/binaryclock/interconnect.jpg" caption="Interconnect" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/binaryclock/led_breadboard_operational.jpg" caption="Operational" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

# Alternate IC

You could use a MCP23008 or MCP23017 as the IC. There are a few more steps to configure the IC, and its limited current capability requires a NPN transistor to switch the LED current.

![NPN Transistor for MCP230XX](/assets/featured-projects/binaryclock/npn_transistor.png)

