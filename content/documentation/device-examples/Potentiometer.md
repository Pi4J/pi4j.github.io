---
title: Potentiometer
weight: 206
tags: ["Potentiometer"]
---
### Description
The [Potentiometer](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
The constructor of the class requires an ADS1115 object. In addition, the channel, with which the AD converter evaluates the current position of the sliding contact must be defined. For normalization, the maximum voltage that can drop across the sliding contact must also be specified. Any commercially available potentiometer with three connections (fixed resistor and the slider) can be evaluated with this class.

The current position of the slider can be defined with a single shot. The return value is either in volts or as a normalized value between 0 and 1.

For continuous monitoring either a slow method can be selected. In this case, individual measurements (single shots) are started and evaluated cyclically. With this method up to 4 devices can be attached to the AD converter. The maximum sampling frequency of the signal depends on how many channels of the AD converter are used simultaneously and how high the sampling rate of the AD converter is set.

Using the fast method, a continuous measurement is started in the AD converter.  The maximum sampling frequency is now only dependent on the sampling rate of the AD converter. However, in this mode only one device can be attached to the AD converter.

If continuous measurement is active, a customized event can be triggered when the position of the slider changes. The threshold can be used to set the sensitivity at which the event should be triggered.

### Layout
![Potentiometer Layout](/assets/documentation/device-examples/Layout-Potentiometer.png)
![]()

{{< gallery >}}
{{< figure link="/assets/documentation/device-examples/pictures/PotentiometerBreadboard.png" caption="Potentiometer Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/pictures/ADS1115-Front.png" caption="ADS1115-Front" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/pictures/ADS1115-Back.png" caption="ADS1115-Back" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code
A simple example on how to use the potentiometer from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :

```
        logInfo("Potentiometer test started ...");

        ADS1115 ads1115 = new ADS1115(pi4j);

        Potentiometer poti = new Potentiometer(ads1115, ADS1115.MUX.AIN0_GND, 3.3);

        //read current value from poti one time
        logInfo("Current value of the poti is " + poti.getVoltage() + " voltage.");

        //read current value from the poti in percent one time
        logInfo("The potentiometer slider is currently at " + poti.getPercent() + " % of its full travel.");

        // Register event handlers to print a message when poti is moved
        poti.setRunnable(() -> {
            logInfo("The current voltage drop is currently " + poti.getActualValue() + " volts");
        });

        //start continious reading with single shot in this mode you can connect up to 4 devices to the analog module
        poti.startSlowContiniousReading(0.1, 1);

        // Wait while handling events before exiting
        logInfo("Move the potentiometer to see it in action!");
        delay(30_000);

        //stop continious reading
        poti.stopSlowContiniousReading();


        logInfo("Potentiometer test done");
```

### Further application
The class is implemented in the sample project [Theremin](https://github.com/DieterHolz/RaspPiTheremin).

### Further projetct ideas
- An application, to control the brightness of the lighting. 
- The speed and direction of a drone can be controlled with a potentiometer.
