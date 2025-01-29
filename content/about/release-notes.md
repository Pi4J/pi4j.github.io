---
title: 'Release Notes'
weight: 40
---

All releases of Pi4J V.2 are listed on [github.com/Pi4J/pi4j/releases](https://github.com/Pi4J/pi4j/releases).

## 2024-10-03 - V2.7.0

* Libraries are loaded depending on the platform, by calling `BoardInfoHelper.runningOnRaspberryPi()`.
* `BoardModel` has been extended with 2Gb Raspberry Pi 5, Raspberry Pi Pico 2, and extra board codes for the Compute Module 4. 
* Allowing configuration of the shutdown hook. It's disabled by default.
* [Issue #354](https://github.com/Pi4J/pi4j/issues/354): Gracefully handle UnsatisfiedLinkError on newAutoContext.
* [Issue #368](https://github.com/Pi4J/pi4j/issues/368): Mock providers don't seem to be loaded on an non-RPi system.
* [Issue #369](https://github.com/Pi4J/pi4j/issues/369): WARN noise in the log about Ignoring providers on every startup. 
  * Removed unnecessary String concatenations in logging statements.
  * Reduced log output and reviewed `warn` levels to reduce to `info` where more applicable.
* [Issue #383](https://github.com/Pi4J/pi4j/issues/383): Increase amount of write bytes to SPI devices over 65535. `spiWrite` has been modified to write data in chunks of 4096 bytes so it can handle larger messages.
* [Issue #388](https://github.com/Pi4J/pi4j/issues/388): I2C writeRead method compares written to writeOffset instead of writeSize.

Because of the changes in the loading of the mock providers, if you want to load them on a Raspberry Pi board, you need to use the following context builder:

```java
var pi4j = Pi4J.newContextBuilder().autoDetectMockPlugins().autoDetectPlatforms().build();
```

Thanks to contributions by [@ylexus](https://github.com/ylexus), [@mores](https://github.com/mores), [@taartspi](https://github.com/taartspi), [@eitch](https://github.com/eitch), [@fdelporte](https://github.com/fdelporte).

All changes: https://github.com/Pi4J/pi4j/compare/2.6.1...2.7.0

## 2024-07-29 - V2.6.1

This is a minor bug fix release to allow a smoother integration in a Spring Boot Starter by allowing to run on PC for testing without initialization errors and with reduced logging of the I2C Mock plugin.

* [Issue #354](https://github.com/Pi4J/pi4j/issues/354): Gracefully handle UnsatisfiedLinkError on newAutoContext when not running on a Raspberry Pi, for instance, when testing on Windows or macOS.
* Clean up of logs in `MockI2C.java`.

All changes: https://github.com/Pi4J/pi4j/compare/2.6.0...2.6.1

## 2024-04-29 - V2.6.0

* New hardware PWM provider added to the GpioD plugin, see: 
  * [Blog: PWM Hardware Support on RPi5](https://pi4j.com/blog/2024/20240423_pwm_rpi5/).
  * [Documentation: I/O Examples: Pulse Width Modulation (PWM)](https://pi4j.com/documentation/io-examples/pwm/).
* Various improvements in the I2C implementation in both core and plugins, see:
  * [Blog: Ongoing I2C Improvements](https://pi4j.com/blog/2024/20240418_i2c_improvements/).
* Dependency bumps in the pom file, see [pull request #337](https://github.com/Pi4J/pi4j/pull/337).
* New BoardInfo included to detect type of Raspberry Pi board, providing a lot of info about the board, SoC, pins, etc., see:
  * [Documentation: Using Board Info](https://pi4j.com/documentation/board-info/).
  * Example implementation and visualization on [api.pi4j.com](https://api.pi4j.com/).
* Fix for "IOBase constructor do not update the fields id, name & description".
  * [Issue #257](https://github.com/Pi4J/pi4j/issues/257): IOAlreadyExistsException when reopening Serial-connection.
  * [Issue #244](https://github.com/Pi4J/pi4j/issues/244): Multiple SPI throws IOAlreadyExistsException.
* Several code improvements and clean-up.

Thanks to contributions by [@fusetim](https://github.com/fusetim), [@taartspi](https://github.com/taartspi), [@eitch](https://github.com/eitch), [@fdelporte](https://github.com/fdelporte).

Make sure to also read the interviews with [Robert von Burg](https://pi4j.com/blog/2024/20240419_interview_robert_von_burg/) and [Tom Aarts](https://pi4j.com/blog/2024/20240425_interview_tom_aarts/).

All changes: https://github.com/Pi4J/pi4j/compare/2.5.1...2.6.0

## 2024-03-18 - V2.5.1

Sorry! Because of a configuration error, the wrong native code is included in 2.5.0 for the new GpioD Provider. But [thanks to the lightning fast action](https://github.com/Pi4J/pi4j/commit/6ac458ec2d9b38a20b2195f4ecc03a65fbdebff7) of [Robert von Burg](https://github.com/eitch) we have a fixed version for you to enjoy :-)

All changes: https://github.com/Pi4J/pi4j/compare/2.5.0...2.5.1

## 2024-03-18 - V2.5.0

With over 100 commits from multiple branches, this is a major release with many improvements! With many thanks to the core team ([Robert von Burg](https://github.com/eitch), [Tom Aarts](https://github.com/taartspi)), and a major addition of [Alexander Liggesmeyer](https://github.com/alex9849), Pi4J is again lifted to a higher level!

You can find out [more about Alexander in this blog post](/blog/2024/20240318_interview_alexander_liggesmeyer/).

{{% notice warning %}}
The new GpioD Provider needs the latest Raspberry Pi OS version (`Debian GNU/Linux 12 (bookworm)`).
{{% /notice %}}

### Changes in 2.5.0

* A new GpioD Provider adds **support for the Raspberry Pi 5**.
  * Issues [#321](https://github.com/Pi4J/pi4j/issues/321), [#320](https://github.com/Pi4J/pi4j/issues/320), [#317](https://github.com/Pi4J/pi4j/issues/317)
  * This new GpioD provider interfaces directly with the Raspberry Pi's gpiochip device, located at `/dev/gpiochip...`. It leverages the [native libgpiod library](https://git.kernel.org/pub/scm/libs/libgpiod/libgpiod.git/?h=v1.6.x), which is developed as a part of the Linux kernel. Libgpiod is currently the recommended way to control GPIO pins. Therefore, using this provider is also recommended.
  * This new provider can be used without the need to start a Pi4J application with sudo, so also fixes [#212](https://github.com/Pi4J/pi4j/issues/212) when you only need DigitalInput and/or DigitalOutput.
* Better handling of mock Plugins: Plugins can now define if they are mocks, and these are not auto-detected anymore. The default target for the Pi4J library is the Raspberry Pi, and thus auto-detecting mocks on the Pi, which are only for tests is counterintuitive.
* Extended Providers with a priority: this priority helps to determine which Provider should be loaded, when multiple Providers with the same IOType are being loaded by different plugins. This change enforces that a given IOType can only have one Provider loaded at runtime preventing errors when, for instance, two I2C providers are loaded at the same time, concurrently writing to the I2C bus.
* Fix for: LinuxFile reused scratch buffers ensuring size was usable. But the limit value cannot be modified so later usage failed as an intended overwrite. Pull request [#331](https://github.com/Pi4J/pi4j/pull/331), commit [ed208f2](https://github.com/Pi4J/pi4j/commit/ed208f26cfd2a92978d010495fa1c6b5f8726e12).
* Fix for: I2C interface should use a restart between the write and read operation. Pull request [#333](https://github.com/Pi4J/pi4j/pull/333).
* Fix for: Shutting down pool executor too early. Commit [7909a2d](https://github.com/Pi4J/pi4j/commit/7909a2d64d07d23732e5e31254d4d32d4c4087bd).
* ProviderProxyHandler got removed, simplifying provider loading, thus no more reflection on the instances.
* You can now add and remove IO instances at runtime.
* You can now easily switch a GPIO from output to an input and vice versa, see issue [#26](https://github.com/Pi4J/pi4j/issues/26), extending on the work by [@MEBoo](https://github.com/MEBoo), in pull request [#1](https://github.com/MEBoo/pi4j-issue26/pull/1).
* A race condition got fixed in the default runtime registry.
* Proper life cycle management got added for of all threads in Pi4J.

All changes: https://github.com/Pi4J/pi4j/compare/2.4.0...2.5.0

### Known Issue

* _java.io.IOException: Remote I/O error java.base/java.io.RandomAccessFile.writeBytes(Native Method). Using linuxfs-i2c, dependent upon i2c operations this exception can occur_: If the program initially uses read or write, and later uses readRegister or writeRegister there is no exception. However, if the program initially uses readRegister or writeRegister subsequent write or read may encounter this exception. For more info and the temporary fix, check [#335](https://github.com/Pi4J/pi4j/issues/335).

## 2023-10-24 - V2.4.0

* Extended LinuxFS plugin
  * PWM provider
  * First set of implementations for Digital Input and Output
  * To be further extended, see https://github.com/Pi4J/pi4j/issues/307
* Don't re-initialize pigpio twice, thus use singleton
* Implement blink method in DigitalOutputBase
* Added testcases for I2CRegisterDataReader, I2CRegisterDataWrite
* Fix I2C write register: multi byte register may fail with large data
* Fix mock SPI.transfer() functionality
  * https://github.com/Pi4J/pi4j/issues/298
  * https://github.com/Pi4J/pi4j/issues/299
  * https://github.com/Pi4J/pi4j/issues/300
* Add readEntireMockBuffer() method to class MockSpi
* Fix for data read over I2C becomes out of sync over a slower wireless network
  * https://github.com/Pi4J/pi4j/issues/16
  * https://github.com/Pi4J/pi4j/issues/303
* Use Socket#setSoTimeout to timeout read requests of GPIO socket implementation
  * https://github.com/Pi4J/pi4j/issues/305

Thanks to [@GeVanCo](https://github.com/GeVanCo), [@MMMMMNG](https://github.com/MMMMMNG), [@IAmNickNack](https://github.com/IAmNickNack), [@savageautomate](https://github.com/savageautomate), [@eitch](https://github.com/eitch), [@taartspi](https://github.com/taartspi), [@FDelporte](https://github.com/FDelporte).

All changes: https://github.com/Pi4J/pi4j/compare/2.3.0...2.4.0

## 2023-02-06 - V2.3.0

* Improvements for PIGPIO.gpioCfgInterfaces by [@bwaldvogel](https://github.com/bwaldvogel).
* New i2c interface to support multibyte register address by [@taartspi](https://github.com/taartspi).
* Fix in LinuxFsI2C byte array offset by [@harlanhu](https://github.com/harlanhu).
* Remove unused JNA references by [@taartspi](https://github.com/taartspi).

All changes: https://github.com/Pi4J/pi4j/compare/2.2.1...2.3.0

## 2022-10-17 - V2.2.1

Multiple fixes by [@taartspi](https://github.com/taartspi):

* Better error message when mixing 32- and 64-bit artifacts
* SPI improvements:
  * Add missing initialization in constructor
  * Track weather the user set the mode or bus config values to improve the use of SPI flags

All changes: https://github.com/Pi4J/pi4j/compare/2.2.0...2.2.1

## 2022-08-30 - V2.2.0

What an amazing achievement! No major issues were found in the previous release, but several small fixes were added by more people than ever before in the Pi4J-history. This is a real confirmation of the openness of this project and how a community can work together to further improve a project. 

A big thank you to everyone who experimented with Pi4J, took part in the discussions, filed an issue, created a merge request, added examples,...!

### New example implementations

Thanks to the work of FHNW students and @taartspi, the list of available example implementations has become larger and larger. We even moved them to their own section of this documentation website! Take a look at [Example implementations](/examples/) if you need a quick-start to use a buzzer, camera, LED strip, TCA9548, MCP4725,... or any of the other examples.

### Changes in V2.2.0

Multiple improvements were added in this release (and others are already in progress for the next one!):

* by [@taartspi](https://github.com/taartspi) to improve SPI initialization, see [#229](https://github.com/Pi4J/pi4j/discussions/229)
* by [@haumacher](https://github.com/haumacher) regarding the use of ByteBuffers, see [#185](https://github.com/Pi4J/pi4j/issues/185)
* by [@savageautomate](https://github.com/savageautomate) regarding the polarity of digital output, see [#93](https://github.com/Pi4J/pi4j/issues/93)
* by [@gugrim](https://github.com/gugrim) to ensure positive values are returned from reading unless at end of file, see [#164](https://github.com/Pi4J/pi4j/issues/164)
* by [@eitch](https://github.com/eitch) to also export LinuxFS I2C in module-info.java
* by [@eitch](https://github.com/eitch) to also copy native libs to distribution zip
* by [@hagen](https://github.com/hagen) to be able to configure sample rate and peripheral in PiGpio
* by Saskia Bikle to add an implementation of deregistration/shutdown for IO's
* by [@savageautomate](https://github.com/savageautomate) to add a new value "flags" too SPI implementation

All the differences can be checked by comparing with the previous release 2.1.1 via [this link](https://github.com/Pi4J/pi4j/compare/2.1.1...2.2.0).

## Earlier release notes

Release notes of the previous releases of Pi4J V.2 are available on [github.com/Pi4J/pi4j/releases](https://github.com/Pi4J/pi4j/releases).