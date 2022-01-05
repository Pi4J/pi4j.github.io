---
title: Build Java modules with Maven
weight: 161
---

{{% notice note %}}
At this moment this is the only way to distribute a Pi4J V2 project.
{{% /notice %}}

Because the Pi4J V2 project follows the modular approach of Java, the functionality of the framework has been split into
different modules, each with their own responsibility. 

The easiest way to start a new project, is to copy one of the example projects which include a full Maven pom.xml-file
with all the required steps and configurations to build the project with all its modules into the `target/distribution`
directory.

Take for instance a look at the ["Minimal example application"](/getting-started/minimal-example-application/).

When building this project with ...

```shell
$ mvn clean package
``` 

... you will find the generated package and required Java-modules and can start your application with the provided run.sh script:

```shell
$ cd target/distribution
$ ls -l
total 644
-rw-r--r-- 1 pi pi 364456 Jun 19 10:04 pi4j-core-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi   7243 Jun 19 10:04 pi4j-example-minimal-0.0.1.jar
-rw-r--r-- 1 pi pi 142461 Jun 19 10:04 pi4j-library-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  37302 Jun 19 10:04 pi4j-plugin-pigpio-2.0-SNAPSHOT.jar
-rw-r--r-- 1 pi pi  26917 Jun 19 10:04 pi4j-plugin-raspberrypi-2.0-SNAPSHOT.jar
-rwxr-xr-x 1 pi pi    101 Jun 19 10:04 run.sh
-rw-r--r-- 1 pi pi  52173 Jun 19 10:04 slf4j-api-2.0.0-alpha0.jar
-rw-r--r-- 1 pi pi  15372 Jun 19 10:04 slf4j-simple-2.0.0-alpha0.jar
$ sudo ./run.sh
``` 