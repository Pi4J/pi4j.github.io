---
title: 'Maven settings'
---

To simplify development but not commit sensitive information, you can add personal or PC-specific settings in the Maven settings.xml file. This file is stored or needs to be created in the ".m2" directory in your home directory:
* Windows: C:\Users\YOUR_NAME\.m2
* Linux: /home/YOUR_NAME/.m2
* Mac: /Users/YOUR_NAME/.m2

For more info see [this article on Baeldung](https://www.baeldung.com/maven-local-repository).

This is an example settings file, including settings for compiling of Pi4J and credentials to upload the generated code to a Raspberry Pi.

```
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
      <localRepository/>
      <interactiveMode/>
      <offline/>
      <pluginGroups/>
      <servers/>
      <mirrors/>
      <proxies/>
  
  <profiles>
    <profile>
      <id>pi4j</id>
      <properties>
        <!-- Docker compiler settings -->
        <pi4j.native.compiler>DOCKER-COMPILER</pi4j.native.compiler>
        
        <!-- SSH credentials of your test Raspberry Pi -->
  	    <pi4j.dev.transfer>false</pi4j.dev.transfer>
        <pi4j.dev.host>192.168.1.1</pi4j.dev.host>
        <pi4j.dev.port>22</pi4j.dev.port>
        <pi4j.dev.user>pi</pi4j.dev.user>
        <pi4j.dev.password>raspberry</pi4j.dev.password>
        <pi4j.dev.directory>/home/pi/pi4j-temp</pi4j.dev.directory>  
      </properties>
    </profile>
  </profiles>
   
  <activeProfiles>
    <activeProfile>pi4j</activeProfile>
  </activeProfiles>

</settings>
```