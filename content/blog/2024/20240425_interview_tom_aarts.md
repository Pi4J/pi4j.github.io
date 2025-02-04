---
title: "Interview Tom Aarts"
date: 2024-04-25
tags: ["Interview", "Pi4J"]
---

2024-04-25, by Frank Delporte

**Tom Aarts** started contributing to the Pi4J project when he did his first commit in the [pi4j-example-devices repository](https://github.com/Pi4J/pi4j-example-devices/). At this moment, you can find example implementations for a long list of devices (see screenshot below), using V2 of Pi4J. While creating these implementations he found and fixed some missing pieces and bugs in the core library. See, for instance, this [blog post about the ongoing PWM improvements for the Raspberry Pi 5](https://pi4j.com/blog/2024/20240423_pwm_rpi5/). Furthermore, you can find Tom often in assisting users who [filed a Pi4J V2 issue](https://github.com/Pi4J/pi4j/issues) or [started a discussion](https://github.com/Pi4J/pi4j/discussions).

Let's learn more about him...

{{< gallery >}}
{{< figure link="/assets/about/team/tom.jpg" caption="Tom Aarts" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/tom/pi4j-example-devices.png" caption="Devices implemented in pi4j-example-devices" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/tom/desk.jpg" caption="Toms desk" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

_**Can you introduce yourself? What is your history in software (Java) development?**_

Hi I'm Tom. My degree and career started in hardware. In 1971, I was working on HF transmitters that used vacuum tubes the size of your fist. By the eighties, I transitioned to firmware and software engineering.

My first Java involvement was at IBM in the 90's when Java was first implemented on the AS400 to support the SOM (SystemObjectModel) architecture. This was the initial Java compiler, JIT and Garbage collector for the AS400. So although I was doing Java implementations, I interacted with these teams learning from them.

Then next was WebSphere, implementing a distributed Java financial application. After this time, my work was in server firmware development and later hardware simulation. Although the languages being used were not Java, Java remained my preferred language to code any tools my work required.

_**How did you get involved in the Pi4J development?**_

As I neared retirement I looked for future activities of interest and selected Raspberry Pi to be one of those activities. At that time, Pi4J was V1 and I used it to use some I2C chips. When V2 was released, and I migrated my existing code to V2, I became more interested in the Pi4J implementation.

The direction in V2 was no longer to provide device specific implementations. I offered to make my existing device implementations public if they could assist new users to understand Pi4J. Ongoing, while assisting on the discussions, I used the chip in question to create an example to demonstrate a way to solve a question. Along the way, I supplied a couple Pi4J fixes and enhancements becoming more involved in maintenance of the Pi4J V2 code base.

_**What are you focusing on in the Pi4J project?**_

My focus remains device support and examples to assist in issues and discussions. Also, helping with the work brought on by the new Raspberry Pi 5 to support the RP1 chip and bug fix and enhancements that result from various questions.

_**How do you use Pi4J in your own personal or company projects?**_

I have a couple home projects for clocks and temperature, and a great number of prototype boards to support the various chips I implemented.

{{< gallery >}}
{{< figure link="/assets/blogs/tom/setup-1.jpg" caption="Test setup" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/tom/setup-2.jpg" caption="Test setup" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/blogs/tom/setup-3.jpg" caption="Test setup" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}

_**You answer a lot of questions in the Pi4J discussions and tickets. What is the most challenging part to be able to help users?**_

Users usually ask a specific question. The difficulty is determining what level of response they need. Based on some questions, the details that are given, and what is asked, I think this particular user is experienced and understands Pi4J and the Raspberry Pi so a technical response to just their question will be good.

Some questions include details that make me conclude this person is new to Pi4J. So I need to think about what 'newbie' mistakes could be made and provide a larger list of recommended steps and references of where more detail is available.

It are the questions that fall between these two categories that are more difficult to rapidly help the user. If I think they have more understanding, than they actually feel my response is too short and the user tries to accomplish what I suggested, and they make little or no progress and likely get frustrated. On the other hand if I think they are not experienced and give a great deal of information, the user then views it as a waste of their time as they already correctly completed what I suggest, and that certainly frustrates that user.

_**How do you think the Pi4J project can evolve further?**_

By adding more demonstration cases of Pi4J we can increase the interest and users. Pi4J doesn't intend to implement IOT devices or supply Machine Learning applications, but we need these as reference projects. These should be simple but fully functional projects to demonstrate the capability of a Raspberry Pi using Pi4J. I believe this will bring in more users wanting to implement Home or Work IOT and do the implementation themselves. In addition, it can encourage STEM learning centers to use the Raspberry Pi and Pi4J as the Raspberry Foundation originally intended: _a learning tool_.

_**What is the future of Java on embedded or small systems like the Raspberry Pi?**_

I think Java will remain a valuable choice for these cases. Currently, there is emphasis on languages that prevent memory leaks and provide security, Java does both these items.  I think we can assume the Java Runtime Environments will continue to improve performance and memory usage of Java. Also, there are very useful IDEs available for development, and of course Java portability.