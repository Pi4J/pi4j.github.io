---
title: Build as a FAT JAR with Maven
weight: 162
---

{{% notice note %}}
Pi4J V2 projects as FAT JAR don't work at this moment.
<br/><br/>
This document is a description of the current problem in preparation of a discussion to find a solution... 
{{% /notice %}}

## About FAT JARs

With Pi4J V1 you can create a so-called FAT JAR, which packages all the dependencies into one jar-file. That way it is
very easy to build your project on one computer and distribute your application as a single file to one or more clients.

Because of the modular approach and how Pi4J V2 loads it dependencies at runtime, this approach is no longer working.

## Example FAT JAR project

To illustrate the problem, a simple project has been created on 
[github.com/Pi4J/pi4j-example-fatjar](https://github.com/Pi4J/pi4j-example-fatjar/).

The pom.xml-file uses the `maven-assembly-plugin` plugin to create the FAT JAR:

```xml
<plugin>
    <artifactId>maven-assembly-plugin</artifactId>
    <version>${maven-assembly-plugin.version}</version>
    <configuration>
        <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
        <archive>
            <manifest>
                <addClasspath>true</addClasspath>
                <mainClass>com.pi4j.example.MinimalExample</mainClass>
            </manifest>
        </archive>
    </configuration>
    <executions>
        <execution>
            <id>make-assembly</id>
            <phase>package</phase>
            <goals>
                <goal>single</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

When building the project with `mvn package` the following two files are created in the `target` directory:

| File                                                | File size |
|:----------------------------------------------------|----------:|
| pi4j-example-fatjar-0.0.1.jar                       |      6 KB |
| pi4j-example-fatjar-0.0.1-jar-with-dependencies.jar |    538 KB |  

As a jar-file is actually a zip-file, we can easily check the contents

* directories
  * com
  * lib
  * META-INF
  * org
* files
  * LICENSE.txt
  * module-info.class
  * NOTICE.txt
  * README.md

## Problem to load the Pi4J modules

Pi4J V2 uses ServiceLoader to detect which modules are available to communicate with the GPIOs. This allows to very 
dynamically extend the possibilities of the framework.

Code extract from [pi4j-core/src/.../runtime/impl/DefaultRuntime.java](https://github.com/Pi4J/pi4j-v2/blob/develop/pi4j-core/src/main/java/com/pi4j/runtime/impl/DefaultRuntime.java#L224):

```java
// detect available Pi4J Plugins by scanning the classpath looking for plugin instances
var plugins = ServiceLoader.load(Plugin.class);
```

The problem is located here as every module has a com.pi4j.extension.Plugin file. When you make a fat jar, only one of 
those files survives and thus the module for which the service file doesn't exist anymore in the fat jar isn't loaded.

In the example file we only see the file com.pi4j.plugin.raspberrypi.RaspberryPiPlugin entry, thus missing all the other plugins.

![Unpacked fat jar with the problem META-INF file](/assets/documentation/fat-jar-problem.png)

The content of this file only contains a single plugin:

```
com.pi4j.plugin.raspberrypi.RaspberryPiPlugin
```

If we look into the sources of the Pi4J V2 project, we see each file has its own META-INF service file.

![The META-INF files of all plugins](/assets/documentation/plugin-meta-inf-files.png)

So would probably need the combined results in the fat jar META-INF file?

``` 
com.pi4j.plugin.linuxfs.LinuxFsPlugin
com.pi4j.plugin.pigpio.PiGpioPlugin
com.pi4j.plugin.raspberrypi.RaspberryPiPlugin
```

When using `maven-shade-plugin` instead of `maven-assembly-plugin` more output is given which actually shows this exact problem:

``` 
[INFO] Including org.slf4j:slf4j-api:jar:1.7.32 in the shaded jar.
[INFO] Including org.slf4j:slf4j-simple:jar:1.7.32 in the shaded jar.
[INFO] Including com.pi4j:pi4j-core:jar:2.0 in the shaded jar.
[INFO] Including com.pi4j:pi4j-plugin-raspberrypi:jar:2.0 in the shaded jar.
[INFO] Including com.pi4j:pi4j-plugin-pigpio:jar:2.0 in the shaded jar.
[INFO] Including com.pi4j:pi4j-library-pigpio:jar:2.0 in the shaded jar.
[WARNING] Discovered module-info.class. Shading will break its strong encapsulation.
[WARNING] Discovered module-info.class. Shading will break its strong encapsulation.
[WARNING] Discovered module-info.class. Shading will break its strong encapsulation.
[WARNING] Discovered module-info.class. Shading will break its strong encapsulation.
[WARNING] Discovered module-info.class. Shading will break its strong encapsulation.
[WARNING] pi4j-core-2.0.jar, pi4j-example-fatjar-0.0.1.jar, pi4j-library-pigpio-2.0.jar, pi4j-plugin-pigpio-2.0.jar, pi4j-plugin-raspberrypi-2.0.jar, slf4j-api-1.7.32.jar, slf4j-simple-1.7.32.jar define 1 overlapping resource:
[WARNING]   - META-INF/MANIFEST.MF
[WARNING] pi4j-core-2.0.jar, pi4j-library-pigpio-2.0.jar, pi4j-plugin-pigpio-2.0.jar, pi4j-plugin-raspberrypi-2.0.jar define 3 overlapping resources:
[WARNING]   - LICENSE.txt
[WARNING]   - NOTICE.txt
[WARNING]   - README.md
[WARNING] pi4j-plugin-pigpio-2.0.jar, pi4j-plugin-raspberrypi-2.0.jar define 1 overlapping resource:
[WARNING]   - META-INF/services/com.pi4j.extension.Plugin
[WARNING] maven-shade-plugin has detected that some class files are
[WARNING] present in two or more JARs. When this happens, only one
[WARNING] single version of the class is copied to the uber jar.
[WARNING] Usually this is not harmful and you can skip these warnings,
[WARNING] otherwise try to manually exclude artifacts based on
[WARNING] mvn dependency:tree -Ddetail=true and the above output.
[WARNING] See http://maven.apache.org/plugins/maven-shade-plugin/
```