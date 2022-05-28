---
title: Servo
weight: 209
tags: ["Servo"]
---
### Description
The [Servo](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
You can set the servo to a specific location, likewise to 110 degrees of it's range.
A suitable hardware component is: [Servo](https://www.berrybase.de/bauelemente/elektromagnetische-bauelemente/motoren-servos/sg92r-micro-servo)

### Layout
![Servo Layout](/assets/documentation/device-examples/Layout-servo.png)

### Code
An example on how to use the Servo-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components)

```
//testing component has only a valid range in 45 degrees
        int maxDegrees = 45;
        //initialising component
        Servo servo = new Servo(pi4j, PIN.PWM18, 500, 1500, maxDegrees);

        logInfo("setting it to the lowest position");
        servo.setMin();
        delay(1000);

        logInfo("setting it to the center position");
        servo.setCenter();
        delay(1000);

        logInfo("setting it to the highest position");
        servo.setMax();
        delay(1000);

        logInfo("counting up from zero");
        for (int i = 0; i < maxDegrees; i++) {
            servo.setPositionDegrees(i);
            delay(500);
        }

        logInfo("closing the connection, shutting down the pwm");
        servo.close();
```

### Further application
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas
- As a Servo can cover up to 180 degrees, it could be used as a steering-wheel hooked to a potetiometer
- A pointer, to show how much time is left