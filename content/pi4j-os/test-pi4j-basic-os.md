---
title: Test Pi4J Basic OS
weight: 30
tags: ["Pi4J OS"]
---

The Pi4J Basic OS contains two simple applications in directory `java-examples` and a sample file to test the audio channel. As Pi4J CrowPi OS and Pi4J Picade OS are based on Pi4J Basic OS, they also contain these tests.

You can start the tests via `ssh`.

### Audio Test

```shell
cd /home/pi
nvlc Music/StarTrekTheme.mp3
```

### Pure JavaFX Application

Compile the JavaFX application

```shell
cd /home/pi/java-examples/pure-javafx
javac --module-path /opt/javafx-sdk/lib --add-modules=javafx.controls,javafx.media hellofx/HelloFX.java
```

To start `HelloFX` in X11-Mode

```shell
DISPLAY=:0 XAUTHORITY=/home/pi/.Xauthority sudo -E java --module-path /opt/javafx-sdk/lib --add-modules javafx.controls,javafx.media -Dglass.platform=gtk hellofx.HelloFX
```

To start `HelloFX` in DRM (Direct Rendering Mode)

```shell
sudo java-kiosk hellofx.HelloFX
```

{{% notice tip %}}
`java-kiosk` is a command provided by our image. It assures to call `java` with the correct (and huge) set of parameters.
{{% /notice %}}

### Pure Pi4J Application

Attach a button to `pin 25`.

* On CrowPi that's the `left`-button.
* on Picade Console that's the `button-4`-button.
- Otherwise:

![Button on Pin 25](https://github.com/Pi4J/pi4j-os/blob/main/assets/pi4j-minimal.png?raw=true)

Compile and start the Java application

```shell
cd /home/pi/java-examples/pure-pi4j
javac -cp "/home/pi/deploy/*:." hellopi4j/MinimalPi4J.java
sudo java -cp "/home/pi/deploy/*:." hellopi4j.MinimalPi4J
```