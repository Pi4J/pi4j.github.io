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

The image of the crowpi project has every prerequisite installed to work with javaFX/FXGL

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

## Steps to run snake on your Raspberry Pi

* Download the project from GitHub and build it:

``` shell
$ git clone https://github.com/Pi4J/pi4j-example-fxgl.git
$ cd pi4j-example-fxgl/
$ mvn clean package
``` 

* Change to the distribution directory where you can find the generated package and required Java-modules. Start it with the provided run.sh script:

``` shell
$ cd target/distribution
$ ls -l
total 644
-rw-r--r-- 1 pi pi 364456 Jun 19 10:04 pi4j-core-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi   7243 Jun 19 10:04 pi4j-example-minimal-0.0.1.jar
-rw-r--r-- 1 pi pi 142461 Jun 19 10:04 pi4j-library-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  37302 Jun 19 10:04 pi4j-plugin-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  26917 Jun 19 10:04 pi4j-plugin-raspberrypi-2.0-SNAPSHOT.jar
-rwxr-xr-x 1 pi pi    101 Jun 19 10:04 run.sh
-rwxr-xr-x 1 pi pi    101 Jun 19 10:04 run-kiosk.sh
-rw-r--r-- 1 pi pi  52173 Jun 19 10:04 slf4j-api-2.0.0-alpha0.jar
-rw-r--r-- 1 pi pi  15372 Jun 19 10:04 slf4j-simple-2.0.0-alpha0.jar
$ sudo ./run.sh
``` 

{{% notice note %}}
There are two run scripts:</br>
**run.sh:** runs the application in standard windowed mode</br>
**run-kiosk.sh:** runs the application in DRM mode, see [kiosk mode](/getting-started/fxgl/kiosk-mode/)
{{% /notice %}}
  
## Picade

To control our game we use the hardware mentioned above. Tho following mapper uses a similar binding method as in the [minimal example](/getting-started/minimal-example-application/)

### Pimapper

To make use of the picade controls for existing FXGL project we provide an interface to simply extend your application.

#### Integrate piMapping

The code for the piMapper is found in the example [snake game](https://github.com/Pi4J/pi4j-example-fxgl).
#### Update Game 
  
Change your Game from “extend GameApplication” to “extend PicadeGameApplication”
PicadeGameApplication overrides the GameApplication class of FXGL and provides additional functions to map the picade controllers
  
``` java
public class FxglExample extends PicadeGameApplication
```

#### Update Key Inputs 
    
Now we can use the new piMapper to address keys as well as picade controls. To do this, we need to tell the onKeyDown function, what control we want.
Inputs are defined as in previous tutorials in the picadeControl enum

``` java
onKeyDown(PicadeControl.PIN_BUTTON_1, KeyCode.F, () -> player.getComponent(SnakeHeadComponent.class).grow());
onKeyDown(KeyCode.G, () -> player.getComponent(SnakeHeadComponent.class).log());
```

### GPIO
* The Enum PicadeControl handles the the gpio numbers for the connected controls. [pinout.xyz](https://pinout.xyz/pinout/picade_hat) 
``` java
PIN_JOYSTICK_UP(12),
PIN_JOYSTICK_DOWN(6),
PIN_JOYSTICK_LEFT(20),
PIN_JOYSTICK_RIGHT(16),
PIN_BUTTON_1(5);
```

## Run Scripts

**run.sh**
</br>Runs the application in windowed mode

``` shell
#!/usr/bin/env bash
java \
  -Dglass.platform=gtk \
  -Djava.library.path=/opt/javafx-sdk-17/lib \
  -Dmonocle.platform.traceConfig=false \
  -Dprism.verbose=false \
  -Djavafx.verbose=false \
  --module-path .:/opt/javafx-sdk-17/lib \
  --add-modules javafx.controls \
  --module com.pi4j.example/com.pi4j.example.FxglExample $@
```

**run-kiosk.sh**
</br>Runs the application with monocle in DRM (Direct rendering mode).
More to kiosk mode [here](/getting-started/fxgl/kiosk-mode/)



