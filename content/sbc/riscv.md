---
title: "Setting up Pi4J for RISC-V"
weight: 40
tags: ["RISC-V"]
---

[RISC-V](https://en.wikipedia.org/wiki/RISC-V) is an open, royalty-free instruction set architecture, and boards built around it are becoming more common as alternatives to ARM-based SBCs. This page collects what's needed to get Java and Pi4J running on RISC-V hardware.

{{% notice warning %}}
This page is a work in progress. Expect more tested boards and details in the near future...
{{% /notice %}}

## Tested boards

1. [Milk-V Mars](https://milkv.io/docs)

## Installing JDK 25+

There aren't many builds of Java for the RISC-V architecture yet, so we recommend installing it from the [Adoptium project](https://adoptium.net/temurin/releases):

```shell
sudo apt install -y wget apt-transport-https gpg
wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/adoptium.gpg > /dev/null
echo "deb https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
sudo apt update
sudo apt install temurin-25-jdk
```

## Board Details

### Milk-V Mars

1. Download the Ubuntu image from Canonical: [ubuntu-24.04.4-preinstalled-server-riscv64+jh7110.img.xz](https://cdimage.ubuntu.com/releases/noble/release/ubuntu-24.04.4-preinstalled-server-riscv64+jh7110.img.xz)
2. Flash the Ubuntu image to an SD card, as described in [Canonical's flashing guide](https://ubuntu.com/hardware/docs/boards/how-to/special_hardware/flash-images/#flash-images-to-a-microsd-card) (or use [Balena Etcher](https://etcher.balena.io/)).
3. Connect UART from your PC to the Milk-V Mars, following [Canonical's UART console instructions](https://ubuntu.com/hardware/docs/boards/how-to/ubuntu_supported/milk-v-mars/#uart-console).
4. Open the UART console on your PC and press any key when the message "Hit any key to stop autoboot" appears.
5. Run the following commands:

   ```shell
   sf probe
   load mmc 1:1 $kernel_addr_r /usr/lib/u-boot/starfive_visionfive2/u-boot-spl.bin.normal.out
   sf update $kernel_addr_r 0 $filesize
   load mmc 1:1 $kernel_addr_r /usr/lib/u-boot/starfive_visionfive2/u-boot.itb
   sf update $kernel_addr_r 0x100000 $filesize
   reset
   ```

6. Press any key again when the message "Hit any key to stop autoboot" reappears.
7. Run the following commands:

   ```shell
   env default -f -a
   env save
   reset
   ```

8. After the reboot, you'll see the boot process in the UART console. Once you see the "login" prompt, log in as `ubuntu:ubuntu`.
9. Have fun!
