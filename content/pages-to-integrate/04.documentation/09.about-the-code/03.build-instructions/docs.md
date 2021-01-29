---
title: 'Build Instructions'
---

Building the Pi4J Project is simple and requires minimal effort.  Pi4J is primarily built using Apache Maven and Java 11.  Pi4J can be built directly on your host computer or inside a Docker container where all toolchains and dependencies are already installed, configuired and cached.   

! **Note**: if you wish to build using a Docker container, please skip ahead to the [_Building with Docker_](#building-with-docker) topic.



---

### Prerequsites

In order to build  Pi4J, the host system must have the following toolchains pre-installed.

| Name | Version | URL |
| --- | --- | -- |
| Java Development Kit (JDK) |  11.0.7 (_or newer_)   | https://openjdk.java.net/ |
| Apache Maven |  3.6.3 (_or newer_)   | https://maven.apache.org/download.cgi |

---

### Build Environment

The `JAVA_HOME` system environment variable must be configiured to point to the JDK installed path.

---

### Building with Maven

To build the Pi4J project, use the following Maven comand from the parent Pi4J directory.
```
mvn clean install
```
If you prefer to skip all unit/integration testing, use the folllowing Maven command:
```
mvn clean install -DskipTests
```

---

### Building with Docker

Alternatively, the Pi4J project can be entirely compiled inside a prebuilt Pi4J Builder Docker container.  This eliminates the need/requirement to install the build toolchains and configure your system to build Pi4J.  To build the Pi4J project using Docker, run the following shell script from the parent Pi4J directory.
```
./build-docker.sh
```

The project which provides these Docker images can be found on [GitHub > Pi4J/pi4j-docker](https://github.com/Pi4J/pi4j-docker) and includes an extensive README with the full info on how to build and use these images.

!!! Extract from the README:

<p>This project contains the Dockerfiles and build scripts to create the Pi4J builder<br>
docker images used for compiling/building the Pi4J projects.  The Pi4J builder images
include the following:</p>
<ul>
<li>
<p><strong><a href="https://hub.docker.com/repository/docker/pi4j/pi4j-builder-base" rel="nofollow">Pi4J Base Builder</a></strong> <code>pi4j/pi4j-builder-base:latest</code> :
This is the base image used by all the other builder images.  It's based on Ubuntu 18.04
with JDK 11 and Maven pre-installed.  This image's entry point is a Bash shell.
(<a href="https://hub.docker.com/repository/docker/pi4j/pi4j-builder-base" rel="nofollow">https://hub.docker.com/repository/docker/pi4j/pi4j-builder-base</a>)</p>
</li>
<li>
<p><strong><a href="https://hub.docker.com/repository/docker/pi4j/pi4j-builder-native" rel="nofollow">Pi4J Native Builder</a></strong> <code>pi4j/pi4j-builder-native:latest</code> :
This image is derived from <code>pi4j/pi4j-builder-base</code> and adds support for native cross-compilers
and build tools for architectures: <code>arm</code>, <code>armhf</code>, <code>aarch64/arm64</code>.  This image's
entry point is a bash shell attempting to execute the file <code>./build.sh</code> in the volume mounted
under the <code>/build</code> path.</p>
</li>
<li>
<p><strong><a href="https://hub.docker.com/repository/docker/pi4j/pi4j-builder:1.4" rel="nofollow">Pi4J v1.4 Builder</a></strong> <code>pi4j/pi4j-builder:1.4</code> :
This image is derived from <code>pi4j/pi4j-builder-native</code> and additionally includes pre-cached Maven
build plugins and dependencies for <a href="http://github.com/Pi4J/pi4j">Pi4J v1.4</a> builds.  This image's
entry point is a Maven shell.  If not explicitly provided, the default maven build arguments will be:
<code>clean install -DskipTests -Pall-platforms</code>.  This will effectively build all Pi4J projects including
the <code>pi4j-native</code> project containing native libraries which will be cross-compiled for RaspberryPi/ARM
(32-bit &amp; 64-bit) devices.</p>
</li>
<li>
<p><strong><a href="https://hub.docker.com/repository/docker/pi4j/pi4j-builder:2.0" rel="nofollow">Pi4J v2.0 Builder</a></strong> <code>pi4j/pi4j-builder:2.0</code> :
This image is derived from <code>pi4j/pi4j-builder-native</code> and additionally includes pre-cached Maven
build plugins and dependencies for <a href="http://github.com/Pi4J/pi4j-v2">Pi4J v2.0</a> builds.  This image's
entry point is a Maven shell.  If not explicitly provided, the default maven build arguments will be:
<code>clean install -DskipTests -native</code>.  This will effectively build all Pi4J projects including
the native library projects which will be cross-compiled for RaspberryPi/ARM (32-bit &amp; 64-bit) devices.</p>
</li>
</ul>
<p><strong>Note:</strong> Pi4J versions prior to v1.4 are not currently tested or supported in these Docker images.</p>

---

### Building Pi4J Native Libraries

Pi4J V2 also includes native libraries that will need to be compiled if you are modifying any native code.  Most users will never need to compile the native libraries as these artifacts are automatically downloaded  when building the Pi4J JARs from Maven repositories. One of the following commands can be used to build the Pi4J JARs and Native Libraries:
```
mvn clean install -Pnative
mvn clean install -Pnative,docker
mvn clean install -Pnative,cross-compile
```
!!! **Note:** See the custom build profiles in the [Custom Build Profiles](#custom-build-profiles) section for more information about the profiles illustrated in these commands.

Additional information about Docker Builds vs Cross-Compiler builds can be found here:
https://github.com/Pi4J/pi4j-v2/issues/21#issuecomment-651976487

!! **TODO**::  Create a topic here detailing Docker builds vs Cross-compiler builds.

---

### Custom Build Profiles

The Pi4J Maven build includes a number of custom profiles that can be activated to perform various build steps.

| Profile | Description | Notes |
| --- | --- | --- |
| `sources` |  Package raw sources for each JAR   |  Only needed when performing a snapshot or release build. |
| `javadoc` |  Compile and package JavaDoc for each JAR   |  Only needed when performing a snapshot or release build. |
| `native` |  Compile any native libraries included in the build  |  Only needed when modifying native code or performing a snapshot or release build. |
| `docker` |  Use docker builder containers to compile native library artifacts  |  Only used when incuding the `native` profile or performing a snapshot or release build. |
| `cross-compile` |  Use cross-compilers on host to compile native library artifacts  | Only used when incuding the `native` profile or performing a snapshot or release build. |
| `test-hardware` |  Perform hardware integration testing  | EXPERIMENTAL |
| `mac` |  Use docker builder containers to compile native library artifacts (Same as `docker` profile)  | Automatically activated when running build from a MacOS host system. |
| `windows` |  Use docker builder containers to compile native library artifacts (Same as `docker` profile)  | Automatically activated when running build from a Windows host system. |
| `transfer` |  Perform SSH/SCP file transfers for each JAR to a remote Raspberry Pi  | Used for parallel development and testing. |



You can activate a build profile using the `-P`{profile-name} argument in the Maven command:

```
mvn clean install -Pjavadoc
```

### Release/Snapshot Builds

Pi4J release and snapshot builds are reserved for the Pi4J Development Team.  A release build ensures all JARs, resources, source-bundles, native libraries, and javadoc artifacts are compiled and deployed to the public Maven repositories.  You can use the following command to perform all the build steps that would be performed during a release or snapshot build.
```
mvn clean install -Drelease-build
```



