---
title: LinuxFS Provider
weight: 93
tags: ["LinuxFS", "PWM", "I2C"]
---

The current implementation of the LinuxFS plugin implements a file based I2C, SPI, and PWM provider. The file based I2C provider opens 
`/dev/i2c-1` using a `RandomAccessFile` to perform I2C reads and writes. The file based PWM provider opens
`/sys/class/pwm/pwmchip?` using a `RandomAccessFile` to perform PWM operations.

{{% notice warning %}}
The Linuxfs provider linuxfs-pwm requires minimum kernel Bullseye 6.1.21 and Bookworm 6.6.22 !
{{% /notice %}}

Providers in the LinuxFS plugin:

* linuxfs-i2c
* linuxfx-spi
* linuxfs-pwm --> check below for important info about the channel configuration!
* Under construction
  * linuxfs-digital-input
  * linuxfs-digital-output

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

## I2C 

Example on how to use I2C with LinuxFS:

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

## SPI

The buffer size for this SPI implementation is 4096 bytes. This can be configured in `config.txt`:

* Debian Bullseye OS: `/boot/config.txt`
* Raspberry Pi OS, based on Debian Bookworm: `/boot/firmware/config.txt`

```java
      var spiConfig = Spi.newConfigBuilder(pi4j)
        .id(SPI_PROVIDER_ID)
        .name(SPI_PROVIDER_NAME)
        .bus(spiBus)
        .chipSelect(chipSelect)
        .baud(Spi.DEFAULT_BAUD)
        .mode(SpiMode.MODE_0)
        .provider("linuxfs-spi")
        .build();
var spi = pi4j.create(spiConfig);

```

## PWM

To use PWM with the LinuxFS provider, it's important to understand the config builder needs the **channel number**, not the BCM number! This channel number, is different depending on the type of board you are using. 

For instance, on a Raspberry Pi 5 with the `dtoverlay=pwm-2chan` setting in `config.txt`, a PWM connection on BCM 19 must be configured as `channel=3`. 

See the [Pulse Width Modulation (PWM)](/documentation/io-examples/pwm/#linuxfs-provider-linuxfs-pwm) page on how to configure hardware PWM and which channels are available per board.

Example on how to use PWM with LinuxFS:

```java
  /**
     * Builds a new PWM configuration for the buzzer
     *
     * @param pi4j    Pi4J context
     * @param channel Channel number of the PWM
     * @return PWM configuration
     */
    protected static PwmConfig buildPwmConfig(Context pi4j, int channel) {
        return Pwm.newConfigBuilder(pi4j)
            .id("PWMChannel" + channel)
            .name("Buzzer")
            .address(channel)
            .pwmType(PwmType.HARDWARE)
            .provider("linuxfs-pwm")
            .initial(0)
            .shutdown(0)
            .build();
    }

```

