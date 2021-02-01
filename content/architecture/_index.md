---
title: Architecture/Design
weight: 40
---

The code of Pi4J is based on a layered approach, visualized in the picture below.

Since Pi4J is a low-level library, it tries to avoid inheriting third-party libraries at all costs. More complex dependency chains make it more difficult for users, especially novice users. Therefor, [the only dependency Pi4J V.2 has is SLF4J](https://github.com/Pi4J/pi4j-v2/blob/master/pi4j-core/src/main/java/module-info.java) to provide a standardized and extensible logging framework. 

The dark grey blocks "Annotation Engine", "@Register" and "@Inject" are here as a future idea but are not included in the current V2.

![Pi4J V2 architecture](https://raw.githubusercontent.com/Pi4J/pi4j-v2/master/assets/draw.io/pi4j-v2-architecture.jpg)
