---
title: 'SmartCoop'
weight: 53
tags: ["I2C", "SPI", "Serial"]
---

{{% notice tip %}}
PROJECT WEBSITE: [smartcoop.tech](https://www.smartcoop.tech)
{{% /notice %}}

Dave Duncanson, an ex Royal Australian Airforce (RAAF) electronics technician and embedded software developer, created the **SmartCoop**. It's a fully automated Chicken Coop Controller solution which uses a Raspberry Pi and a ESP32-S3 Processor located on a custom designed Surface Mount Designed (SMD) PCB. The goal of this project was to significantly reduce the amount of regular and routine tasks required to keep a small flock (~30) of chickens on a hobby farm located in NSW just outside of Canberra Australia. 

The 4th generation of this solution is based on over ten years in development with a lot of trail and error along the way. Just one example was the need to run all of the wiring harness within Conduit otherwise the local cockatoos will eat the wiring. There are no plans to commercialize this project, and all sources and hardware designs [are available on BitBucket](https://bitbucket.org/DaveDuncanson/smartcoop.tech/src/master/README.md).

Dave admits that this solution is most likely over-engineered and therefore not cost-effective for the typical small suburban chicken coop or flock. But it's the perfect solution for him to fully automate the chicken coop, including multiple doors, water management, feed monitoring, system logging (MQTT). He can control everything with an advanced web based user interface. And it protects his chickens from foxes!

He wants to extend the project further with UHF RFID Chicken Tag Readers. This way it will become possible to automatically close the main door when all the chickens have entered the Coop, and even record which chickens are laying the eggs in each laying box.

Thanks to the different providers (GPIO and I2C) in V2 of the Pi4J library, the development of the software became a lot easier as Dave could switch between providers when he was debugging some of the I2C implementations. Because he uses a Raspberry Pi (instead of embedded-only with, for instance, Arduino), he was able to do the majority of the development in Java running on the Pi. This made the implementation of advanced features like the H2 database, MQTT, and GPSD a lot simpler.

{{< gallery >}}
{{< figure link="/assets/featured-projects/smartcoop/GEN4-PCB-Panel-small.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/smartcoop/GEN4-RFID-Reader-Tags-small.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/smartcoop/GEN4-WebUX-small.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/smartcoop/GEN4-WiringPanel-small.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/smartcoop/GEN4-YardGate-small.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/featured-projects/smartcoop/solarregulator.jpg" caption="" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Key Features

The 4th Generation of the SmartCoop provides the following key features:

* Fully Automated Main Door, utilising a light sensor to trigger the open and close with dawn and dusk setting for each day at your location via a GPS.
* Fully automated Yard Door, that utilises a weather forecast from the Australia BOM to decide if the yard door should be opened each day
* Comprehensive Web interface that provides a range of manual controls, configuration settings and charting of sensor data
* Manual push buttons on the PCB to open or close either of the doors, fill the water tank or power up the Raspberry Pi
* Monitors and automated fill of a water tank
* Preset configurable power down and on again function for the Raspberry Pi to reduce overnight battery power consumption
* Nightly check is send via email to ensure that everything is closed for the overnight power down
* Open Source Relational Database to store configuration and long term monitoring of all sensor information
* GPS interface that provides an accurate Time Source for updating the RTC and when our Internet is down, plus LAT & LONG coordinates used for Dusk & Dawn settings
* Realtime monitoring of remaining chicken food across two separate feeders
* Fetches the weather forecast for the location from the Australian BOM site to determine if yard door is to be opened for the day
* Realtime monitoring of the chicken coop system via a MQTT broker

## Sofware

The application uses the following key software components and libraries:

* The Java Runtime Environment (JRE 17x)
* The Pi4J Project - Java I/O Library for the Raspberry Pi (v2.7)
* Hibernate ORM Library (v6.x)
* H2 Database Engine

## Hardware

The hardware design is composed of the following key components:

* Raspberry Pi Zero 2W
* A supporting PCB
* Any 12VDC Solar Regulator (5amp)
* Any 12Vdc Solar Panel (~100W)
* Deep cycle 12VDC Battery
* 1 x 12VDC Water Solenoid
* 2 x 12VDC electric motors (geared ~23rpm)
* 5 x Inductive Proximity Sensor Switch PNP DC6V-36V (LJ12A3-4-Z/BY)
* 1 x Single Float Value Switch (12VDC)
* 20kg Load Cell
* A suitable water proof enclosure (IP66) with clear Front Door to house the PCB and solar regulator
