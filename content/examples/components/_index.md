---
title: Components
weight: 50
---

The core Pi4J V.2 library doesn't contain any specific support for devices like buttons, motors, LCD etc. This page lists widely used components
for which a Java implementation, based on Pi4J V.2, is available.

### Current available components

| Device(s)                     | Developed by          | Link              |
| :---                          | :---                  | :---              |
| [Simple Button](/documentation/device-examples/components/simplebutton) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/SimpleButton_App.java)|
| [Simple LED](/documentation/device-examples/components/simpleled) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/SimpleLED_App.java)|
| [AD Converter ADS1115](/documentation/device-examples/components/ads1115) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/ADS1115_App.java)|
| [Buzzer](/documentation/device-examples/components/buzzer) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/Buzzer_App.java)|
| [Camera](/documentation/device-examples/components/camera) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/Camera_App.java)|
| [Joystick](/documentation/device-examples/components/joystick) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/Joystick_App.java)|
| [Joystick Analog](/documentation/device-examples/components/joystickanalog) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/JoystickAnalog_App.java)|
| [LCD Display](/documentation/device-examples/components/lcddisplay) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/LCDDisplay_App.java)|
| [LED Button](/documentation/device-examples/components/ledbutton) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/LEDButton_App.java)|
| [LED Matrix](/documentation/device-examples/components/ledmatrix) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/LEDMatrix_App.java)|
| [LED Strip](/documentation/device-examples/components/ledstrip) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/LEDStrip_App.java)|
| [Potentiometer](/documentation/device-examples/components/potentiometer) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/Potentiometer_App.java)|
| [ServoMotor](/documentation/device-examples/components/servo) | Reto Stutz, Mike Schoder | [Example Devices](https://github.com/Pi4J/pi4j-example-components/blob/main/src/main/java/com/pi4j/catalog/applications/Servo_App.java)|

### Simple Implementation

For a Simple Implementation, the recommendation is to use the [Launcher Class](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/Launcher.java).
With this, a simple application can be started.

### Electrical Engineering
General inputs and help on electrical engineering can be looked up on Getting started with PI4J / [Electrical Engineering](/getting-started/electricalengeneering/) page.