---
title: "Ongoing I2C Improvements"
date: 2024-04-18
tags: ["Pi4J", "I2C"]
---

2024-04-17, by Frank Delporte

Robert von Burg is working on improvements of the I2C implementation in Pi4J in preparation for the next release. The changes are in [pull request #351](https://github.com/Pi4J/pi4j/pull/351/files). It's still work-in-progress but will bring these improvements:

* New `I2C.execute(Callable)` method to allow to atomically execute multiple I2C calls in a thread in a safe way.
* New `I2C.writeRead(byte[], byte[])` method to atomically perform a `write`, immediately followed by a `read` on the I2C bus.
* Fix an issue where the `LinuxFsI2CBus` was closed when closing an I2C device. This can lead to errors as another device might still be open on the same bus, and an operation on the underlying `RandomAccessFile` would lead to exceptions.
* Fix a workaround that required an `I2C.read()` on a newly created `LinuxFsI2C` device, if the first call was an `ioctl`. The device was not selected prior to the `ioctl` call.
* Additional code cleanup and more to come...

This kind of methods is hard to test in unit tests as they interact with real components and need to handle the data and I2C devices depending on the interaction. As a solution, Robert is using a [test project](https://github.com/eitch/pi4j-test/tree/feature/eitch-leds) that has an implementation for an OLED display over I2C, using these commands.

<video controls width="800">
  <source src="/assets/blogs/i2c/i2c-test.mp4" />
</video>

