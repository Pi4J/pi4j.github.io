---
title: "IO Checker Tool"
date: 2025-10-13
tags: ["PWM", "SPI", "I2C", "UART", "Serial", "GPIO", "Jbang"]
---

For some of the IO types (PWM, SPI,...), additional configurations are required. These are documented in 
[I/O Types](/documentation/io-types/), but still, sometimes it's hard to remember what's required or difficult
to validate. For that reason, an IO Checker tool has been created. It's part of the [Pi4J OS repository](https://github.com/Pi4J/pi4j-os/tree/main/iochecks) and can be executed directly from the GitHub file with JBang. This means it's very
easy to use, but also to extend if other checks reveal to be helpful.

To run the tool for all IO types, use:
```shell
jbang https://github.com/pi4j/pi4j-os/blob/main/iochecks/IOChecker.java
```

Individual checks can be executed by passing one or more check names as argument:

* gpio
* pwm
* i2c
* spi
* serial

For example:

* Only PWM:
```shell
jbang https://github.com/pi4j/pi4j-os/blob/main/iochecks/IOChecker.java pwm
```
* I2C and SPI:
```shell
jbang https://github.com/pi4j/pi4j-os/blob/main/iochecks/IOChecker.java i2c spi
```

You will get a result like the following, indicating if the check passed or failed, with more info about the expected 
and found result. For example, the I2C check also lists the detected devices, in this case on addresses 0x21, 0x5C, 0x70.

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

Each of the available tests are also documented on the page for each IO type:

* [Checking PWM Configuration](/documentation/io-types/pwm/#checking-pwm-configuration)
* [Checking I2C Configuration](/documentation/io-types/i2c/#checking-i2c-configuration)
* [Checking SPI Configuration](/documentation/io-types/spi/#checking-spi-configuration)
* [Checking Serial Configuration](/documentation/io-types/serial/#checking-serial-configuration)