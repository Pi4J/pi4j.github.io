---
title: "RPi5 PWM NoSuchFileException"
date: 2025-08-11
tags: ["PWM", "LinuxFS"]
description: "A Raspberry Pi 5 kernel update renumbers PWM chips and breaks Pi4J's PWM support; here's the code change to point at the new pwmchip0 path."
---

2025-08-11, by Tom Aarts

On the Pi5, Pi kernel updates may result in failing PWM. The
exception details will state `/sys/class/pwm/pwmchip2/npwm was not found`.

A kernel code update (6.12) resulted in the objects within `/sys/class/pwm` being numbered differently. It is most likely the PWM is using `/sys/class/pwm/pwmchip0`.

Until a proper fix is available, the following change to your application should resolve this error:

```java
// Add imports
import com.pi4j.plugin.linuxfs.provider.pwm.LinuxFsPwmProvider;
import com.pi4j.plugin.linuxfs.provider.pwm.LinuxFsPwmProviderImpl;

// Replace newAutoContext

// Instead of:
// Context pi4j = Pi4J.newAutoContext();

// Use:
Context pi4j = Pi4J.newContextBuilder()
   .add(new LinuxFsPwmProviderImpl("/sys/class/pwm/", 0) )
   .build();
```