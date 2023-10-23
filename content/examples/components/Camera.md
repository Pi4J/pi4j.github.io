---
title: Camera
weight: 210
tags: ["Camera"]
---

### Description

The [Camera](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/Camera.java) is a template class, that you can use in your own Java-project.
Currently, the code is only tested with a [Raspberry-Camera](https://www.raspberrypi.com/documentation/accessories/camera.html#introducing-the-raspberry-pi-cameras) and the [crowpi-image](/getting-started/crowpi/crowpi-os/).
You can take pictures or videos, with or without a preview.

{{% notice note %}}
To connect the camera, use this [video](https://youtu.be/GImeVqHQzsE). The video is mentioned on the official [website](https://www.raspberrypi.com/documentation/accessories/camera.html).
The camera class is using the bash-commands "libcamera-hello", "libcamera-still" and "libcamera-vid". To use them, set up the raspberry with the following [Introduction](https://www.raspberrypi.com/documentation/accessories/camera.html#getting-started)
{{% /notice %}}

### Layout

{{< gallery >}}
{{< figure link="/assets/examples/components/pictures/Raspberry-Camera.png" caption="Raspberry Camera" caption-position="center" caption-effect="fade" >}}{{< /gallery >}}
{{< load-photoswipe >}}

### Code

An example on how to use the Camera-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components)

```java
        Camera camera = new Camera();

        System.out.println("Taking a default picture");
        camera.recordPicture();

        System.out.println("Taking a pic with different parameters");
        var config = Camera.newPictureConfigBuilder()
        .outputPath("/home/pi/Pictures/")
        .delay(3000)
        .disablePreview(true)
        .encoding(Camera.PicEncoding.PNG)
        .useDate(true)
        .quality(93)
        .width(1280)
        .height(800)
        .build();

        camera.recordPicture(config);

        System.out.println("Waiting for camera to take pic");
        delay(Duration.ofSeconds(4));

        System.out.println("Taking a video for 3 seconds");
        var vidconfig = Camera.newVidConfigBuilder()
        .outputPath("/home/pi/Videos/")
        .recordTime(3000)
        .useDate(true)
        .build();
        camera.recordVideo(vidconfig);

        camera.reset();
```

### Further application

The class is implemented in the sample project [Photobooth](https://github.com/DieterHolz/PhotoBooth).

### Further project ideas

- Use a camera and a motion-sensor to create a wildlife-camera
- Use a camera to monitor the entrance of a building, by publishing the preview of the camera to a webserver
