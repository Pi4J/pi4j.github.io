---
title: Potentiometer
weight: 210
tags: ["Potentiometer"]
---

### Description

The [Potentiometer](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/Potentiometer.java) is a template class, that you can use in your own Java-project.
The constructor of the class requires an ADS1115 object. In addition, the channel, with which the AD converter evaluates the current position of the sliding contact must be defined. For normalization, the maximum voltage that can drop across the sliding contact must also be specified. Any commercially available potentiometer with three connections (fixed resistor and the slider) can be evaluated with this class.

The current position of the slider can be defined with a single shot. The return value is either in volts or as a normalized value between 0 and 1.

For continuous monitoring either a slow method can be selected or a fast one. In this case, individual measurements (single shots) are started and evaluated cyclically. With this method, up to 4 devices can be attached to the AD converter. The maximum sampling frequency of the signal depends on how many channels of the AD converter are used simultaneously and how high the sampling rate of the AD converter is set to.

Using the fast method, a continuous measurement is started in the AD converter.  The maximum sampling frequency is now only dependent on the sampling rate of the AD converter. However, in this mode only one device can be attached to the AD converter simultaneously.

If continuous measurement is active, a customized event can be triggered when the position of the slider changes. The threshold can be used to set the sensitivity at which the event should be triggered.

### Layout

![Potentiometer Layout](/assets/examples/components/components/Layout-Potentiometer.png)
![]()

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/PotentiometerBreadboard.png" caption="Potentiometer Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/Potentiometer.png" caption="Potentiometer" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/ADS1115-Front.png" caption="ADS1115-Front" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/ADS1115-Back.png" caption="ADS1115-Back" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the potentiometer from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
System.out.println("Potentiometer test started ...");

Ads1115 ads1115 = new Ads1115(pi4j, 0x01, Ads1115.GAIN.GAIN_4_096V, Ads1115.ADDRESS.GND, 4);

Potentiometer poti = new Potentiometer(ads1115, 0, 3.3);

//read current value from poti one time
System.out.println("Current value of the poti is " + String.format("%.3f", poti.singleShotGetVoltage()) + " voltage.");

//read current value from the poti in percent one time
System.out.println("The potentiometer slider is currently at " + String.format("%.3f", poti.singleShotGetNormalizedValue()) + " % of its full travel.");

// Register event handlers to print a message when potentiometer is moved
poti.setConsumerSlowReadChan((value) -> System.out.println("The potentiometer slider is currently at " + String.format("%.3f", value) + " % of its full travel."));

//start continuous reading with single shot in this mode you can connect up to 4 devices to the analog module
poti.startSlowContinuousReading(0.05, 10);

// Wait while handling events before exiting
System.out.println("Move the potentiometer to see it in action!");
delay(30_000);

//stop continuous reading
poti.stopSlowContinuousReading();

System.out.println("Potentiometer test done");
```

### Further application

The class is implemented in the sample project [Theremin](https://github.com/DieterHolz/RaspPiTheremin).

### Further project ideas

- An application, to control the brightness of some lights.
- The speed and direction of a drone can be controlled with a potentiometer.
