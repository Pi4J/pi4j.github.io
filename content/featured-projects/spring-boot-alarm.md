---
title: 'Spring Boot Alarm System'
weight: 52
tags: ["Spring", "Spring Boot", "Gradle", "Digital Input", "Digital Output", "PIR", "LED", "Buzzer"]
---

{{% notice tip %}}
GITHUB PROJECT: [github.com/bmike2047/springboot-rpi-alarm-system](https://github.com/bmike2047/springboot-rpi-alarm-system)
{{% /notice %}}

This project by **Mihai Buleandra**, uses Spring Boot to create a simple wired alarm system. Most examples on this website use Maven, but this project is a nice example of how to configure a Gradle project to use Pi4J. Mihai also uses Thymeleaf and Bootstrap for the web user interface, that has live updates showing the state of the alarm system.

{{< youtube xRUWgISEngM >}}

The alarm system makes use of Java's multithreading capabilities, as it's based on a non-blocking Finite State Machine. This means each state runs in its own thread allowing the web interface to not block while waiting for different operations. Multi-threaded reusable Java drivers for the Raspberry Pi are implemented using the Pi4J library for the keypad, Passive Infrared sensor (PIR), LED and Buzzer.
Keypad driver includes debounce implementation also.

![](/assets/featured-projects/spring-boot-alarm/rpi-alarm-bb.png)

The code and more info is available in the [GitHub project](https://github.com/bmike2047/springboot-rpi-alarm-system).