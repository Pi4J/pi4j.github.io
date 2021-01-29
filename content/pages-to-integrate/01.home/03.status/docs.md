---
title: 'Project Status'
taxonomy:
    category:
        - docs
visible: true
---

#### Project Status/Summary

Version 2.0 of Pi4J is finally starting to come together and is _almost_ ready for some real-world BETA testing.  Significant progress has been made on the general architecture and primary user-facing interfaces.  Pi4J V.2 is a complete re-write and **does not maintain API compatibility** with previous versions.  It is not intended to be a drop-in replacement for previous versions of Pi4J.  Pi4J V.2 is a completely new design bringing modern conventions, development practices, extensibility support and simplified integration experience for Pi4J users.

!! Pi4J Version 2.0 is still considered **EXPERIMENTAL** at this point.  While many parts of the project are working, there are still a number of areas that require further development and certain APIs are subject to change without notice.  A significant portion of the code is presently undocumented and hardware integration testing is incomplete.  It is not recommended to use Pi4J V.2 in any production workload at this time.

---

##### Feature/Component Status

The following tables outlines some of the current (high-level) features planned for V.2 release.  Please note that some of these features may get deferred and not incuded in the first release.

| ARCHTECTURAL COMPONENTS | STATUS | PRIORITY |
|---	|---	|--- |
| Runtime Context | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
| I/O Registry | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
| Platforms | [fa=fa-hourglass-half /] **Incomplete** | [fa=fa-arrow-circle-up /] HIGH |
| Providers | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
| Dependency Injection | [fa=fa-flask /] In Research | [fa=fa-arrow-circle-up /] HIGH |

---

| CORE FEATURES | STATUS | PRIORITY |
|---	|---	|--- |
| Remote I/O (via TCP) | [fa=fa-cogs /] InTesting |  [fa=fa-arrow-circle-up /] HIGH |
| Executor Service | [fa=fa-hourglass-half /] **Incomplete** |  [fa=fa-arrow-circle-up /] HIGH |
| GPIO Pulse | [fa=fa-hourglass-half /] **Incomplete** | [fa=fa-arrow-circle-up /] HIGH |
| GPIO Blink | [fa=fa-hourglass-half /] **Incomplete** | [fa=fa-arrow-circle-up /] HIGH |

---

| I/O PLUGINS | STATUS | PRIORITY |
|---	|---	|--- |
| PiGpio GPIO Provider Plugin | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
| PiGpio SPI Provider Plugin | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
| PiGpio SERIAL Provider Plugin | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
| PiGpio I2C Provider Plugin | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
| PiGpio PWM Provider Plugin | [fa=fa-cogs /] In Testing | [fa=fa-arrow-circle-up /] HIGH |
|---	|---	|--- |
| LinuxFX GPIO Provider Plugin | [fa=fa-hourglass-half /] Incomplete | [fa=fa-arrow-circle-down /] LOW |
| LinuxFX SPI Provider Plugin | [fa=fa-hourglass-half /] Incomplete | [fa=fa-arrow-circle-down /] LOW |
| LinuxFX SERIAL Provider Plugin | [fa=fa-hourglass-half /] Incomplete | [fa=fa-arrow-circle-down /] LOW |
| LinuxFX I2C Provider Plugin | [fa=fa-hourglass-half /] Incomplete | [fa=fa-arrow-circle-down /] LOW |
|---	|---	|--- |
| WiringPi GPIO Provider Plugin | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-down /] LOW |
| WiringPi SPI Provider Plugin | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-down /] LOW |
| WiringPi I2C Provider Plugin | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-down /] LOW |
| WiringPi PWM Provider Plugin | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-down /] LOW |
|---	|---	|--- |
| PiGpio Bitbang Serial | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-down /] LOW |
| PiGpio Bitbang I2C | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-down /] LOW |
| PiGpio Bitbang SPI | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-down /] LOW |

---

##### Hardware Testing Status

The table below illustrates the testing progress on the various supported platforms/models.

As standard OpenJDK versions are not available for the ARMv6 these are considered to be low priority.

| PLATFORM/MODEL | [ARM](https://en.wikipedia.org/wiki/Raspberry_Pi#Specifications) | STATUS | PRIORITY |
|---	|---	|--- |
| RaspberryPi - 4B | ARMv8 | [fa=fa-cogs /] In Testing; Preliminary Tests PASSED | [fa=fa-arrow-circle-up /] HIGH |
|---	|---	|--- |
| RaspberryPi - 3A+ | ARMv8 | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-up /] HIGH |
| RaspberryPi - 3B+| ARMv8 | [fa=fa-cogs /] In Testing; Preliminary Tests PASSED | [fa=fa-arrow-circle-up /] HIGH |
| RaspberryPi - 3B | ARMv8 | [fa=fa-cogs /] In Testing; Preliminary Tests PASSED | [fa=fa-arrow-circle-up /] HIGH |
|---	|---	|--- |
| RaspberryPi - ZeroW | ARMv6 | [fa=fa-times /] Not Supported | [fa=fa-arrow-circle-down /] LOW |
| RaspberryPi - Zero | ARMv6 | [fa=fa-times /] Not Supported | [fa=fa-arrow-circle-down /] LOW |
|---	|---	|--- |
| RaspberryPi - 2B (v1.2) | ARMv8 | [fa=fa-hourglass-o /] Not Started | [fa=fa-circle /] MEDIUM |
| RaspberryPi - 2B | ARMv7 | [fa=fa-hourglass-o /] Not Started | [fa=fa-circle /] MEDIUM |
| RaspberryPi - 1B+ | ARMv6 | [fa=fa-times /] Not Supported | [fa=fa-arrow-circle-down /] LOW |
| RaspberryPi - 1A+ | ARMv6 | [fa=fa-times /] Not Supported | [fa=fa-arrow-circle-down /] LOW |
| RaspberryPi - 1B (Rev 2) | ARMv8 | [fa=fa-hourglass-o /] Not Started | [fa=fa-circle /] MEDIUM |
| RaspberryPi - 1B (Rev 1) | ARMv7 | [fa=fa-hourglass-o /] Not Started | [fa=fa-circle /] MEDIUM |
| RaspberryPi - 1A | ARMv6 | [fa=fa-times /] Not Supported | [fa=fa-arrow-circle-down /] LOW |
|---	|---	|--- |
| RaspberryPi - CM3+ (Compute Module)  | ARMv8 | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-up /] HIGH |
| RaspberryPi - CM3 (Compute Module)  | ARMv8 | [fa=fa-hourglass-o /] Not Started | [fa=fa-arrow-circle-up /] HIGH |
| RaspberryPi - CM1 (Compute Module)  | ARMv6 | [fa=fa-times /] Not Supported | [fa=fa-arrow-circle-down /] LOW |

---
