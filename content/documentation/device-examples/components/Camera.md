---
title: Camera
weight: 210
tags: ["Camera"]
---
### Description
The [Camera](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/components) (src/main/java/com/pi4j/components/components) is a template class, that you can use in your own Java-project.
Currently, the code is only tested with a [Raspberry-Camera](https://www.raspberrypi.com/documentation/accessories/camera.html#introducing-the-raspberry-pi-cameras) and the [crowpi-image](/getting-started/crowpi/crowpi-os/).
You can take pictures or videos, with or without a preview.

{{% notice note %}}
To connect the camera, use this [video](https://youtu.be/GImeVqHQzsE). The video is mentioned on the official [website](https://www.raspberrypi.com/documentation/accessories/camera.html).
The camera class is using the bash-commands "libcamera-hello", "libcamera-still" and "libcamera-vid". To use them, set up the raspberry with the following [Introduction](https://www.raspberrypi.com/documentation/accessories/camera.html#getting-started)
{{% /notice %}}

### Layout
{{< gallery >}}
{{< figure link="/assets/documentation/device-examples/pictures/Raspberry-Camera.png" caption="Raspberry Camera" caption-position="center" caption-effect="fade" >}}{{< /gallery >}}
{{< load-photoswipe >}}

### Code
An example on how to use the Camera-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components)

```
System.out.println("Initializing the camera");
Camera camera = new Camera();

System.out.println("Taking a default picture");
camera.takeStill();

System.out.println("Taking a pic with different parameters");
var config = Camera.PicConfig.Builder.outputPath("/home/pi/Pictures/")
		.delay(3000)
		.disablePreview(true)
		.encoding(Camera.PicEncoding.PNG)
		.useDate(true)
		.quality(93)
		.width(1280)
		.height(800)
		.build();

camera.takeStill(config);

System.out.println("waiting for camera to take pic");
delay(4000);

System.out.println("Taking a video for 3 seconds");
var vidconfig = Camera.VidConfig.Builder.outputPath("/home/pi/Videos/")
		.recordTime(3000)
		.useDate(true)
		.build();
camera.takeVid(vidconfig);
```

### Further application
The class is implemented in the sample project [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further project ideas
- Use a camera and a motion-sensor to create a wildlife-camera
- Use a camera to monitor the entrance of a building, by publishing the preview of the camera to a webserver
