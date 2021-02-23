---
title: User interface with JavaFX
weight: 70
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-example-javafx](https://github.com/Pi4J/pi4j-example-javafx)
{{% /notice %}}

JavaFX is a framework to create user interfaces for desktop (Windows, Mac, Linux) and mobile phones. JavaFX is
an opensource project which is documented on [openjfx.io](https://openjfx.io/) and the sources are available
in [this GitHub project](https://github.com/openjdk/jfx). 

The main goal of Java has always been to be able to create applications which are **"write once, run everywhere"**.

[Gluon](https://gluonhq.com/) is the main maintainer of the OpenJFX project and offers commercial support to 
companies who want to use JavaFX in critical applications. They also provide [tools to build and compile Java 
code to native applications for all platforms](https://gluonhq.com/products/).

# JavaFX on Raspberry Pi

JavaFX is also an ideal framework to build Java applications with a user interface for the Raspberry Pi.

You can find a runtime version dedicated to the Raspberry Pi on the [Gluon download page](https://gluonhq.com/products/javafx/).
Let's install it on our board, so we can start Java+JavaFX applications which make best use of the capabilities 
of the Raspberry Pi.

## Installation

To get the latest version on your Raspberry Pi:

* check the Gluon download page for the download link
* download the file 
* unzip the file
* move the unzipped directory to the opt-directory (optionally, but it's a logical place)

```
$ wget -O openjfx.zip https://gluonhq.com/download/javafx-linux-arm32-drm-sdk/
$ unzip openjfx.zip
$ sudo mv arm32fb-sdk/ /opt/arm32fb-sdk/
```

## Start an application 

Now the OpenJFX-runtime is available on our Raspberry Pi, we can start each Java application which was compiled
to a JAR with some additional parameters to run it with the best rendering support.

```
java \
  -Dmonocle.egl.lib=/opt/arm32fb-sdk/lib/libgluon_drm.so \
  -Djava.library.path=/opt/arm32fb-sdk/lib \
  -Dmonocle.platform.traceConfig=false \
  -Dprism.verbose=false \
  -Djavafx.verbose=false \
  -Dmonocle.platform=EGL \
  --module-path /opt/arm32fb-sdk/lib:. \
  --add-modules javafx.controls \
  --module {YOUR_MAIN_CLASS} $@
```

# Minimal example application

TODO