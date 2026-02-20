---
title: 'Release Notes'
weight: 40
---

All releases of Pi4J V2+ are listed on [github.com/Pi4J/pi4j/releases](https://github.com/Pi4J/pi4j/releases).

## V4

Requires Java 25, see [What's New in V4](/about/info-v4/) for more info.

### 2026-02-20 - V4.0.0

This is a big release with almost 400 commits and 300+ files added/changed...! **Pi4J V4 introduces the new [FFM plugin](/documentation/providers/ffm) and bumps the Java version to 25**. The FFM plugin makes use of the now Foreign Function & Memory API (FFM) to access the GPIOs. The FFM API got introduced in Java 22 with [JEP 454](https://openjdk.org/jeps/454).

This is the most tested release of Pi4J yet! The `pi4j-test` module has been reworked by [@taartspi](https://github.com/taartspi) to provide a smoke test approach with a fixed hardware setup that uses, for instance, input GPIOs to validate output GPIOs and PWM. Check [Hardware Testing](/architecture/about-the-code/hardware-testing/) for more info and how to setup.

Some highlights of all the changes in this release:

* [Issue #454](https://github.com/Pi4J/pi4j/issues/454): Implement new FFM API approach. First big pull request by [@DigitalSmile](https://github.com/DigitalSmile): [#458](https://github.com/Pi4J/pi4j/pull/458) with more for further improving, finetuning, and testing.
* Consistent use of `bcm`, `channel`, `bus`, `chip` when initializing an IO instead of the sometimes confusing `pin`or `address`. With related changes in the Pi4J registry to be able to correctly remove and reuse IO instances.
* [Issue #478](https://github.com/Pi4J/pi4j/issues/478): Race condition in GpioDDigitalInput causes monitor thread to exit
* BoardInfo: added CM5 Lite, and 500 Plus
* Bump Docker builder to JDK 25
* Nexus staging plugin replaced with Central Publishing plugin
* Rework of the [pi4j-test](https://github.com/Pi4J/pi4j/tree/develop/pi4j-test) module to provide an easy SmokeTest approach with a fixed hardware test setup.
* Various LinuxFS plugin improvements.
* Overall code fixes, improvements, new helper methods, cleanup, etc..
* Complete removal of serial support, use jSerialComm instead of Pi4J for serial communication, as [explained here](https://www.pi4j.com/documentation/io-types/serial/).

Thanks to contributions by [@DigitalSmile](https://github.com/DigitalSmile), [@IAmNickNack](https://github.com/IAmNickNack), [@stefanhaustein](https://github.com/stefanhaustein), [@taartspi](https://github.com/taartspi), [@eitch](https://github.com/eitch), [@fdelporte](https://github.com/fdelporte).

Detailed list of all the changes: https://github.com/Pi4J/pi4j/compare/3.0.3...4.0.0

## V3

Requires Java 21, see [What's New in V3](/about/info-v3/) for more info.

### 2025-09-23 - V3.0.3

Work is ongoing to extend Pi4J with a plugin based on the FFM API (Foreign Function & Memory API). To make this possible, some changes have been made to the core code in preparation for this new plugin. And of course more improvements and bug fixes... 

* Board models: Added CM5 Lite board codes.
* Replace Nexus Staging plugin with Central Publishing plugin.
* Refactored `Registry` to use `IOType` for managing addresses, ensuring better segregation of address spaces between IO types. Updated related methods and internal data structures accordingly.
* Introduced the ability to shutdown and unregister IO instances using the instance itself, complementing the existing ID-based method. Updated related methods, tests, and documentation to reflect the new functionality.
* Ensure proper removal of IO instance during shutdown in DefaultRuntimeRegistry.
* PWM IO Change Float to Integer and remove float related conversions.
* Gate digital output event creation on listener / binding presence.
* Move PWM chip detection to BoardInfo to make it usable for all plugins.
* Unit test improvements.
* LinuxFS plugin:
  * I2C: Improvements in `registerRead`.
  * SPI: SPI write now supports larger buffers by creating multi ioctl spi writes.
  * PWM: When the RP1 chip is found, PWM provider will use the RP1 architected address of PWM0 to determine the correct pwmChipx to use. This change will effect Raspberry Pi 5 and Compute Module 5 using updated kernel.
* GpioD plugin:
  * Introduced a volatile `running` flag to properly manage the lifecycle of the input listener thread. Enhanced shutdown logic to ensure threads are safely and consistently terminated. Fix for [Issue #478](https://github.com/Pi4J/pi4j/issues/478).
  * Make GpioLine Closeable.

Thanks to contributions by [@IAmNickNack](https://github.com/IAmNickNack), [@stefanhaustein](https://github.com/stefanhaustein), [@taartspi](https://github.com/taartspi), [@eitch](https://github.com/eitch), [@fdelporte](https://github.com/fdelporte).

All changes: https://github.com/Pi4J/pi4j/compare/3.0.2...3.0.3

### 2025-05-20 - V3.0.2

* Board model can now be forced to allow the use of Pi4J on other/unrecognized boards. See [Overriding the Detected Board](/documentation/board-info/#overriding-the-detected-board) for more info.
* `BoardInfoHelper.usesRP1()` has been improved as more boards use this RP1 (5, 500, Compute 5), and even more are expected in the future.
* [Issue #455](https://github.com/Pi4J/pi4j/issues/455): GpioDDigitalInput may never start monitoring line events. Fixed by simplifying and improving the wait for the input listener loop to exit on shutdown.
* [APIdia badge and link](https://apidia.net/mvn/com.pi4j/pi4j) added to README.md
* [Pull request #461](https://github.com/Pi4J/pi4j/pull/461): Removal in the core code of the SpiChipSelect to enforce a PiGpio limitation of the values 0, 1, or 2. 

Thanks to contributions by [@ylexus](https://github.com/ylexus), [@taartspi](https://github.com/taartspi), [@eitch](https://github.com/eitch), [@fdelporte](https://github.com/fdelporte).

All changes: https://github.com/Pi4J/pi4j/compare/3.0.1...3.0.2

### 2025-03-24 - V3.0.1

This is the first release of Pi4J that requires Java runtime 21 or higher. Check the blog post [Pi4J welcomes Java 21](/blog/2025/20250211-welcome-java-21/) to understand why we needed this change to prepare the project for the future...

Because of a last-minute change to improve the detection of Raspberry Pi 5, 500, and Compute 5, **release 3.0.0 has been skipped**.

* Bump the Java version to 21 and update many dependencies, such as the Maven plugin.
* Added JNA dependency (needed for Java 21).
* Added Maven wrapper.
* Improved lifecycle shutdown handling for registry elements: Updated the `Lifecycle` interface to clarify shutdown behavior and added tests to ensure proper element recreation after shutdown. These enhancements make the shutdown process more robust and intuitive.
* Issue [#308](https://github.com/Pi4J/pi4j/discussions/308): Remove serial support from Pi4J. All serial methods are marked as `@Deprecated(forRemoval = true)`. We advise using [jSerialComm](https://fazecast.github.io/jSerialComm/) for all serial communication.
* Pull request [#438](https://github.com/Pi4J/pi4j/pull/438): Extra unit test for shutdown and re-creation of a DigitalInput.
* Issue [#439](https://github.com/Pi4J/pi4j/issues/439): Allow Specifying GPIO Chip for GpioDContext. For more info on how to use, see [Specifying the GPIO Chip](/documentation/providers/gpiod/).
* Pull request [#449](https://github.com/Pi4J/pi4j/pull/449): Fixes a minor bug in DigitalOutput where pulseAsync ignored the given state and always pulsed high.
* Pull request [#452](https://github.com/Pi4J/pi4j/pull/452): PWM linuxfs failed if the first interface call was off().
* Pull request [#453](https://github.com/Pi4J/pi4j/pull/453) for issue [#296](https://github.com/Pi4J/pi4j/discussions/296): Generic BoardModels (with and without RP1) have been added, with a new method `BoardInfoHelper.current().setBoardModel(BoardModel.GENERIC);` to make it possible to **use Pi4J on other types of boards**, see [Overriding the Detected Board](https://www.pi4j.com/documentation/board-info/#overriding-the-detected-board). The goal of the Pi4J project is still to focus on the Raspberry Pi. However, this should allow testing the library's compatibility with other boards with similar architecture. We are excited to hear from the community about possible improvements to this approach.

Thanks to contributions by [@stefanhaustein](https://github.com/stefanhaustein), [@Haruka0522](https://github.com/Haruka0522), [@mpilone](https://github.com/mpilone), [@dariuszzbyrad](https://github.com/dariuszzbyrad), [@taartspi](https://github.com/taartspi), [@eitch](https://github.com/eitch), [@fdelporte](https://github.com/fdelporte).

All changes: https://github.com/Pi4J/pi4j/compare/2.8.0...3.0.1

## V2

Requires Java 11, see [What's New in V2](/about/info-v2/) for more info.

### 2025-01-28 - V2.8.0

* Several code and JavaDoc improvements by adding the checkstyle plugin.
* Improvements in loading the Mock providers to build and test Pi4J on a Raspberry Pi. 
* Issue [#421](https://github.com/Pi4J/pi4j/issues/421): Unable to detect board type. Several improvements have been integrated in the board detection to prevent errors when reading the board code. 
* Added to `BoardModel`:
  * Issue [#406](https://github.com/Pi4J/pi4j/issues/406): Old boards not auto detected. Missing codes have been added for Model 1 boards.
  * The Raspberry Pi Compute 5. Only the board code `c04180` for the 4Gb has been confirmed by Jeff Geerling. The other types are not documented yet. We assume they are `a04180`, `b04180`, and `d04180`, similar to the Compute 4, but will adjust whenever more info is available.
  * The Raspberry Pi 500 with the board code `d04190`, again confirmed by Jeff who received an evaluation device.
  * The Raspberry Pi 5 with 16GB memory with the board code `e04171` (thanks again Jeff).
* Added to `BoardReading`:
  * Pull request [#432](https://github.com/Pi4J/pi4j/pull/432): Add Support for Throttled State Parsing and Retrieval
* Improvements in the LinuxFS provider (for Raspberry Pi 5):
  * Pull Request [#433](https://github.com/Pi4J/pi4j/pull/433): Enhance LinuxFsI2CBus validation with detailed exception messages and comprehensive Javadocs.
  * Pull Request [#434](https://github.com/Pi4J/pi4j/pull/434): Add SPI support in LinuxFS. No `sudo` is needed to use SPI.

Thanks to contributions by [@mpilone](https://github.com/mpilone), [@cniesen](https://github.com/cniesen), [@geerlingguy](https://github.com/geerlingguy), [@dariuszzbyrad](https://github.com/dariuszzbyrad), [@taartspi](https://github.com/taartspi), [@eitch](https://github.com/eitch), [@fdelporte](https://github.com/fdelporte).

Special thanks to [Dariusz Zbyrad](https://github.com/dariuszzbyrad) for joining the project and improving the Maven builds with a wrapper for more consistency, for example, in the [pi4j-example-devices repository](https://github.com/Pi4J/pi4j-example-devices), and other contributions. And also special thanks to [Mike Pilone](https://github.com/mpilone) for the initial work for LinuxFS SPI.

All changes: https://github.com/Pi4J/pi4j/compare/2.7.0...2.8.0

### 2024-10-03 - V2.7.0

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

### 2024-07-29 - V2.6.1

This is a minor bug fix release to allow a smoother integration in a Spring Boot Starter by allowing to run on PC for testing without initialization errors and with reduced logging of the I2C Mock plugin.

* [Issue #354](https://github.com/Pi4J/pi4j/issues/354): Gracefully handle UnsatisfiedLinkError on newAutoContext when not running on a Raspberry Pi, for instance, when testing on Windows or macOS.
* Clean up of logs in `MockI2C.java`.

All changes: https://github.com/Pi4J/pi4j/compare/2.6.0...2.6.1

### 2024-04-29 - V2.6.0

* New hardware PWM provider added to the GpioD plugin, see: 
  * [Blog: PWM Hardware Support on RPi5](https://pi4j.com/blog/2024/20240423_pwm_rpi5/).
  * [Documentation: I/O Examples: Pulse Width Modulation (PWM)](https://pi4j.com/documentation/io-types/pwm/).
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

### 2024-03-18 - V2.5.1

Sorry! Because of a configuration error, the wrong native code is included in 2.5.0 for the new GpioD Provider. But [thanks to the lightning fast action](https://github.com/Pi4J/pi4j/commit/6ac458ec2d9b38a20b2195f4ecc03a65fbdebff7) of [Robert von Burg](https://github.com/eitch) we have a fixed version for you to enjoy :-)

All changes: https://github.com/Pi4J/pi4j/compare/2.5.0...2.5.1

### 2024-03-18 - V2.5.0

With over 100 commits from multiple branches, this is a major release with many improvements! With many thanks to the core team ([Robert von Burg](https://github.com/eitch), [Tom Aarts](https://github.com/taartspi)), and a major addition of [Alexander Liggesmeyer](https://github.com/alex9849), Pi4J is again lifted to a higher level!

You can find out [more about Alexander in this blog post](/blog/2024/20240318_interview_alexander_liggesmeyer/).

{{% notice warning %}}
The new GpioD Provider needs the latest Raspberry Pi OS version (`Debian GNU/Linux 12 (bookworm)`).
{{% /notice %}}

#### Changes in 2.5.0

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

#### Known Issue

* _java.io.IOException: Remote I/O error java.base/java.io.RandomAccessFile.writeBytes(Native Method). Using linuxfs-i2c, dependent upon i2c operations this exception can occur_: If the program initially uses read or write, and later uses readRegister or writeRegister there is no exception. However, if the program initially uses readRegister or writeRegister subsequent write or read may encounter this exception. For more info and the temporary fix, check [#335](https://github.com/Pi4J/pi4j/issues/335).

### 2023-10-24 - V2.4.0

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

### 2023-02-06 - V2.3.0

* Improvements for PIGPIO.gpioCfgInterfaces by [@bwaldvogel](https://github.com/bwaldvogel).
* New i2c interface to support multibyte register address by [@taartspi](https://github.com/taartspi).
* Fix in LinuxFsI2C byte array offset by [@harlanhu](https://github.com/harlanhu).
* Remove unused JNA references by [@taartspi](https://github.com/taartspi).

All changes: https://github.com/Pi4J/pi4j/compare/2.2.1...2.3.0

### 2022-10-17 - V2.2.1

Multiple fixes by [@taartspi](https://github.com/taartspi):

* Better error message when mixing 32- and 64-bit artifacts
* SPI improvements:
  * Add missing initialization in constructor
  * Track weather the user set the mode or bus config values to improve the use of SPI flags

All changes: https://github.com/Pi4J/pi4j/compare/2.2.0...2.2.1

### 2022-08-30 - V2.2.0

What an amazing achievement! No major issues were found in the previous release, but several small fixes were added by more people than ever before in the Pi4J-history. This is a real confirmation of the openness of this project and how a community can work together to further improve a project. 

A big thank you to everyone who experimented with Pi4J, took part in the discussions, filed an issue, created a merge request, added examples,...!

#### New example implementations

Thanks to the work of FHNW students and @taartspi, the list of available example implementations has become larger and larger. We even moved them to their own section of this documentation website! Take a look at [Example implementations](/examples/) if you need a quick-start to use a buzzer, camera, LED strip, TCA9548, MCP4725,... or any of the other examples.

#### Changes in V2.2.0

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

## V1

Up till version 1.3.0 requires Java 8, while version 1.4.0 requires Java 11. See [Info about V1](/about/info-v1/) for more info.