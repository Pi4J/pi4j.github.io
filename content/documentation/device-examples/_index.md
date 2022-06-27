---
title: Devices examples
weight: 130
---

The core Pi4J V.2 library doesn't contain any specific support for devices like buttons, motors, LCD... This was part of 
V.1 but made it much more difficult to maintain and fully test the library.

On this page we want to keep a list of projects which contain implementation code for specific devices using the Pi4J 
V.2 core library. Please let us know through [the forum](https://forum.pi4j.com) if you want to have your project added 
to this list.

### Current available device support projects

| Device(s)                     | Developed by          | Link              |
| :---                          | :---                  | :---              |
| MCP230008, MCP23017, TCA9548  | Thomas Aarts          | [github.com/Pi4J/pi4j-device-tca9548](https://github.com/Pi4J/pi4j-device-tca9548) |
| [Simple Button](/documentation/device-examples/simplebutton) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [Simple LED](/documentation/device-examples/simpleled) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [AD Converter ADS1115](/documentation/device-examples/ads1115) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [Buzzer](/documentation/device-examples/buzzer) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [Joystick](/documentation/device-examples/joystick) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [Joystick Analog](/documentation/device-examples/joystickanalog) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [LCD Display](/documentation/device-examples/lcddisplay) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [LEDButton](/documentation/device-examples/ledbutton) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [LEDMatrix](/documentation/device-examples/ledmatrix) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [LEDStrip](/documentation/device-examples/ledstrip) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [Potentiometer](/documentation/device-examples/potentiometer) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|
| [Servo](/documentation/device-examples/servo) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components)|

### Simple Implementation

For a simple implementation of a project with one of the components, the recommendation is to use the [Template-Project](https://github.com/Pi4J/pi4j-template-javafx).
The Readme.md describes how to get started with the project.
To get a better understanding, look at one of those finished template-projects: [Theremin](https://github.com/DieterHolz/RaspPiTheremin) or [Photobooth](https://github.com/DieterHolz/PhotoBooth)

### Electrical Engineering
General inputs and help on electrical engineering can be looked up on Getting started with PI4J / .[Electrical Engineering](/getting-started/electricalengeneering/) page.