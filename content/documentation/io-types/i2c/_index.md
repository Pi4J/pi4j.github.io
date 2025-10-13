---
title: Inter-Integrated Circuit (I²C)
weight: 230
tags: ["I2C"]
aliases:
  - /documentation/io-examples/i2c/
---

## What is it?

I²C (spoken as I-Squared-C) is a bus originally invented by Philips. 
It is designed as a classic master-slave bus. A data transfer is always i
nitiated by a master. It can also be set up in a multi-master system. 
I²C is connected via two signal lines (data line and clock line). 
The transmission rate of the bus can be between 0.1 Mbit/s up to 3.4 Mbit/s 
depending on the clock rate. If only a unidirectional connection is required, 
even 5.0 Mbit/s would be possible. It should be noted: the higher the clock rate, 
the more susceptible to failure the overall system becomes. The low operating 
voltage of only 3.3V does not contribute to interference resistance either.

## Uses

I²C is mainly used for communication between microcontrollers. The advantage 
that a whole series of microcontrollers can be controlled via just 2 lines is 
of course very interesting for the circuit board layout. The main advantages of 
I²C are its simplicity. There are certainly newer bus systems with better 
transmission rates. Hardly any bus system is as easy to use as I²C. Even 
“hot plugging”, ie plugging in and unplugging the devices during operation, 
is possible with I²C.

## Addressing

I²C uses an address space of 7 bits. This allows up to 112 nodes on one bus. 
The remaining 16 addresses are reserved for special applications. Usually the 
address of a device is defined directly by the manufacturer. It can therefore 
be found in the relevant data sheets. Due to the shortage of addresses, 
there is also a variant with a 10-bit address space. Up to 1136 nodes are 
possible, and the protocol is compatible with the smaller 7-bit address space.

Command line tool to output a list of installed busses:
```
root@rp5:~# i2cdetect -l
i2c-1	i2c       	Synopsys DesignWare I2C adapter 	I2C adapter
i2c-11	i2c       	107d508200.i2c                  	I2C adapter
i2c-12	i2c       	107d508280.i2c                  	I2C adapter
```

If you are not seeinging `i2c-1, then you might have missed a few steps in [The First Boot](https://www.pi4j.com/prepare/first-boot/).
The specific line needed to enable i2c is:
```shell
root@rp5:~# raspi-config nonint do_i2c 0
```

Command line tool to immediately scan the standard addresses on I2C bus 1 (i2c-1)
```
root@rp5:~# i2cdetect -y 1
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:                         -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 3f 
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- --
```
1 device found with address of 0x3f.

## Checking I2C Configuration

You can check the I2C configuration of your Raspberry Pi with the following command, using [JBang](/prepare/install-java/#install-sdkman-maven-and-jbang) and a checker tool available in the [GitHub Pi4J OS repository](https://github.com/pi4J/pi4j-os). One or more checks are performed depending on the IO type checked by the tool. You will get a result like this, indicating if the check passed or failed, with more info about the expected and found result:

```shell
$ jbang https://github.com/pi4j/pi4j-os/blob/main/iochecks/IOChecker.java i2c

Results from I2C Detection

	Configuration check for I2C in config.txt
		Status: PASS
		Expected: 
			dtparam=i2c_arm=on
		Result: 
			Found in /boot/firmware/config.txt: dtparam=i2c_arm=on

	Search for I2C in /proc/device-tree
		Status: PASS
		Expected: 
			i2c device-tree entries with status=okay
		Result: 
			✗ i2c@7d005600 (status: disabled)
			✓ i2c@7d508200 (status: okay)
			✓ i2c@7d508280 (status: okay)
			✗ i2c3_m4_agpio0_pins (status: unknown)

	i2cdetect -l
		Status: PASS
		Expected: 
			One or more devices, e.g. 'i2c-1' (I2C bus adapters detected by 'i2cdetect -l')
		Result: 
			1: Synopsys, DesignWare I2C adapter I2C adapter
			13: 107d508200.i2c, I2C adapter
			14: 107d508280.i2c, I2C adapter

	i2cdetect -y 1
		Status: PASS
		Expected: 
			One or more I2C used addresses detected on bus 1
		Result: 
			Found 3 used addres(ses) on bus 1: 0x21, 0x5C, 0x70

	i2cdetect -y 13
		... # Truncated for brevity
```

## Transfer rates

| Mode | Max. transfer rate | Direction |
| --- | --- | --- |
| Standard Mode | 0.1 Mbit/s | bidirektional |
| Fast Mode | 0.4 Mbit/s | bidirektional |
| Fast Mode Plus | 1.0 Mbit/s | bidirektional |
| High Speed Mode | 3.4 Mbit/s | bidirektional |
| Ultra Fast-mode | 5.0 Mbit/s | unidirektional |

## Additional information

- [Wikipedia I²C](https://en.wikipedia.org/wiki/I%C2%B2C)
- [I²C Bus](https://i2c-bus.org)

## Code example

{{% notice tip %}}
Feel free to check the [Kotlin DSL for I²C](/kotlin/i2c/)
{{% /notice %}}

The following code shows setting the pins on a TCA 9534 which can be found on 
["Sequent Microsystems"](https://www.kickstarter.com/projects/279405789/4-relays-for-raspberry-pi-8-level-stackable-10a-250v-each)

To use the LinuxFS provider, which provides I2C, add the proper dependency:

```xml

<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-plugin-linuxfs</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```

Now we can use the following example:

```java
import com.pi4j.Pi4J;
import com.pi4j.context.Context;
import com.pi4j.io.i2c.I2C;
import com.pi4j.io.i2c.I2CConfig;
import com.pi4j.io.i2c.I2CProvider;

public class SimpleTca9534I2cTest {

	private static final byte TCA9534_REG_ADDR_OUT_PORT = 0x01;
	private static final byte TCA9534_REG_ADDR_CFG = 0x03;

	public static void main(String[] args) throws Exception {

		Context pi4j = Pi4J.newAutoContext();
		I2CProvider i2CProvider = pi4j.provider("linuxfs-i2c");
		I2CConfig i2cConfig = I2C.newConfigBuilder(pi4j).id("TCA9534").bus(1).device(0x3f).build();
		try (I2C tca9534Dev = i2CProvider.create(i2cConfig)) {

			int config = tca9534Dev.readRegister(TCA9534_REG_ADDR_CFG);
			if (config < 0)
				throw new IllegalStateException(
						"Failed to read configuration from address 0x" + String.format("%02x", TCA9534_REG_ADDR_CFG));

			byte currentState = (byte) tca9534Dev.readRegister(TCA9534_REG_ADDR_OUT_PORT);

			if (config != 0x00) {
				System.out.println("TCA9534 is not configured as OUTPUT, setting register 0x" + String
						.format("%02x", TCA9534_REG_ADDR_CFG) + " to 0x00");
				currentState = 0x00;
				tca9534Dev.writeRegister(TCA9534_REG_ADDR_OUT_PORT, currentState);
				tca9534Dev.writeRegister(TCA9534_REG_ADDR_CFG, (byte) 0x00);
			}

			// bit 8, is pin 1 on the board itself, so set pins in reverse:
			currentState = setPin(currentState, 8, tca9534Dev, true);
			Thread.sleep(500L);
			currentState = setPin(currentState, 8, tca9534Dev, false);
			Thread.sleep(500L);

			currentState = setPin(currentState, 7, tca9534Dev, true);
			Thread.sleep(500L);
			currentState = setPin(currentState, 7, tca9534Dev, false);
			Thread.sleep(500L);
		}
	}

	public static byte setPin(byte currentState, int pin, I2C tca9534Dev, boolean high) {
		byte newState;
		if (high)
			newState = (byte) (currentState | (1 << pin));
		else
			newState = (byte) (currentState & ~(1 << pin));

		System.out.println("Setting TCA9534 to new state " + asBinary(newState));
		tca9534Dev.writeRegister(TCA9534_REG_ADDR_OUT_PORT, newState);
		return newState;
	}

	public static String asBinary(byte b) {
		StringBuilder sb = new StringBuilder();

		sb.append(((b >>> 7) & 1));
		sb.append(((b >>> 6) & 1));
		sb.append(((b >>> 5) & 1));
		sb.append(((b >>> 4) & 1));
		sb.append(((b >>> 3) & 1));
		sb.append(((b >>> 2) & 1));
		sb.append(((b >>> 1) & 1));
		sb.append(((b >>> 0) & 1));

		return sb.toString();
	}
}
```
