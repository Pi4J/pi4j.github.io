---
title: Project structure
weight: 10
---

To ensure the Pi4J V2 project is easy to maintain, there is a clear separation between the core functions and isolated test, example and plugin projects.

On this page we want to give you an overview of the projects which are part of the [GitHub Pi4J Project](https://github.com/Pi4J).

![Pi4J V2 code structure](https://raw.githubusercontent.com/Pi4J/pi4j-v2/master/assets/draw.io/pi4j-v2-code-structure.jpg)



# Pi4J V2 Main project

* [github.com/Pi4J/pi4j-v2](https://github.com/Pi4J/pi4j-v2)
* This is the main Pi4J V2 project providing all (basic) I/O functionalities.

## Pi4J Parent POM 
* /pom.xml
* This is "the grandparent POM" and the place to build the entire project.

## Pi4J Libraries

* /libraries/*
* This folder contains (JNI native) libraries that Pi4J or Pi4J plugins may require for runtime.
* Libraries are not Pi4J extension, plugins, providers, platforms, etc. 
* At this moment only a PiGpio library is included, but could be extended in the future.
* By isolation the native functions in libraries, the underlying I/O interface can easily be replaced later without breaking the core library.

### Pi4J Libraries Parent POM

* /libraries/pi4j-library/pom.xml
* Base library to be used when creating a new library.
* Contains the parent pom.xml-file for all library implementations.

### Pi4J PiGPIO JNI Wrapper Library

* /libraries/pi4j-library-pigpio
* This library is a Java library to wrap the PiGPIO API and implement the JNI layer to facilitate use of PiGPIO in Java.  
* There is no Pi4J specific API or code in this library. 
* This PiGPIO wrapper can be used directly without using the Pi4J-core but in that case your application highly depends on the methods of PiGPIO and will be very hard to refactor if you need to use another wrapper.

## Pi4J Core Library

* /pi4j-core
* This is the Pi4J V2 API and core implementation of the framework and runtime.   
* Doesn't contain any actual I/O providers, platforms or IO/platform implementation --> those are all provided via extensions/plugins.  

## Pi4J Unit/Integration Test 

* /pi4j-test
* This is intended to be a place for unit and integration tests to test the APIs and features.
* It only performs tests using MOCK I/O via the Mock IO Provider (plugin). 
* It should not attempt to perform any real I/O testing.

## Pi4J Plugins: the actual I/O providers, platforms and implementations

* /plugins/*
* This folder contains any plugins for use with Pi4J such as IO providers, platforms, or extensions.  
* Plugins must implement the Pi4J Plugin Interface (com.pi4j.extension.Plugin) and declare the implementation class using the "provides" directive in the module info class. 
* See for an example in [/plugins/pi4j-plugin-mock/src/main/java/module-info.java](https://github.com/Pi4J/pi4j-v2/blob/master/plugins/pi4j-plugin-mock/src/main/java/module-info.java)

### Pi4J Libraries Parent POM
 
* /plugins/pi4j-plugin/pom.xml*
* Base library to be used when creating a new plugin.
* Contains the parent pom.xml-file for all plugin implementations.

### Pi4J LinuxFS Provider

* /plugins/pi4j-plugin-linuxfs 
* This plugin is intended to implement I/O Providers for Linux file system operations such as SERIAL, SPI, I2C and perhaps basic GPIO.  
* This plugin is mostly empty at this moment.
* Goal is to have an I/O Provider which is totally independant of an underlying program.

### Pi4J Mock Platform & Provider

* /plugins/pi4j-plugin-mock
* This plugin implements both a Mock Platform and Mock I/O Providers for every I/O type supported by Pi4J.
* This Mock plugin is used by the unit and integration testing project.

### Pi4J PiGPIO Provider

* /plugins/pi4j-plugin-pigpio
* This plugin implements I/O Providers for every I/O type supported by the PiGPIO library.  
* At this moment, this single plugin supports both
** local/native connectivity to PiGPIO
** remote (TCP) connectivity to PiGPIO
** TO BE DISCUSSED: Perhaps this should be separated into two plugins? Or moved to a separate "remote connectivity project"?

### Pi4J RaspberryPi Platform & Provider

* /plugins/pi4-plugin-raspberrypi
* This plugin is intended to implement the Provider for the Raspberry Pi models and declare the default I/O providers for each of the I/O types supported by each RPi model.

### Pi4J WiringPi Provider

* NOT IN THE PROJECT CODE
* This plugin was intended to implement I/O Providers for use with the WiringPi library, similar to the PiGPIO provider.  
* However with the WiringPi project no longer being maintained publicly, this plugin was not implemented

# Stand-alone projects

## Pi4J Test Harness

*  [github.com/Pi4J/pi4j-test-harness](https://github.com/Pi4J/pi4j-test-harness)
*  This project contains the source code (both Java library and Arduino code) for the hardware test harness which has been created to eventually perform hardware testing at the physical layer to help speed up verification for each RPI hardware model
*  Current state is very rough but functional.  
*  This project has been moved outside of the core project as this is only used for the validation test cycle before releasing a new version. 
*  For more info, see ["Hardware testing"](/core-code-internals/hardware-testing)

## Pi4J Example projects

### Pi4J Examples

* [github.com/Pi4J/pi4j-examples](https://github.com/Pi4J/pi4j-examples)
* This project contains numerous code examples to demonstrate how to use Pi4J
* Certain functions have examples to reach the same goal with different use types, e.g. initialization of a DigitalInput with code, properties and annotations.

### Pi4J Minimal example

* [github.com/Pi4J/pi4j-example-minimal](https://github.com/Pi4J/pi4j-example-minimal)
* Example project only showing the use of a digital input and output with minimal code but a lot of comments

### Pi4J Telegraph example

* [github.com/Pi4J/pi4j-example-telegraph](https://github.com/Pi4J/pi4j-example-telegraph)
* Example project demonstrated during Oracle Code One 2019