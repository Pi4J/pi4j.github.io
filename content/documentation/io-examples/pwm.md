---
title: 'Pulse Width Modulation (PWM)'
---

The RaspberryPi hardware supports 2 hardware PWM channels. But as Pi4J uses PiGPIO "under the hood", we can take advantage of the 

The Raspberry Pi supports 2 hardware based PWM channels. You can access these two channels via 2 separate sets of 4 GPIO header pins. But still limited to only 2 channels (2 unique PWM timing configurations).

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

As Pi4J is using PiGPIO "under the hood", you can take advantage of the additional PWM functionalities of it. PiGPIO is providing **additional (soft) PWM support to any of the GPIO pins (0-31) and its using some hardware timing technique to optimize performance** --- but its not the same as the actual hardware PWM pins natively on the RaspberryPi. In the Pi4J API, we call this "Software" PWM and you would need to set ```.pwmType(PwmType.SOFTWARE)```. We consider this software-based PWM because its being provided at a software layer, in this case by the PIGPIO library.

If you need more than 2 PWM pins, use the software PWM functionality, it may be perfectly fine for your application. If they are not good enough, then you will probably need a PWM expander board/chip (controlled by I2C/SPI) to provide additional PWM support.

!! TODO add example code