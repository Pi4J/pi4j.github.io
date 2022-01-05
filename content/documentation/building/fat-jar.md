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
| pi4j-example-fatjar-0.0.1.jar                       | 6 KB      |
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

Pi4J V2 uses ServiceLoader to detect which modules are available to communicate with the GPIOs. This allows to very dynamically extend the possibilities of the framework.

Code extract from [pi4j-core/src/.../runtime/impl/DefaultRuntime.java](https://github.com/Pi4J/pi4j-v2/blob/develop/pi4j-core/src/main/java/com/pi4j/runtime/impl/DefaultRuntime.java#L224):

```java
// detect available Pi4J Plugins by scanning the classpath looking for plugin instances
var plugins = ServiceLoader.load(Plugin.class);
```

TODO further explain problem here...