---
title: Test Pi4J Picade OS
weight: 40
tags: ["Pi4J OS"]
---

Pi4J Picade OS contains an additional Test and the audio test should use the internal loudspeaker.

Compile the JavaFX application

```shell
cd /home/pi/java-examples/pure-picade
javac --module-path /opt/javafx-sdk/lib --add-modules=javafx.controls,javafx.media hellopicade/HelloPicade.java
```

To start `HelloPicade` in X11-Mode

```shell
DISPLAY=:0 XAUTHORITY=/home/pi/.Xauthority sudo -E java --module-path /opt/javafx-sdk/lib --add-modules javafx.controls,javafx.media -Dglass.platform=gtk hellopicade.HelloPicade
```

To start `HelloPicade` in DRM

```shell
sudo java-kiosk hellopicade.HelloPicade
```

Check the mapping of the Picade buttons to JavaFX KeyCodes:

| Picade                  | KeyCode          |
|:------------------------|:-----------------|
| Joystick up             | KeyCode.UP       |
| Joystick down           | KeyCode.DOWN     |
| Joystick left           | KeyCode.LEFT     |  
| Joystick right          | KeyCode.RIGHT    | 
| right side black button | KeyCode.ENTER    |
| left side black button  | KeyCode.ESCAPE   |
| all other buttons       | no mapping       | 
