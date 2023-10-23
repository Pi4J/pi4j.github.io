---
title: ServoMotor
weight: 210
tags: ["Servo Motor"]
---

### Description

The [ServoMotor](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/ServoMotor.java) is a template class, that you can use in your own Java-project.
You can set the servo to a specific location, likewise to 110 degrees of it's range.

You can use a wide variety of analog servo motors such as the SG92R or the SG-5010 (for a little more torque).

### Layout

![Servo Layout](/assets/examples/components/components/Layout-Servo.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/ServoBreadboard.png" caption="Servo Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/ServoSG-5010-TopView.png" caption="Servo SG-5010 Top View" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/ServoSG-5010-SideView.png" caption="Servo SG-5010 Side View" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/ServoSG92R-SideView.png" caption="Servo SG92R Side View" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/miniPowerSupplyModule.jpeg" caption="Mini Power Supply Module" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/miniPowerSupplyModuleFrontBack.jpeg" caption="Mini Power Supply Module Front Back" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

An example how to use the Servo-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
        // Initialize servo motor component
final var servoMotor = new ServoMotor(pi4j, PIN.PWM18, 50, -90.0f, 90.0f, 2.0f, 12f);

        // Demonstrate the percentage mapping on the servo
        System.out.println("In 2 seconds, the servo motor will move to the left-most position which is 0%");
        delay(Duration.ofSeconds(2));
        servoMotor.setPercent(0);

        System.out.println("In another 2 seconds, the servo motor will show 100% by moving to the right-most position");
        delay(Duration.ofSeconds(2));
        servoMotor.setPercent(100);

        System.out.println("Last but not least, in 2 more seconds the servo will be centered to display 50%");
        delay(Duration.ofSeconds(2));
        servoMotor.setPercent(50);


        // Sweep once from left to right using the setAngle function
        System.out.println("We will sweep once to the left in 2 seconds...");
        delay(Duration.ofSeconds(2));
        servoMotor.setAngle(-45);

        System.out.println("... and now to the right in 2 more seconds!");
        delay(Duration.ofSeconds(2));
        servoMotor.setAngle(45);

        // Use a custom range for displaying the data
        System.out.println("Imagine a pointer on the servo positioned above a label between -20ºC and +40ºC");
        System.out.println("By using the setRange() method, we can automatically map our temperature range to the servo range!");
        System.out.println("As an example, in five seconds the servo will show -10º which should be on the far left of the servo.");
        delay(Duration.ofSeconds(2));

        servoMotor.setRange(-20, +40); // This will define our range as values between -20 and +40
        servoMotor.moveOnRange(-10); // This will map -10 based on the previously defined range

        servoMotor.reset();

```

### Further application

The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Photobooth](https://github.com/DieterHolz/PhotoBooth).

### Further project ideas

- As a Servo can cover up to 180 degrees, it could be used as a steering-wheel hooked to a potentiometer
- As a pointer, to show how much time is left in a timer
