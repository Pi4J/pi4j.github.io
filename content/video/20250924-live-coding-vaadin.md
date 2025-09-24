---
title: "2025 Live Coding: Vaadin"
date: 2025-09-24
tags: ["Video", "Vaadin", "Spring", "CrowPi", "Live Coding"]
---

## Live Stream Coding

### Improving the Vaadin+Spring+Pi4J demo application with Matti Tahvonen

2025-09-24, by Frank Delporte

During a live stream coding session, [Matti Tahvonen](https://www.linkedin.com/in/mattitahvonen/) and [Frank Delporte](https://www.linkedin.com/in/frankdelporte/) updated an existing Vaadin+Spring+Pi4J demo application to use the latest version of the libraries and Java 25. It's a demo application created a few years ago to be used during presentations at conferences. Of course, everything evolves, so a big update and refactoring was needed.

(Sorry for the hiccups in the first minutes, the network connection dropped a few times...)

{{< youtube gtcXnA3endo >}}

Links from this video:

* [Sources of the demo application](https://github.com/FDelporte/Vaadin-examples)
* [Pi4J project](https://www.pi4j.com/)
* [Vaadin components](https://vaadin.com/docs/latest/components)
* [Vaadin directory](https://vaadin.com/directory/)
* [Vaadin 24.9 release notes](https://vaadin.com/blog/vaadin-24-9-release)
* [Gauge component](https://vaadin.com/directory/component/gauge)
* [Notifications with Vaadin](https://vaadin.com/blog/which-notifications-are-best-for-your-java-app-web-vaadin-or-push)  
* [Start your Java application at Linux startup](https://docs.spring.io/spring-boot/3.5-SNAPSHOT/how-to/deployment/installing.html#howto.deployment.installing.system-d)
* [MelodyMatrix, a website created with Vaadin](https://melodymatrix.rocks/)
* [Using a Raspberry Pi as HDMI camera](https://webtechie.be/post/2021-12-20-raspberry-pi-as-hdmi-camera-for-atem-mini/)

However, during the live session, a problem appeared when building the application for the Raspberry Pi. But the problem was quickly fixed after the stream was finished, as you can see in the video below. And we now have a nice graphical view of the temperature and humidity measured with the DHT11 sensor on the CrowPi 2.

{{< youtube ygrbrxnKflY >}}