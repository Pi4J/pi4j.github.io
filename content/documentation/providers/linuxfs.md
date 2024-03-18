---
title: LinuxFS Provider
weight: 93
tags: ["LinuxFS"]
---

The current implementation of the LinuxFS plugin implements a file based I2C provider. The file based provider opens 
`/dev/i2c-1` using a `RandomAccessFile` to perform I2C reads and writes.

Providers in the LinuxFS plugin:

* linuxfs-i2c
* Under construction
  * linuxfs-digital-input
  * linuxfs-digital-output
  * linuxfs-pwm

To use the LinuxFS provider include the following dependencies:

``` xml
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-core</artifactId>
    <version>${pi4j.version}</version>
</dependency>
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-plugin-raspberrypi</artifactId>
    <version>${pi4j.version}</version>
</dependency>
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-plugin-linuxfs</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```

And then one can get access to the provider as follows:

``` java
Context pi4j = Pi4J.newAutoContext();
I2CProvider i2CProvider = pi4j.provider("linuxfs-i2c");
I2CConfig i2cConfig = I2C.newConfigBuilder(pi4j).id("TCA9534").bus(1).device(0x3f).build();

try (I2C tca9534Dev = i2CProvider.create(i2cConfig)) {

	int config = tca9534Dev.readRegister(TCA9534_REG_ADDR_CFG);

	tca9534Dev.writeRegister(TCA9534_REG_ADDR_OUT_PORT, currentState);
	tca9534Dev.writeRegister(TCA9534_REG_ADDR_CFG, (byte) 0x00);

	tca9534Dev.writeRegister(TCA9534_REG_ADDR_OUT_PORT, newState);
}

pi4j.shutdown();
```
