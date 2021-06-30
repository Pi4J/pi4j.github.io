---
title: JavaFX kiosk mode
weight: 80
---

{{% notice note %}}
Visit [webtechie.be]( https://webtechie.be/post/2021-04-23-javafx-kiosk-raspberry-pi/) for the full blogpost
{{% /notice %}}

## Kiosk Mode

With Gluon's JavaFX 17-ea, we are able to run applications in different modes: Desktop and Kiosk mode.
In this post we focus on the Kiosk mode only.

With this approach, the application is the only thing you see on the screen. This prevents the user to open any other applications, or mess up your system. 
In this case, there is no need for a window manager, and the application directly uses the underlying (hardware) framebuffer. 
To achieve this, we use <strong>Monocle with EGL and DRM</strong>, as that is the Linux approach to directly address the hardware acceleration, without a window manager. 
The JavaFX application is using Direct Rendering Mode (DRM) to be visualized. An extra benefit is the performance boost, as your program is the only thing that needs to be handled towards the screen.


* By using /sbin/init 3 before the application starts, the desktop mode is stopped.
* As DRM in JavaFX 17-ea is part of the commercial license of Gluon, we need to set the environment value ENABLE_GLUON_COMMERCIAL_EXTENSIONS, for more info see Gluon docs: “JavaFX on Embedded” > “Legal notice”.
* The display id needs to be defined, if card0 is not working and you get the error [GluonDRM] Device /dev/dri/card0 could be opened, but has no drm capabilities., try card1. More info is provided on Gluon docs: “JavaFX on Embedded” > “Testing JavaFX”.
* After the application is stopped, we call /sbin/init 5 to restart the regular desktop environment.

``` shell
#!/usr/bin/env bash
/sbin/init 3
export ENABLE_GLUON_COMMERCIAL_EXTENSIONS=true
java \
  -Degl.displayid=/dev/dri/card0 \
  -Dmonocle.egl.lib=/opt/javafx-sdk-17/lib/libgluon_drm-1.1.3.so \
  -Djava.library.path=/opt/javafx-sdk-17/lib \
  -Dmonocle.platform.traceConfig=false \
  -Dprism.verbose=false \
  -Djavafx.verbose=false \
  -Dmonocle.platform=EGL \
  --module-path .:/opt/javafx-sdk-17/lib \
  --add-modules javafx.controls \
  --module com.pi4j.example/com.pi4j.example.FxglExample $@
/sbin/init 5
```

To run the application in kiosk mode it is recommended to have an open ssh session on the side to follow the process or
in case of errors, being able to restart the desktop with:
``` shell
/sbin/init 5
```

### Performance
By disabling the window manager, more ressources are available for the application, therefore running more performant.
To test the performance of the windowed mode and kiosk mode, several [tests](https://github.com/FDelporte/FXGLPerformanceTest/tree/main/src/main/java/be/webtechie/performancetest) have been executed. 

RaspberryPi model: RaspberryPi 4 8G Model B

The tests were run with 50, 100 and 500 balls. The results of the study show that even thought many more resources are available, the game does not run the expected amount smoother. 
A slight increase of RAM and CPU is noticeable, but the average frames per second do not improve that much. Non the less, the FPS was more stable while running in kiosk mode and might be an advantage when running games.

Overall the kiosk mode has advantages over the windowed mode but using the kiosk mode exclusively to boost the performance is not recommended.

### Extra tips

#### Gluon documentation
Gluon keeps the documentation for Raspberry Pi constantly updated, keep an eye on [gluonhq](https://docs.gluonhq.com/#_javafx_on_embedded) to stay up-to-date.

#### 64-bit OS and JavaFX
If you want to go 64-bit, you can use the same approach. There is no official 64-bit Raspberry Pi OS yet, but you can find more information on [“Faster & More Reliable 64-bit OS on Raspberry Pi 4 with USB Boot”](https://foojay.io/today/64-bit-raspbian-os-on-raspberry-pi-4-with-usb-boot/).

#### Unclutter
Another great addition for a kiosk approach is [Unclutter](https://wiki.archlinux.org/title/Unclutter), a small tool which hides your mouse cursor when you do not need it. You only have to move the mouse for the cursor to reappear.
``` shell
sudo apt install unclutter
``` 

To run the application in kiosk mode it is recommended to have an open ssh session on the side to follow the process or 
in case of errors, being able to restart the desktop with:
``` shell
/sbin/init 5
```

