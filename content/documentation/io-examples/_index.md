---
title: I/O Examples
weight: 120
---

Here you can find detailed examples for the different functionalities of Pi4J per I/O type.

The supported low-level I/O interface types are defined in the core library as [an enumerated list](https://github.com/Pi4J/pi4j-v2/blob/master/pi4j-core/src/main/java/com/pi4j/io/IOType.java). 

```
ANALOG_INPUT(AnalogInputProvider.class, AnalogInput.class, AnalogInputConfig.class, AnalogInputConfigBuilder.class),
ANALOG_OUTPUT(AnalogOutputProvider.class, AnalogOutput.class, AnalogOutputConfig.class, AnalogOutputConfigBuilder.class), 
DIGITAL_INPUT(DigitalInputProvider.class, DigitalInput.class, DigitalInputConfig.class, DigitalInputConfigBuilder.class), 
DIGITAL_OUTPUT(DigitalOutputProvider.class, DigitalOutput.class, DigitalOutputConfig.class, DigitalOutputConfigBuilder.class), 
PWM(PwmProvider.class, Pwm.class, PwmConfig.class, PwmConfigBuilder.class), 
I2C(I2CProvider.class, com.pi4j.io.i2c.I2C.class, I2CConfig.class, I2CConfigBuilder.class), 
SPI(SpiProvider.class, Spi.class, I2CConfig.class, I2CConfigBuilder.class), 
SERIAL(SerialProvider.class, Serial.class, SerialConfig.class, SerialConfigBuilder.class);
```
