---
title: "Interview Robert von Burg"
date: 2024-04-19
tags: ["Interview", "Pi4J"]
---

2024-04-19, by Frank Delporte

The Pi4J project has two important Roberts. The first one is **Robert Savage** (living in the US), who started the Pi4J development. You can read more about him and the reason Pi4J was created in [this interview on Foojay](https://foojay.io/today/interviews-with-robert-savage-and-johan-vos-on-the-state-of-java-on-raspberry-pi/). He also created V2 of Pi4J, but hasn't been involved a lot in the project since its release. Luckily, we have another Robert in [the Pi4J team](https://pi4j.com/about/team/)! **Robert von Burg** (living in Switzerland), also known as **Eitch**, is the [main maintainer now of the Pi4J V2 sources](https://github.com/Pi4J/pi4j) and takes care of the releases.

Let's learn more about him...

_**Can you introduce yourself? What is your history in software (Java) development?**_

My name is Robert von Burg. I've started programming in 1998 learning a bit of C, but quickly moved to Java, which became my favourite language. 
I first worked on programming workflow control systems, taking orders from ERP systems, and controlling the shop floor by communicating with PLCs, e.g. Siemens using TCP/IP.
Later i worked a bit on enterprise clinical information systems using Java Enterprise Beans, and it's ecosystem.
For the last decade I've been working at [Atexxi](https://www.atexxi.ch/), of which I'm a co-owner and founder. We are developing our [eSyNet platform](https://www.atexxi.ch/system/), 
with which we enable hospitals, pharmacies and elderly/nursing homes to digitize their drug logistics. Our platform is software based, but could not work without our electronic cabinets and accessories,
with which the users of our system interact and thus allow to track inventory.
Our goal is to unburden nurses, and move the administrative work surrounding drug logistics of nurses to the pharmacy.

{{< gallery >}}
{{< figure link="/assets/about/team/eitch.jpg" caption="Robert von Burg" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/strolch/10_eSyBox_Foto_Noemi_Tirro.jpg" caption="eSyBox using pi4j to communicate with the Raspberry Pi's I2C bus" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/strolch/IMG_8095.JPG" caption="eSyBox slot detection in action" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

_**How did you get involved in the Pi4J development?**_

For our electronic cabinets we use Raspberry Pis as the embedded platform to communicate with our custom PCBs using I2C. As we want to use the same programming language and domain model on the server and the cabinets, we looked for a Java library giving us access to the Raspberry Pi's I/Os. Thus, the Pi4J project was selected. During our use we detected a bug, and since the Pi4J maintainer was a little busy, I offered to send a merge request for the fix. Over time, this lead to more involvement with the core project.

_**What are you focusing on in the Pi4J project?**_

My focus is on code review and testing of GPIO and I2C interfaces, as these are the interfaces where I have a certain amount of understanding.

_**Do you use Pi4J in any personal projects?**_

Yes, I use it for a bit of LED and power outlet control. 

_**Do you think Java on Raspberry Pi is a valid choice for business use?**_

Absolutely. Thanks to the community, of which [Azul](https://www.azul.com/) has done a lot, we have a robust JVM on the Raspberry Pi, and we can stay in our domain model on the server and the embedded systems, which makes developing the software easier.

_**How do you think the Pi4J project can evolve further?**_

We are focusing on making the API easier to understand and use, make it work on the different Raspberry Pi versions and then help the community create a standard suite of components to communicate with different hardware which people use in their projects. This makes it easier for newcomers to start using Java on the Raspberry Pi and thus strengthen the Java community as a whole.

_**What is the future of Java on embedded or small systems like the Raspberry Pi?**_

These devices, as they become more and more powerful with each generation, make it easier to implement more and more features at home. If we think how people use them to extend their home networks for security, media playback, or home automation, I see a bright future. Our goal with the Pi4J project is to make it as easy as possible to onboard newcomers.