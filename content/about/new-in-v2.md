---
title: 'What''s New (V2)'
taxonomy:
    category:
        - docs
visible: true
---

#### What's New in 2.0?

Pi4J version 2.0 brings with it many new features and an entirely new architecture that focuses on extensibility, simplified integration and a modern Java API including the following:

* Fluent APIs/Interfaces
* Immutable Runtime Context
* Extensible Provider/Platform/Plug-in Architecture
* Builder-patterns for creating new I/O instances
* Dependency Injection via Pi4J Annotations
* Well-documented source code
* Hardware PWM Support
* Remote I/O Support (via TCP/IP)
* Java 11

In addition to the features listed above, Pi4J version 2.0 also abandons the old WiringPi pin numbering scheme in favor of the more traditional and commonly used Broadcom pin numbering scheme.  This pin numbering scheme has been a source of confusion for a number of years, especially with beginners and is somewhat cumbersome to maintain as new Raspberry Pi models are introduces with differing or added GPIO pins.  Moving forward, Pi4J will only use the Broadcom (BCM) pin numbering scheme.  

The WiringPi project has now been deprecated (see [http://wiringpi.com/wiringpi-deprecated/](http://wiringpi.com/wiringpi-deprecated/)).   Pi4J version 2.0 will no longer be based on WiringPi and has moved to using the PIGPIO library ([http://abyz.me.uk/rpi/pigpio/](http://abyz.me.uk/rpi/pigpio/)) internally for low level integation.   With this move, we will also support the remote I/O features (via TCP socket) offered by the PIGPIO daemon ([http://abyz.me.uk/rpi/pigpio/pigpiod.html](http://abyz.me.uk/rpi/pigpio/pigpiod.html)).  

---

#### What are the differences compared to V1?

Starting with the Pi4J 2.0 builds, the Pi4J project is prioritizing focus on providing Java programs access, control and communication with the core I/O capabilities of the Raspberry Pi platform. Earlier versions of Pi4J were perhaps too ambitious in scope and that led to significant project bloat to the point that the project was becoming unsustainable. The goal moving forward is to limit scope to that of the raw I/O capabilities of the Raspberry Pi platform and provide timely updates and releases for bug fixed and new RaspberryPi model introductions. Reducing the scope of the project should better serve the Java community for basic I/O access by reducing complexity.

The following features have been removed from the Pi4J library:

* **IO Expanders** -- IO expansion is still supported but concrete implementations should be provided outside the core Pi4J core project such that they can be maintained and extended independently.

* **Other Platforms** -- Other platforms such as Odroid, BananaPi, NanoPi, OrangePi, etc. have been removed and will no longer be supported. The challenge with supporting these additional platforms is that Pi4J depends on the underlying WiringPi project and WiringPi ports for these other platforms is not well supported by the various SoC vendors or community. The various WiringPi ports for these other platforms are also inconsistent causing inconsistent features and functionality of Pi4J. Additionally, regression testing of bug fixes and new features in Pi4J is compounded with each additional supported platform.

* **Components & Devices** -- Pi4J originally provided higher level interfaces for components and devices that provided an abstraction layer between real world devices (things) and lower-level I/O interfaces. While a noble goal, unfortunately this part of the project never received the attention and time that it deserved and never gained much adoption by the community. We are removing these to allow Pi4J to focus solely on the raw I/O supported by the Raspberry Pi platform.

---