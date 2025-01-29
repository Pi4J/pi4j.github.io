---
title: Download/Install
weight: 20
---

You can build the project from sources available on [GitHub](https://github.com/Pi4J/pi4j).

* Checkout the project [pi4j](https://github.com/Pi4J/pi4j)
* Use a JDK version 21 or newer, e.g. `sdk use java 21.0.6-zulu`
* In the root of pi4j run `mvn clean install`

```
[INFO] Executed tasks
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary for Pi4J :: Parent POM 2.0-SNAPSHOT:
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

## Example application

### Building the example application

* Checkout the project [Pi4J V.2 - Telegraph Demo Project](https://github.com/Pi4J/pi4j-demo-telegraph)
* Select JDK 21, e.g. `sdk use java 21.0.6-zulu`
* In the root of pi4j-demo-telegraph run `mvn clean install`
* Check the directory target\distribution --> this contains all the files to be copied to the Raspberry Pi

```
/target/distribution/pi4j-core-2.0-SNAPSHOT.jar
/target/distribution/pi4j-demo-telegraph-1.0-SNAPSHOT.jar
/target/distribution/pi4j-library-pigpio-2.0-SNAPSHOT.jar
/target/distribution/pi4j-plugin-pigpio-2.0-SNAPSHOT.jar
/target/distribution/pi4j-plugin-raspberrypi-2.0-SNAPSHOT.jar
/target/distribution/run.sh
/target/distribution/slf4j-api-2.0.0-alpha0.jar
/target/distribution/slf4j-simple-2.0.0-alpha0.jar
```

### Running on the Raspberry Pi

* After copying all files from target/distribution to a Raspberry Pi, start `./run.sh`