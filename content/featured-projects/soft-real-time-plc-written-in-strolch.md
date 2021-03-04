---
title: 'Soft real time PLC in Strolch'
weight: 55
---

### A soft real time PLC written in Strolch running on Strolch

Strolch is framework for developing Software which has a different approach compared to Spring and other similar type of 
Java frameworks, as the model is defined as an abstract model, where you always have the same three types of objects: 
Resources, Orders and Activities. The fields are mapped as Parameter objects, of which the important primitives are available.

This PLC project by [Robert von Burg](https://twitter.com/eitchme) combines Pi4j, Strolch and the Raspberry Pi. 

It is being used in a material flow controller which coordinates FromStock orders with a medical dispensing robot and dispenses 
the packets into containers which are controlled by this Strolch PLC. The containers travel on a 12m long conveyor with 
multiple segments and entry/exits to position the container at the dispensing robots exit.

The most recent project are medical cabinets which use I2C to communicate with custom electronics to control the locks, 
perform a pick-by-light from slots and uses infrared to detect access to a slot with drugs in it.

{{< gallery >}}
{{< figure link="/assets/featured-projects/strolch/IMG_20200430_153450.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/strolch/10_eSyBox_Foto_Noemi_Tirro.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/strolch/Leitsystem_atexxi-300x169.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

These are projects by [the company atexxi.ch](https://www.atexxi.ch/).