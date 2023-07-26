---
title: Pi4J Operating System
weight: 37
tags: ["Pi4J OS"]
aliases:
  - /getting-started/crowpi/crowpi-os
  - /getting-started/crowpi/crowpi-os/
---

Yes, Raspberry Pi OS is great! And we made if even more awesome by adding some "goodies" for Java developers! So, to be clear, Pi4J OS is not yet another OS. It's the official Raspberry Pi OS, with additional tools and preconfigurations to make it the ideal OS for any Java developer who wants to use a Raspberry Pi.

### Available Flavors

#### Pi4J-Basic-OS

* Support for building 100% pure Java applications using https://pi4j.com[Pi4J], https://openjfx.io[JavaFX]
* can be used for all kind of Pi4J- , or JavaFX-projects
* use https://pi4j.com/examples/components/[Pi4J Component Catalogue] and corresponding https://github.com/Pi4J/pi4j-example-components[GitHub project] to experiment with popular hardware components attached to your RaspPi.
* use https://github.com/Pi4J/pi4j-template-javafx[RaspiFX template project] to start your own JavaFX/Pi4J or plain Pi4J project

[Download latest release of Pi4J-Basic-OS Image](https://pi4j-download.com/latest.php?flavor=basic)

#### Pi4J-CrowPi-OS

* all of Pi4J-Basic-OS
* support for https://www.elecrow.com/crowpi-compact-raspberry-pi-educational-kit.html[CrowPi]
* comes with `lirc` preinstalled to run the IR receiver component
* use https://github.com/Pi4J/pi4j-example-crowpi[CrowPi template project] to start your CrowPi experiments

[Download latest release of Pi4J-CrowPi-OS](https://pi4j-download.com/latest.php?flavor=crowpi)

#### Pi4J-Picade-OS

* all of Pi4J-Basic-OS
* support for https://shop.pimoroni.com/products/picade-console[Picade Console] and https://shop.pimoroni.com/products/picade-x-hat-usb-c?variant=29156918558803[Picade X HAT USB-C]
* use link:[FXGL template project] to start your Picade project (available soon)

[Download latest release of Pi4J-Picade-OS](https://pi4j-download.com/latest.php?flavor=picade)

### Table of contents of the "Pi4J OS" section

{{% children depth="3" %}}
