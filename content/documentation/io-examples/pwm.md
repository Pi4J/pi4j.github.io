---
title: Pulse Width Modulation (PWM)
weight: 220
tags: ["PWM", "CrowPi"]
---

## What is it?

The abbreviation PWM stands for "Pulse Width Modulation" and is also often referred 
to in German as pulse width modulation or pulse duration modulation. This technology 
is used, among other things, to control servomotors and is also used, for example, 
for the fans of a regular computer.

With PWM, it is possible to control a component such as a motor no longer purely 
binary, i.e. off (0% power) or on (100% power), but to control them almost at will. 
The functionality of PWM works in such a way that the component is switched off and 
on again and again within a certain period of time.

## Pigpio Provider (pigpio-pwm)

### Software vs. Hardware

When using the pigpio-pwm provider two different types of PWM are available on the Raspberry Pi, specifically a software 
and a hardware implementation. Both basically offer the same options, but the software
version cannot achieve precise or particularly fast frequencies. When using the linuxfs-pwm provider only 
hardware PWM is available.

### Software PWM limitation

The reason for this is that in the software implementation for each individual cycle 
(on / off) a new control command must be transmitted from the JVM (Java Virtual Machine) 
to the corresponding component, while in the hardware implementation of the Raspberry Pi 
notices the desired frequency and regulates it independently directly on the board.

The Raspberry Pi supports 2 hardware based PWM channels. You can access these two channels
via 2 separate sets of 4 GPIO header pins, but still limited to only 2 channels 
(2 unique PWM timing configurations).

### PWM GPIOs

The same PWM channel is available on multiple GPIOs.
The latest frequency and dutycycle setting will be used by all GPIO which share a PWM channel.

The GPIO must be one of the following:

```
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
The GPIO number in the above chart is supplied as the buildPwmConfig config value ```address```.

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


## Linuxfs Provider (linuxfs-pwm)

As of version 2.6.0 of Pi4J, `linuxfs-pwm` also supports hardware PWM on the Raspberry Pi 5. More information and an example implementation is available in the blog post [PWM Hardware Support on Raspberry Pi5](/blog/2024/20240423_pwm_rpi5/).

### Hardware only

Only hardware PWM is supported.

### PWM GPIOs
The channel number in the following charts are supplied as the buildPwmConfig config value ```address```.

The user must modify `config.txt` to enable PWM. 

* Raspberry OS Bullseye: `/boot/config.txt`
* Raspberry OS Bookworm  `/boot/firmware/config.txt` 
 
To take effect after file modification the Raspberry Pi must be rebooted.

#### Raspberry Pi 4

Use one of the following configurations:

```text
[all]
dtoverlay=pwm
# GPIO 18 = channel 0

[all]
dtoverlay=pwm-2chan
# GPIO 18 = channel 0
# GPIO 19 = channel 1

[all]
dtoverlay=pwm-2chan,pin=12,func=4,pin2=13,func2=4
# GPIO 12 = channel 0
# GPIO 13 = channel 1
```

You can test the PWM channels in the terminal like this:

```bash
# With dtoverlay=pwm-2chan in config.txt
$ pinctrl get 18
18: a5    pd | lo // GPIO18 = PWM0_0
$ pinctrl get 19
19: a5    pd | lo // GPIO19 = PWM0_1
```

#### Raspberry Pi 5

Use one of the following configurations:

```text
[all]
dtoverlay=pwm
# GPIO 18 = channel 2

[all]
dtoverlay=pwm-2chan
# GPIO 18 = channel 2
# GPIO 19 = channel 3
 
[all]
Dtoverlay=pwm-2chan,pin=12,func=4,pin2=13,func2=4
# GPIO 12 = channel 0
# GPIO 13 = channel 1
```

The statement added to `config.txt` will determine which GPIOs will exhibit the PWM behavior.
The channel number in the above charts are supplied as the `buildPwmConfig` value for the `address`.

You can test the PWM channels in the terminal like this:

```bash
# With dtoverlay=pwm-2chan in config.txt
$ pinctrl get 18
18: a3    pd | lo // GPIO18 = PWM0_CHAN2
$ pinctrl get 19
19: a3    pd | lo // GPIO19 = PWM0_CHAN3
```

When needed, you can also configure a combination of, for example, GPIO12 and GPIO18 as needed on the CrowPi 2 to control both the buzzer (18) and RGB LED Matrix (12):

```bash
# In config.txt
dtoverlay=pwm-2chan,pin=18,func=2,pin2=12,func2=4

# Reboot and test
$ pinctrl get 12
12: a0    pd | lo // GPIO12 = PWM0_CHAN0
$ pinctrl get 13
13: no    pd | -- // GPIO13 = none
$ pinctrl get 18
18: a3    pd | lo // GPIO18 = PWM0_CHAN2
$ pinctrl get 19
19: no    pd | -- // GPIO19 = none
```

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

### Additional Information
- [Choosing an I/O Provider](../providers/_index.md)
- [Wikipedia on PWM](https://en.wikipedia.org/wiki/Pulse-width_modulation)
- [Wikipedia with audio frequencies](https://en.wikipedia.org/wiki/Piano_key_frequencies)
- [Possible exception](../../blog/2025/20250811-Pi5-PWM-not-working--NoSuchFileException)

### Code example

The following example is an extract of the [CrowPi example project](../../examples/crowpi/crowpi-examples.md) which includes 
a component to control a buzzer with PWM.
Of importance, this example executes on a Raspberry Pi4, the buildPwmConfig(Context pi4j, int address) example 
code uses pigpio-pwm and the value passed for 'address' is the BCM pin number.


```java
public class BuzzerComponent extends Component {

    protected final Pwm pwm;

    /**
     * Creates a new buzzer component with a custom BCM pin.
     *
     * @param pi4j    Pi4J context
     * @param address Custom BCM pin address
     */
    public BuzzerComponent(Context pi4j, int address) {
        this.pwm = pi4j.create(buildPwmConfig(pi4j, address));
    }

    /**
     * Plays a tone with the given frequency in Hz indefinitely.
     * This method is non-blocking and returns immediately.
     * A frequency of zero causes the buzzer to play silence.
     *
     * @param frequency Frequency in Hz
     */
    public void playTone(int frequency) {
        playTone(frequency, 0);
    }

    /**
     * Plays a tone with the given frequency in Hz for a specific duration.
     * This method is blocking and will sleep until the specified duration has passed.
     * A frequency of zero causes the buzzer to play silence.
     * A duration of zero to play the tone indefinitely and return immediately.
     *
     * @param frequency Frequency in Hz
     * @param duration  Duration in milliseconds
     */
    public void playTone(int frequency, int duration) {
        if (frequency > 0) {
            // Activate the PWM with a duty cycle of 50% and the given frequency in Hz.
            // This causes the buzzer to be on for half of the time during each cycle, resulting in the desired frequency.
            pwm.on(50, frequency);

            // If the duration is larger than zero, the tone should be automatically stopped after the given duration.
            if (duration > 0) {
                sleep(duration);
                this.playSilence();
            }
        } else {
            this.playSilence(duration);
        }
    }

    /**
     * Silences the buzzer and returns immediately.
     */
    public void playSilence() {
        pwm.off();
    }

    /**
     * Silences the buzzer and waits for the given duration.
     * This method is blocking and will sleep until the specified duration has passed.
     *
     * @param duration Duration in milliseconds
     */
    public void playSilence(int duration) {
        this.playSilence();
        sleep(duration);
    }

    /**
     * Returns the created PWM instance for the buzzer
     *
     * @return PWM instance
     */
    protected Pwm getPwm() {
        return this.pwm;
    }

    /**
     * Builds a new PWM configuration for the buzzer using pigpio-pwm
     *
     * @param pi4j    Pi4J context
     * @param address BCM pin address
     * @return PWM configuration
     */
    protected static PwmConfig buildPwmConfig(Context pi4j, int address) {
        return Pwm.newConfigBuilder(pi4j)
            .id("BCM" + address)
            .name("Buzzer")
            .address(address)
            .pwmType(PwmType.HARDWARE)
            .provider("pigpio-pwm")
            .initial(0)
            .shutdown(0)
            .build();
    }
    
    /**  Builds a new PWM configuration for the buzzer using linuxfs-pwm
    * @param pi4j    Pi4J context
    * @param channel Channel
    * @return PWM configuration
    */
    protected static PwmConfig buildPwmConfig(Context pi4j, int channel) {
        return Pwm.newConfigBuilder(pi4j)
            .id("Channel" + channel)
            .name("Buzzer")
            .address(channel)
            .pwmType(PwmType.HARDWARE)
            .provider("linuxfs-pwm")
            .initial(0)
            .shutdown(0)
            .build();
  }

}
```
