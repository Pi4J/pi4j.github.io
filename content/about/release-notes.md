---
title: 'Release Notes'
weight: 40
---

All releases of Pi4J V.2 are listed on [github.com/Pi4J/pi4j-v2/releases](https://github.com/Pi4J/pi4j-v2/releases).

## 2024-03-?? - V2.5.0

With over 100 commits from multiple branches, this is a major release with many improvements! With many thanks to the core team, and a major addition of Alexander Liggesmeyer, Pi4J is again lifted to a higher level!

* A new GpioD Provider adds **support for the Raspberry Pi 5**.
  * Issues [#321](https://github.com/Pi4J/pi4j-v2/issues/321), [#320](https://github.com/Pi4J/pi4j-v2/issues/320), [#317](https://github.com/Pi4J/pi4j-v2/issues/317)
  * This new provider can be used without the need to start a Pi4J application with sudo, so also fixes [#212](https://github.com/Pi4J/pi4j-v2/issues/212) when you only need DigitalInput and/or DigitalOutput.
* Better handling of mock Plugins: Plugins can now define if they are mocks, and these are not auto-detected anymore. The default target for the Pi4J library is the Raspberry Pi, and thus auto-detecting mocks on the Pi, which are only for tests is counterintuitive.
* Extended Providers with a priority: this priority helps to determine which Provider should be loaded, when multiple Providers with the same IOType are being loaded by different plugins. This change enforces that a given IOType can only have one Provider loaded at runtime preventing errors when, for instance, two I2C providers are loaded at the same time, concurrently writing to the I2C bus.
* Fix for: LinuxFile reused scratch buffers ensuring size was usable. But the limit value cannot be modified so later usage failed as an intended overwrite. Pull request [#331](https://github.com/Pi4J/pi4j-v2/pull/331).
* Fix for: I2C interface should use a restart between the write and read operation. Pull request [#333](https://github.com/Pi4J/pi4j-v2/pull/333).
* Fix for: LinuxFile reused scratch buffers ensuring size was usable, but the limit value cannot be modified so later usage failed as an intended overwrite. Commit [ed208f2](https://github.com/Pi4J/pi4j-v2/commit/ed208f26cfd2a92978d010495fa1c6b5f8726e12).
* Fix for: Shutting down pool executor too early. Commit [7909a2d](https://github.com/Pi4J/pi4j-v2/commit/7909a2d64d07d23732e5e31254d4d32d4c4087bd).
* And more additional changes:
  * Remove the ProviderProxyHandler, simplifying provider loading, thus no more reflection on the instances.
  * Allow to add and remove IO instances at runtime.
  * Allow to easily switch a GPIO from output to an input and vice versa, see issue [#26](https://github.com/Pi4J/pi4j-v2/issues/26), extending on the work by [@MEBoo](https://github.com/MEBoo), in pull request [#1](https://github.com/MEBoo/pi4j-v2-issue26/pull/1).
  * Fixing a race condition in the default runtime registry.
  * Added properly life cycle management of all threads in Pi4J.

All changes: https://github.com/Pi4J/pi4j-v2/compare/2.4.0...2.5.0

## 2023-10-24 - V2.4.0

* Extended LinuxFS plugin
  * PWM provider
  * First set of implementations for Digital Input and Output
  * To be further extended, see https://github.com/Pi4J/pi4j-v2/issues/307
* Don't re-initialize pigpio twice, thus use singleton
* Implement blink method in DigitalOutputBase
* Added testcases for I2CRegisterDataReader, I2CRegisterDataWrite
* Fix I2C write register: multi byte register may fail with large data
* Fix mock SPI.transfer() functionality
  * https://github.com/Pi4J/pi4j-v2/issues/298
  * https://github.com/Pi4J/pi4j-v2/issues/299
  * https://github.com/Pi4J/pi4j-v2/issues/300
* Add readEntireMockBuffer() method to class MockSpi
* Fix for data read over I2C becomes out of sync over a slower wireless network
  * https://github.com/Pi4J/pi4j-v2/issues/16
  * https://github.com/Pi4J/pi4j-v2/issues/303
* Use Socket#setSoTimeout to timeout read requests of GPIO socket implementation
  * https://github.com/Pi4J/pi4j-v2/issues/305

Thanks to [@GeVanCo](https://github.com/GeVanCo), [@MMMMMNG](https://github.com/MMMMMNG), [@IAmNickNack](https://github.com/IAmNickNack), [@savageautomate](https://github.com/savageautomate), [@eitch](https://github.com/eitch), [@taartspi](https://github.com/taartspi), [@FDelporte](https://github.com/FDelporte).

All changes: https://github.com/Pi4J/pi4j-v2/compare/2.3.0...2.4.0

## 2023-02-06 - V2.3.0

* Improvements for PIGPIO.gpioCfgInterfaces by [@bwaldvogel](https://github.com/bwaldvogel).
* New i2c interface to support multibyte register address by [@taartspi](https://github.com/taartspi).
* Fix in LinuxFsI2C byte array offset by [@harlanhu](https://github.com/harlanhu).
* Remove unused JNA references by [@taartspi](https://github.com/taartspi).

All changes: https://github.com/Pi4J/pi4j-v2/compare/2.2.1...2.3.0

## 2022-10-17 - V2.2.1

Multiple fixes by [@taartspi](https://github.com/taartspi):

* Better error message when mixing 32- and 64-bit artifacts
* SPI improvements:
  * Add missing initialization in constructor
  * Track weather the user set the mode or bus config values to improve the use of SPI flags

All changes: https://github.com/Pi4J/pi4j-v2/compare/2.2.0...2.2.1

## 2022-08-30 - V2.2.0

What an amazing achievement! No major issues were found in the previous release, but several small fixes were added by more people than ever before in the Pi4J-history. This is a real confirmation of the openness of this project and how a community can work together to further improve a project. 

A big thank you to everyone who experimented with Pi4J, took part in the discussions, filed an issue, created a merge request, added examples,...!

### New example implementations

Thanks to the work of FHNW students and @taartspi, the list of available example implementations has become larger and larger. We even moved them to their own section of this documentation website! Take a look at [Example implementations](/examples/) if you need a quick-start to use a buzzer, camera, LED strip, TCA9548, MCP4725,... or any of the other examples.

### Changes in V2.2.0

Multiple improvements were added in this release (and others are already in progress for the next one!):

* by [@taartspi](https://github.com/taartspi) to improve SPI initialization, see [#229](https://github.com/Pi4J/pi4j-v2/discussions/229)
* by [@haumacher](https://github.com/haumacher) regarding the use of ByteBuffers, see [#185](https://github.com/Pi4J/pi4j-v2/issues/185)
* by [@savageautomate](https://github.com/savageautomate) regarding the polarity of digital output, see [#93](https://github.com/Pi4J/pi4j-v2/issues/93)
* by [@gugrim](https://github.com/gugrim) to ensure positive values are returned from reading unless at end of file, see [#164](https://github.com/Pi4J/pi4j-v2/issues/164)
* by [@eitch](https://github.com/eitch) to also export LinuxFS I2C in module-info.java
* by [@eitch](https://github.com/eitch) to also copy native libs to distribution zip
* by [@hagen](https://github.com/hagen) to be able to configure sample rate and peripheral in PiGpio
* by Saskia Bikle to add an implementation of deregistration/shutdown for IO's
* by [@savageautomate](https://github.com/savageautomate) to add a new value "flags" too SPI implementation

All the differences can be checked by comparing with the previous release 2.1.1 via [this link](https://github.com/Pi4J/pi4j-v2/compare/2.1.1...2.2.0).

## Earlier release notes

Release notes of the previous releases of Pi4J V.2 are available on [github.com/Pi4J/pi4j-v2/releases](https://github.com/Pi4J/pi4j-v2/releases).