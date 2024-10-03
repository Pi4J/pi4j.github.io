---
title: Pi4J Operating System
weight: 37
tags: ["Pi4J OS"]
aliases:
  - /getting-started/crowpi/crowpi-os
  - /getting-started/crowpi/crowpi-os/
---

Yes, Raspberry Pi OS is great! And we made if even more awesome by adding some "goodies" for Java developers! So, to be clear, Pi4J OS is not yet another OS. It's the official Raspberry Pi OS, with additional tools and preconfigurations to make it the ideal OS for any Java developer who wants to use a Raspberry Pi.

{{% notice tip %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-os](https://github.com/Pi4J/pi4j-os)
{{% /notice %}}

## For Raspberry Pi 3 and 4

{{% notice warning %}}
Pi4j OS doesn't work on the Raspberry Pi 5.
{{% /notice %}}

Because of changes in the Raspberry Pi Operating System related to the release of the Raspberry Pi 5, the Pi4J OS is currently only compatible with the Raspberry Pi 3 and 4.

For the Raspberry Pi 5, you can achieve the same kind of features by starting with a standard installation as [described here](https://www.raspberrypi.com/software/). After starting the Raspberry Pi, you can install Java and everything you need to build Pi4J on the Raspberry Pi, using the following script:

```shell
#!/bin/bash -e
sudo raspi-config nonint do_i2c 0
sudo raspi-config nonint do_ssh 0
sudo raspi-config nonint do_serial_hw 0
sudo raspi-config nonint do_serial_cons 1
sudo raspi-config nonint do_onewire 0
sudo systemctl disable hciuart
echo "dtoverlay=disable-bt" | sudo tee -a /boot/firmware/config.txt

sudo apt install -y i2c-tools vim git java-common libxi6 libxrender1 libxtst6
curl -s "https://get.sdkman.io" | bash
source .bashrc
sdk install maven

mkdir -p ~/Downloads
cd ~/Downloads
wget https://cdn.azul.com/zulu/bin/zulu21.34.19-ca-jdk21.0.3-linux_arm64.deb
sudo dpkg -i zulu21.34.19-ca-jdk21.0.3-linux_arm64.deb
```

You can execute all this with one script using the following command:

```shell
curl -s "https://raw.githubusercontent.com/eitch/pi4j-test/develop/src/assembly/setup.sh" | bash
```

## Additional Features on top of Raspberry Pi OS

This project provides pre-built versions of OS images with all you need to develop 100% pure Java applications for specific Raspberry Pi setups. They are based on the latest official [Raspberry Pi OS](https://www.raspberrypi.org/software/) and are automatically built using Packer. 

By using these images, you will get:

* Preconfigured locale (en_US), keyboard (US) and timezone (Europe/Zurich).
* Preconfigured wireless country (Switzerland) by default.
* Remote management via `SSH` and `VNC` enabled by default.
* Preinstalled [OpenJDK 17](https://openjdk.java.net) with latest [JavaFX 20](https://gluonhq.com/products/javafx/).
* Starter script to launch JavaFX-apps in DRM (aka kiosk-mode).
* Preconfigured `/boot/config.txt` supporting all components out of the box.
* Dynamic wallpaper showing Ethernet/WLAN address and hostname.
* User account `pi`, password `pi4j`.
  * You have to set the corresponding preferences in Raspberry Pi Imager.
* Default WLAN connection.
  * Setup a hotspot, for example on your smartphone, and you’re ready to go.
    * SSID: `Pi4J-Spot`.
    * Password: `MayTheSourceBeWithYou!`.
  * Your laptop has to be in the same WLAN as the Rasperry Pi.

## Available Flavors

### Pi4J-Basic-OS

* Support for building 100% pure Java applications using [Pi4J](/), [JavaFX](https://openjfx.io)
* Can be used for all kind of Pi4J- , or JavaFX-projects
* Use [Pi4J Component Catalogue](/examples/components/) and corresponding [GitHub project](https://github.com/Pi4J/pi4j-example-components) to experiment with popular hardware components attached to your RaspPi.
* Use [RaspiFX template project](https://github.com/Pi4J/pi4j-template-javafx) to start your own JavaFX/Pi4J or plain Pi4J project

[Download latest release of Pi4J-Basic-OS Image](https://pi4j-download.com/latest.php?flavor=basic)

### Pi4J-CrowPi-OS

* All of Pi4J-Basic-OS
* Support for [CrowPi](https://www.elecrow.com/crowpi-compact-raspberry-pi-educational-kit.html)
* Comes with `lirc` preinstalled to run the IR receiver component
* Use [CrowPi template project](https://github.com/Pi4J/pi4j-example-crowpi) to start your CrowPi experiments

[Download latest release of Pi4J-CrowPi-OS](https://pi4j-download.com/latest.php?flavor=crowpi)

### Pi4J-Picade-OS

* All of Pi4J-Basic-OS
* Support for [Picade Console](https://shop.pimoroni.com/products/picade-console) and [Picade X HAT USB-C](https://shop.pimoroni.com/products/picade-x-hat-usb-c?variant=29156918558803)
* Use link:[FXGL template project] to start your Picade project (available soon)

[Download latest release of Pi4J-Picade-OS](https://pi4j-download.com/latest.php?flavor=picade)

## Table of content of the "Pi4J OS" section

{{% children depth="3" %}}
