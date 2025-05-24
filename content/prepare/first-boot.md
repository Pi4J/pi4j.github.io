---
title: The First Boot
weight: 17
---

Put the SD Card with the operating system into the Raspberry Pi, connect a keyboard, mouse, and screen, and power it up!

{{% notice tip %}}
If you configured the login, password, WiFi, and SSH settings in the "Use OS customisation?" part of the Imager tool, you can connect to the Raspberry Pi from another PC via SSH with the username and hostname you filled in: `ssh USERNAME@HOSTNAME.local`.
{{% /notice %}}

## Update the System

Yes, even when you just created the SD Card with the latest OS provided by the Imager tool, it is possible that there are updates available. 

{{% notice tip %}}
Everything on this (and the next) page can be done with one command! It will download a script from the Pi4J OS GitHub project and execute all the different steps automatically. 

Execute this: `shell
curl -sL https://raw.githubusercontent.com/Pi4J/pi4j-os/main/script/prepare-for-java.sh | bash`.
{{% /notice %}}

Run the following commands in the terminal to make sure your system is fully up-to-date. The output in this example will most probably be different on your system:

```shell
$ sudo apt update
Hit:1 http://deb.debian.org/debian bookworm InRelease
Get:2 http://deb.debian.org/debian-security bookworm-security InRelease [48.0 kB]
...
13 packages can be upgraded. Run 'apt list --upgradable' to see them.

$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
...
Need to get 275 MB of archives.
After this operation, 9,003 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

## Configuration Changes

To use the Raspberry Pi for electronic experiments, we need to configure some settings. You can do these one-by-one with the `raspi-config` tool, but this is a full list of commands to do this for you. Copy the whole block, and paste it in the terminal.

```shell
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