---
title: Write OS to SD card
weight: 16
---

The SD card will hold the operating system. On the Raspberry Pi website, [on the download page, you can
find the Imager tool](https://www.raspberrypi.org/software/). Select the version for your computer, download, and install it.

![Imager download](/assets/getting-started/setup/download-imager.png)

Start the Imager and follow these steps:

1. Put the SD Card in your computer
1. Click "Choose Device" and select your type of board
1. Click "Choose OS" > "Raspberry Pi OS (64-bit)" (or 32-bit for an older board)
1. Click "Choose Storage" and select your SD card
1. Click "Next" 
1. In the "Use OS customisation?" screen, click "Edit Settings" 
1. In "General", fill in a name for your board, login, password, wifi settings, etc.
1. In "Services", enable SSH with password authentication
1. In "Options" you can disable telemetry.
1. Back in the "Use OS customisation?" screen, click "Yes"
1. Confirm with "Yes" that all data on the SD Card can be overwritten
1. Wait until "Writing" and "Verifying" are finished
1. You can now take the SD Card out of your computer, and put it in the Raspberry Pi

{{< gallery >}}
{{< figure link="/assets/getting-started/setup/imager-start.png" caption="Imager start screen" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-choose-device.png" caption="Selecting the device" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-os.png" caption="Selecting the operating system" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-sd.png" caption="Selecting the SD card" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-customisation-start.png" caption="Customisation start screen" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-customisation-general.png" caption="Customisation: General settings" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-customisation-services.png" caption="Customisation: Services" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-customisation-options.png" caption="Customisation: Options" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-writing.png" caption="Writing to the SD card" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-verifying.png" caption="Verifying the SD card" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/setup/imager-done.png" caption="Imager is finished" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}
