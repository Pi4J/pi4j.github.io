---
title: Game development with FXGL
weight: 80
tags: ["JavaFX"]
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-example-fxgl](https://github.com/Pi4J/pi4j-example-fxgl)
{{% /notice %}}

As described on [the previous page](/getting-started/user-interface-with-javafx/) you can use JavaFX to build
user interfaces which behave exactly the same on your PC and Raspberry Pi. Let's go a step further and make 
a game with an "Arcade" controller. 

For this project, we will be using [FXGL](https://github.com/AlmasB/FXGL), an opensource library on top of 
JavaFX to build games.

## The controller 

This project uses an [Arcade kit](https://www.kiwi-electronics.nl/pim-471?search=arcade&description=true)
in combination with a [Picade X HAT USB-C](https://www.kiwi-electronics.nl/index.php?route=product/product&search=arcade&description=true&product_id=4337)
to easily connect the wires of the buttons and joystick.

Connect the USB power to the hat instead of your Raspberry Pi, and use the power button on the hat to
start your Raspberry Pi.

{{< gallery >}}
{{< figure link="/assets/getting-started/fxgl/arcade_parts_kit.jpg" caption="Arcade kit components" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/fxgl/picade_hat.jpg" caption="Picade Hat" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/fxgl/assembled.jpg" caption="Assembled Picade Hat and Arcade kit" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/fxgl/assembled_closeup.jpg" caption="Connected wires on Picade Hat" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/getting-started/fxgl/picade_hat_pin_numbers.png" caption="Picade Hat pin numbers" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

Pimoroni provides a [GitHub project](https://github.com/pimoroni/picade-hat) with software to use
this hat with RetroPie, but this project aims to take full control of the hardware with Java.

The GPIO numbers are defined by the hat and can be found on [pinout.xyz](https://pinout.xyz/pinout/picade_hat)

## The application

**TODO, currently only minimal implementation is done based on Snake game created by Almas and Frank**

