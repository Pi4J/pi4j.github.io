---
title: Prepare SD with Pi4J OS
weight: 10
tags: ["Pi4J OS"]
---

To prepare an SD-card with one of these flavors, download the latest build from [pi4j.com/download](https://pi4j.com/download/) and follow the steps described in ["Set up a new Raspberry Pi](/getting-started/set-up-a-new-raspberry-pi/), but instead of selecting one of the OS's predefined in the Imager tool, select "Choose OS > Use custom", and selected the downloaded file.

## Install the Raspberry Pi Imager

The official Imager Tool can be downloaded directly from the [Raspberry Pi website](https://www.raspberrypi.org/software/).
This simple tool works on all common operating systems and can be installed very easily with just a few keystrokes.
More detailed instructions for installation are also available on the homepage of the Raspberry Pi website or here
on ["Set up a new Raspberry Pi"](/getting-started/set-up-a-new-raspberry-pi/).

## Download the Pi4J OS Image

The image for the Pi4J OS which contains the operating system for the Raspberry Pi can be obtained directly from the
[pi4j.com/download/](https://pi4j.com/download/). 

{{< gallery >}}
{{< figure link="/assets/pi4j-os/download-latest.png" caption="Download Pi4J OS Image" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}

After the download, unzip the .zip archive. Everything is now ready for the next step!

## Writing the image to an SD card

{{% notice warning %}}
When the image is written to the SD card, all data that is still on it will be overwritten!
{{% /notice %}}

First, the SD card must be available as a drive on the computer. There are different possibilities for this.
Card readers are just as suitable as USB adapters. The Raspberry Pi Imager tool is now started. First, the operating
system must be selected. Press the button "Choose OS".

At the bottom of the list, select "Use custom". In the selection dialog, select the previously downloaded and unzipped
Pi4J OS img-file.

{{< gallery >}}
{{< figure link="/assets/pi4j-os/selectos-raspberrypi-imager.png" caption="Choose OS in Imager Tool" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/pi4j-os/usecustom-raspberrypi-imager.png" caption="Use custom in Imager Tool" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}

The second step is to add a user and password via the preferences-button.

* Username: pi
* Password: pi4j

{{< gallery >}}
{{< figure link="/assets/pi4j-os/imager-preferences.png" caption="Setting Username and Password " caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}

All the other settings should be left as they are.


The third step is to select the SD card. To do this, press the button "Choose storage". It automatically
shows you only the available removable media such as USB sticks or SD cards. It is now very important to select the correct entry in order to avoid unwanted data loss. On Windows, the drive letter that is actually affected is shown under the data carrier, so that this can be easily checked in Explorer. In case of doubt, however, simply unplug the data carrier with important media beforehand so that nothing can happen.

Everything is ready to write the image to the SD card. The process can be started by pressing the "Write" button.
Another confirmation dialog follows before the SD card is finally overwritten. Writing the image to the SD card can
take a few minutes which is completely normal. As soon as the process is completed, a message appears. The SD card can
now be removed from the computer.

## Insert the SD card into the Raspberry Pi

To use the new operating system with your Raspberry Pi, insert the prepared SD card. Power up the device and it will probably restart a few times, after which it's ready to be used.

### Using Pi4J CrowPi OS

When using a CrowPi, the 4 retaining screws may have to be loosened. These can be found here:

After loosening the screws, the Raspberry Pi can be lifted. At most, a few cables must be unplugged. The SD card slot
can now be found on the underside. Here the SD card with the contact surfaces can be inserted in the Raspberry Pi. The
slot is marked again in the picture below. As soon as the SD card is inserted, the Raspberry Pi can be correctly installed
in the CrowPi and any cables that may have been disconnected can be plugged in again. As soon as everything is back in
its place, the CrowPi can be connected to the power.

Before the CrowPi is put into operation, it should be checked again whether all 3 cables are connected to the Raspberry Pi.
The HDMI adapter on the left, the USB cable on the lower side and the GPIO ribbon cable on the right should be connected.
These mandatory cables are framed with red circles in the next graphic. Optionally, a keyboard and mouse can be connected
via USB, which is marked with a pink circle below:

{{< gallery >}}
{{< figure link="/assets/pi4j-os/crowpi-raspberrypi-screws.jpg" caption="Raspberry Pi in the CrowPi with marked screws" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/pi4j-os/crowpi-raspberrypi-sdslot.jpg" caption="Raspberry Pi SD card slot" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/pi4j-os/crowpi-cables.jpg" caption="Raspberry Pi cables" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}

## Establish the network connection

Only the network connection of the freshly started Raspberry Pi still has to be made manually. Otherwise, all settings
are already optimally contained in the image. Now there are a few options for the network connection:

* Connection via WLAN
* Connection via Ethernet cable (DHCP)
* Connection via Ethernet cable directly to the computer

The easiest way to make the settings is to use the mouse and keyboard connected to the Raspberry Pi. Setting up via WLAN
is explicitly recommended, as it can be used in almost any environment and works great with the hotspot function on your
own smartphone even when you are out and about.

In the following, only the connection via WLAN is described, however, if there is expertise in this area, a connection
via cable can also be established.

### Establishing a WLAN connection

To connect via wireless network, the two arrows on the icon on the desktop must be pressed on the top right, after which
you can select the desired network. Then enter the corresponding password in the dialog for secure connections.
A few seconds after the connection, the desktop background image will automatically update and display the assigned IP
address. An Ethernet address is also visible on the images. This means that at the moment of the recording there was also
an Ethernet cable connected to the Raspberry Pi. Now that we have a network connection, we are ready to set
up the development environment as the next step.

{{< gallery >}}
{{< figure link="/assets/pi4j-os/crowpi-selectwlan.jpg" caption="Select WLAN" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/pi4j-os/crowpi-wlanpassword.jpg" caption="WLAN password" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/pi4j-os/crowpi-background-ipaddresses.jpg" caption="Background with IP addresses" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}