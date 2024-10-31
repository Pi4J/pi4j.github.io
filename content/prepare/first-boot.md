---
title: The First Boot
weight: 17
---

## Update the System

Yes, even when you just created the SD Card with the latest OS provided by the Imager tool, it is possible that there are updates available. Run the following commands to make sure your system is fully up-to-date:

```shell
sudo apt update
sudo apt upgrade
```

## Configuration Changes

To use the Raspberry Pi for electronic experiments, we need to configure some of the settings. You can do these one-by-one with the `raspi-config` tool, but this is a full list of commands to do this for you:

```shell
#!/bin/bash -e
sudo raspi-config nonint do_i2c 0
sudo raspi-config nonint do_ssh 0
sudo raspi-config nonint do_serial_hw 0
sudo raspi-config nonint do_serial_cons 1
sudo raspi-config nonint do_onewire 0
sudo systemctl disable hciuart
echo "dtoverlay=disable-bt" | sudo tee -a /boot/firmware/config.txt
```

## Keep your Raspberry Pi up-to-date

It's a good idea to run the following commands from time to time to make sure the system makes use of all the latest improvements.

```shell
sudo apt update
sudo apt full-upgrade
```

Raspberry Pi OS is based on [Debian](https://www.debian.org/) - one of the largest Linux distributions. When running
these commands regularly, you will keep your installation up to date for the particular major Raspberry Pi OS
release you are using (e.g. Debian V9, aka Stretch). It will not update from one major release to another, for example, Stretch (V9) to Buster (V10).