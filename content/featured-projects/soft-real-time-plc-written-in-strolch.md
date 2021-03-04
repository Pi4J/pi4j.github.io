---
title: 'Soft real time PLC with Strolch'
weight: 55
---

Strolch is a framework for developing Software which has a different approach compared to Spring and other similar types of 
Java frameworks, as the model is defined as an abstract model, where you always have the same three types of objects: 
Resources, Orders and Activities. The fields are mapped as Parameter objects, of which the important primitives are available.

{{< gallery >}}
{{< figure link="/assets/featured-projects/strolch/IMG_20200430_153450.jpg" caption="Conveyors for containers filled by a dispensing robot" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/strolch/10_eSyBox_Foto_Noemi_Tirro.jpg" caption="eSyBox using pi4j to communicate with the Raspberry Pi's I2C bus" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/strolch/IMG_8095.JPG" caption="eSyBox slot detection in action" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

These are projects by [the company atexxi.ch](https://www.atexxi.ch/).

### A soft real time PLC written in Java running on Strolch

This PLC project by [Robert von Burg](https://twitter.com/eitchme) combines Pi4j, Strolch and the Raspberry Pi. 

It is being used in a material flow controller which coordinates FromStock orders with a medical dispensing robot and dispenses 
the packets into containers. These containers are then moved by a Strolch based PLC. The containers travel on a 12m long conveyor with 
multiple segments and entry/exits to position the container at the dispensing robot's exit.

### Medical cabinet with pick-by-light

The most recent project are medical cabinets which use I2C to communicate with custom electronics to control the locks, 
perform a pick-by-light from slots and uses infrared to detect access to a slot with products in it.

