---
title: Write OS to SD card
weight: 16
---

The SD card will hold the operating system. On the Raspberry Pi website, [on the download page, you can
find the Imager tool](https://www.raspberrypi.org/software/). Select the version for your computer, download, and install it.

![Imager download](/assets/prepare/setup/website-download.png)

Start the Imager and follow these steps:

1. Put the SD Card in your computer
1. **Device**: Select your type of board, click "Next"
1. **OS**: Select "Raspberry Pi OS (64-bit)" (or 32-bit for an older board), click "Next"
1. **Storage**: Select the SD card, click "Next"
1. **Hostname**: Fill in a name for your board, click "Next"
1. **Localisation**: Select your city, time zone, and keyboard layout, click "Next"
1. **User**: Fill in a username and password, click "Next"
1. **Wi-Fi**: Fill in the name of your Wi-Fi network, and the password, click "Next"
1. **Remote access**: Enable SSH so you can access the board remotely, click "Next"
1. **Raspberry Pi Connect**: Enable this if you want to able to access the board via Raspberry Pi Connect, click "Next"
1. **Writing**: Now you get a short overview of your choices, click "Write"
1. Confirm you want to erase all data from the SD card. Double check you have put the right SD card in your computer and you selected that one in the **Storage** step. Click "I understand, erase and write".
1. Wait until the writing is finished...
1. You can now take the SD Card out of your computer, and put it in the Raspberry Pi

{{< gallery >}}
{{< figure link="/assets/prepare/setup/imager-device.png" caption="Selecting the device" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-os.png" caption="Selecting the operating system" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-storage.png" caption="Selecting the SD card" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-hostname.png" caption="Specify the hostname" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-localisation.png" caption="Specify the localization settings" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-user.png" caption="Specify the user name and password" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-wifi.png" caption="Specify the Wi-Fi settings" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-ssh.png" caption="Enable SSH" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-connect.png" caption="Enable Connect if needed" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-write-check.png" caption="Double check before writing" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-write-confirm.png" caption="Confirm to write" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-writing.png" caption="Writing progress" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/prepare/setup/imager-done.png" caption="Done" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}
