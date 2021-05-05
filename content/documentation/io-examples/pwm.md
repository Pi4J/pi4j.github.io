---
title: Pulse Width Modulation (PWM)
weight: 220
tags: ["PWM"]
---

## What is it?

The abbreviation PWM stands for "Pulse Width Modulation" and is also often referred 
to in German as pulse width modulation or pulse width modulation. This technology 
is used, among other things, to control servomotors and is also used, for example, 
for the fans of a regular computer.

With PWM, it is possible to control a component such as a motor no longer purely 
binary, i.e. off (0% power) or on (100% power), but to control them almost at will. 
The functionality of PWM works in such a way that the component is switched off and 
on again and again within a certain period of time.

## Software vs. Hardware

Two different types of PWM are available on the Raspberry Pi, specifically a software 
and a hardware implementation. Both basically offer the same options, but the software
version cannot achieve precise or particularly fast frequencies.

The reason for this is that in the software implementation for each individual cycle 
(on / off) a new control command must be transmitted from the JVM (Java Virtual Machine) 
to the corresponding component, while in the hardware implementation of the Raspberry Pi 
notices the desired frequency and regulates it independently directly on the board.

The Raspberry Pi supports 2 hardware based PWM channels. You can access these two channels
via 2 separate sets of 4 GPIO header pins, but still limited to only 2 channels 
(2 unique PWM timing configurations).

```
The same PWM channel is available on multiple GPIO. 
The latest frequency and dutycycle setting will be used by all GPIO which share a PWM channel.

The GPIO must be one of the following:

12  PWM channel 0  All models but A and B
13  PWM channel 1  All models but A and B
18  PWM channel 0  All models
19  PWM channel 1  All models but A and B

40  PWM channel 0  Compute module only
41  PWM channel 1  Compute module only
45  PWM channel 1  Compute module only
52  PWM channel 0  Compute module only
53  PWM channel 1  Compute module only
```

As Pi4J is using PiGPIO "under the hood", you can take advantage of the additional 
PWM functionalities of it. PiGPIO is providing **additional (soft) PWM support to any 
of the GPIO pins (0-31) and its using some hardware timing technique to optimize 
performance** --- but its not the same as the actual hardware PWM pins natively on the 
RaspberryPi. In the Pi4J API, we call this "Software" PWM and you would need to set 
```.pwmType(PwmType.SOFTWARE)```. We consider this software-based PWM because its being 
provided at a software layer, in this case by the PIGPIO library.

If you need more than 2 PWM pins, use the software PWM functionality, it may be perfectly 
fine for your application. If they are not good enough, then you will probably need a 
PWM expander board/chip (controlled by I2C/SPI) to provide additional PWM support.

## Technical implementation

For the technical control of a component with PWM, two values must be defined:

* Pulse-pause ratio (English: Duty Cycle): This value defines the ratio between the 
  switched-on and switched-off status and is represented by a number between 0% and 100%. 
  A value of 50% means that within one cycle the component is switched on exactly half 
  the time and then switched off. A value of 25%, on the other hand, would mean that 
  the component is switched on only a quarter of the time and the component remains 
  switched off for the remaining three quarters of the cycle.
* Frequency: This value defines how often per second a cycle (on / off) takes place for 
  this component and is usually specified in the unit Hertz (Hz). With a value of 10Hz, 
  the component would alternate 10 times between being switched on and switched off in 
  one second.

These two values can be controlled via the Pi4J library and are also used internally by this project.

## Additional Information

- [Wikipedia on PWM](https://en.wikipedia.org/wiki/Pulse-width_modulation)
- [Wikipedia with audio frequencies](https://en.wikipedia.org/wiki/Piano_key_frequencies)
