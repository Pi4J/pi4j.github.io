---
title: 'Features and testing'
weight: 45
---

## Feature/Component Status

The following tables outlines some of the current (high-level) features planned for V.2 release.  

| ARCHTECTURAL COMPONENTS | STATUS | PRIORITY |
| :---	| :---	| :--- |
| Runtime Context | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| I/O Registry | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| Platforms | <i class="fa fa-hourglass-half"></i> **Incomplete** | <i class="fa fa-arrow-circle-up"></i> HIGH |
| Providers | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| Dependency Injection | <i class="fa fa-flask"></i> In Research | <i class="fa fa-arrow-circle-up"></i> HIGH |

---

| CORE FEATURES | STATUS | PRIORITY |
| :---	| :---	| :--- |
| Remote I/O (via TCP) | <i class="fa fa-cogs"></i> InTesting |  <i class="fa fa-arrow-circle-up"></i> HIGH |
| Executor Service | <i class="fa fa-hourglass-half"></i> **Incomplete** |  <i class="fa fa-arrow-circle-up"></i> HIGH |
| GPIO Pulse | <i class="fa fa-hourglass-half"></i> **Incomplete** | <i class="fa fa-arrow-circle-up"></i> HIGH |
| GPIO Blink | <i class="fa fa-hourglass-half"></i> **Incomplete** | <i class="fa fa-arrow-circle-up"></i> HIGH |

---

| I/O PLUGINS | STATUS | PRIORITY |
| :---	| :---	| :--- |
| PiGpio GPIO Provider Plugin | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| PiGpio SPI Provider Plugin | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| PiGpio SERIAL Provider Plugin | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| PiGpio I2C Provider Plugin | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| PiGpio PWM Provider Plugin | <i class="fa fa-cogs"></i> In Testing | <i class="fa fa-arrow-circle-up"></i> HIGH |
| 	| 	|   |
| LinuxFX GPIO Provider Plugin | <i class="fa fa-hourglass-half"></i> Incomplete | <i class="fa fa-arrow-circle-down"></i> LOW |
| LinuxFX SPI Provider Plugin | <i class="fa fa-hourglass-half"></i> Incomplete | <i class="fa fa-arrow-circle-down"></i> LOW |
| LinuxFX SERIAL Provider Plugin | <i class="fa fa-hourglass-half"></i> Incomplete | <i class="fa fa-arrow-circle-down"></i> LOW |
| LinuxFX I2C Provider Plugin | <i class="fa fa-hourglass-half"></i> Incomplete | <i class="fa fa-arrow-circle-down"></i> LOW |
| 	| 	|   |
| WiringPi GPIO Provider Plugin | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-down"></i> LOW |
| WiringPi SPI Provider Plugin | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-down"></i> LOW |
| WiringPi I2C Provider Plugin | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-down"></i> LOW |
| WiringPi PWM Provider Plugin | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-down"></i> LOW |
| 	| 	|   |
| PiGpio Bitbang Serial | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-down"></i> LOW |
| PiGpio Bitbang I2C | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-down"></i> LOW |
| PiGpio Bitbang SPI | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-down"></i> LOW |

---

## Hardware Testing Status

The table below illustrates the testing progress on the various supported platforms/models.

As standard OpenJDK versions are not available for the ARMv6 these are considered to be low priority.

| PLATFORM/MODEL | [ARM](https://en.wikipedia.org/wiki/Raspberry_Pi#Specifications) | STATUS | PRIORITY |
| :---	| :---	| :--- | :--- |
| RaspberryPi - 4B | ARMv8 | <i class="fa fa-cogs"></i> In Testing; Preliminary Tests PASSED | <i class="fa fa-arrow-circle-up"></i> HIGH |
| 	| 	|   |    |
| RaspberryPi - 3A+ | ARMv8 | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-up"></i> HIGH |
| RaspberryPi - 3B+| ARMv8 | <i class="fa fa-cogs"></i> In Testing; Preliminary Tests PASSED | <i class="fa fa-arrow-circle-up"></i> HIGH |
| RaspberryPi - 3B | ARMv8 | <i class="fa fa-cogs"></i> In Testing; Preliminary Tests PASSED | <i class="fa fa-arrow-circle-up"></i> HIGH |
| 	| 	|   |    |
| RaspberryPi - ZeroW | ARMv6 | <i class="fa fa-times"></i> Not Supported | <i class="fa fa-arrow-circle-down"></i> LOW |
| RaspberryPi - Zero | ARMv6 | <i class="fa fa-times"></i> Not Supported | <i class="fa fa-arrow-circle-down"></i> LOW |
| 	| 	|   |    |
| RaspberryPi - 2B (v1.2) | ARMv8 | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-circle"></i> MEDIUM |
| RaspberryPi - 2B | ARMv7 | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-circle"></i> MEDIUM |
| RaspberryPi - 1B+ | ARMv6 | <i class="fa fa-times"></i> Not Supported | <i class="fa fa-arrow-circle-down"></i> LOW |
| RaspberryPi - 1A+ | ARMv6 | <i class="fa fa-times"></i> Not Supported | <i class="fa fa-arrow-circle-down"></i> LOW |
| RaspberryPi - 1B (Rev 2) | ARMv8 | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-circle"></i> MEDIUM |
| RaspberryPi - 1B (Rev 1) | ARMv7 | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-circle"></i> MEDIUM |
| RaspberryPi - 1A | ARMv6 | <i class="fa fa-times"></i> Not Supported | <i class="fa fa-arrow-circle-down"></i> LOW |
| 	| 	|   |    |
| RaspberryPi - CM3+ (Compute Module)  | ARMv8 | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-up"></i> HIGH |
| RaspberryPi - CM3 (Compute Module)  | ARMv8 | <i class="fa fa-hourglass-o"></i> Not Started | <i class="fa fa-arrow-circle-up"></i> HIGH |
| RaspberryPi - CM1 (Compute Module)  | ARMv6 | <i class="fa fa-times"></i> Not Supported | <i class="fa fa-arrow-circle-down /] LOW |

---
