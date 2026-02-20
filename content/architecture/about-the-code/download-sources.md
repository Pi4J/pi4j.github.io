---
title: Download the Sources
weight: 20
---

You can build the project from sources available on [GitHub](https://github.com/Pi4J/pi4j).

* Checkout the `develop` branch of the [pi4j repository](https://github.com/Pi4J/pi4j).
* Use a JDK version 25 or newer, e.g. `sdk use java 25.0.1-zulu`.
* In the root of the `pi4j directory, run `mvn clean install`.

```
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for Pi4J :: Parent POM 4.0.0-SNAPSHOT:
[INFO] 
[INFO] Pi4J :: Parent POM ................................. SUCCESS [  0.972 s]
[INFO] Pi4J :: DOCKER   :: Docker Parent POM .............. SUCCESS [  0.290 s]
[INFO] Pi4J :: TESTING  :: Arduino Test Harness ........... SUCCESS [  1.832 s]
[INFO] Pi4J :: LIBRARY  :: Libraries Parent POM ........... SUCCESS [  0.064 s]
[INFO] Pi4J :: LIBRARY  :: JNI Wrapper for PIGPIO Library . SUCCESS [  6.615 s]
[INFO] Pi4J :: LIBRARY  :: Java Library (CORE) ............ SUCCESS [  6.260 s]
[INFO] Pi4J :: PLUGIN   :: Plugins Parent POM ............. SUCCESS [  0.061 s]
[INFO] Pi4J :: PLUGIN   :: Mock Platform & Providers ...... SUCCESS [  0.683 s]
[INFO] Pi4J :: PLUGIN   :: PIGPIO I/O Providers ........... SUCCESS [  2.084 s]
[INFO] Pi4J :: PLUGIN   :: RaspberryPi Platform & Providers SUCCESS [  0.447 s]
[INFO] Pi4J :: TESTING  :: Unit/Integration Tests ......... SUCCESS [  2.350 s]
[INFO] Pi4J :: EXAMPLE  :: Sample Code .................... SUCCESS [  0.632 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
```
