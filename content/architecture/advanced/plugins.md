---
title: Plug-ins
---

The goal of Pi4J V.2 is to provide a solid base with all required "minimal functionality" while at the same time, promote third-party development and extensibility, thus enabling developers to build and maintain their extensions outside of the Pi4J core projects codebase. 

This will enable us to deliver a stable, fully tested framework as the number of features inside of Pi4J can be limited and support for specific I/O hardware can be provided with an extension for Pi4J.

More info about how this extensibility is achieved:

* Extensible I/O hardware [PROVIDERS](/documentation/providers/):  things like GPIO expanders, I2C bus expanders, GertBoard, add-on hardware shields, etc.
* Extensible SBC platforms [PLATFORMS](/documentation/platforms/):  the core project may only support Raspberry Pi, but the platform and libraries should be written to allow a third party to create plugins for alternate hardware platforms/boards.
* Extensible **plugins**.

Plugins are extensible service modules that interact with or augment the Pi4J infrastructure. The most common plugins are I/O Providers and Platforms. Other plugin examples could be a web app to view/control the Pi4J runtime state/status, some third-party observer to the Pi4J runtime state/status,...

Plugins are implemented as Java modules using [Service Provider Interfaces (SPI)](https://docs.oracle.com/javase/tutorial/sound/SPI-intro.html).

Plugins must declare their pluggable interface in their "module-info.java" config file.  Example from [the Raspberry plugin](https://github.com/Pi4J/pi4j/blob/master/plugins/pi4j-plugin-raspberrypi/src/main/java/module-info.java):

```java
module com.pi4j.plugin.raspberrypi {
    requires com.pi4j;

    exports com.pi4j.plugin.raspberrypi;
    exports com.pi4j.plugin.raspberrypi.platform;
    exports com.pi4j.plugin.raspberrypi.provider.gpio.digital;
    exports com.pi4j.plugin.raspberrypi.provider.pwm;
    exports com.pi4j.plugin.raspberrypi.provider.serial;
    exports com.pi4j.plugin.raspberrypi.provider.spi;
    exports com.pi4j.plugin.raspberrypi.provider.i2c;

    provides com.pi4j.extension.Plugin with RaspberryPiPlugin;
}
```


ServiceLoader overview by [Piotr Mińkowski](https://twitter.com/piotr_minkowski).

![Pi4J V.2 architecture](/assets/architecture/serviceloader-overview.jpg)