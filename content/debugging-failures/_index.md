---
title: Debugging Failures
weight: 36
tags: ["Pi4J OS"]
aliases:
  - /getting-started/crowpi/crowpi-os
  - /getting-started/crowpi/crowpi-os/
---

Combining software with hardware can fail on many levels. You need the correct version of the Operating Systems, the good version of the Pi4J library, the wiring between the Raspberry Pi and the electronic components must be correct, and so on...

## Startup Failures

Always make sure that you log errors in the terminal or into a file! When the Pi4J library initializes, a lot of useful info is outputted. A successfull start looks like this:

```
Pi4J - New auto context
Pi4J - New context builder
BoardInfoHelper - Detected OS: Name: Linux, version: 6.6.20+rpt-rpi-v8, architecture: aarch64
BoardInfoHelper - Detected Java: Version: 21.0.2, runtime: 21.0.2+13-LTS, vendor: Azul Systems, Inc., vendor version: Zulu21.32+17-CA
BoardInfoHelper - Detected board type MODEL_4_B by code: c03112
DefaultContext - Detected board model: Raspberry Pi 4 Model B
DefaultContext - Running on: Name: Linux, version: 6.6.20+rpt-rpi-v8, architecture: aarch64
DefaultContext - With Java version: Version: 21.0.2, runtime: 21.0.2+13-LTS, vendor: Azul Systems, Inc., vendor version: Zulu21.32+17-CA
DefaultRuntime - Initializing Pi4J context/runtime...
...
DefaultRuntime - Pi4J context/runtime successfully initialized.
```

### Error GLIBC_2.33 not found

When the error `GLIBC_2.33 not found` is shown in the startup log, you need to update the Operating System as the required dependencies are not available to communicate with the GPIOs.

```
[main] ERROR com.pi4j.library.gpiod.util.NativeLibraryLoader - Unable to load [libgpiod.so] using path: [/lib/aarch64/pi4j-gpiod/libgpiod.so]
java.lang.UnsatisfiedLinkError: /tmp/libgpiod14998985341386605622.so: /lib/aarch64-linux-gnu/libc.so.6: version GLIBC_2.33' not found (required by /tmp/libgpiod14998985341386605622.so) at java.base/jdk.internal.loader.NativeLibraries.load(Native Method) at java.base/jdk.internal.loader.NativeLibraries$NativeLibraryImpl.open(NativeLibraries.java:388) at java.base/jdk.internal.loader.NativeLibraries.loadLibrary(NativeLibraries.java:232) at java.base/jdk.internal.loader.NativeLibraries.loadLibrary(NativeLibraries.java:174) at java.base/java.lang.ClassLoader.loadLibrary(ClassLoader.java:2394) at java.base/java.lang.Runtime.load0(Runtime.java:755) at java.base/java.lang.System.load(System.java:1970) at com.pi4j.library.gpiod@2.7.0/com.pi4j.library.gpiod.util.NativeLibraryLoader.loadLibraryFromClasspath(NativeLibraryLoader.java:261) at com.pi4j.library.gpiod@2.7.0/com.pi4j.library.gpiod.util.NativeLibraryLoader.load(NativeLibraryLoader.java:179) at com.pi4j.library.gpiod@2.7.0/com.pi4j.library.gpiod.internal.GpioD.<clinit>(GpioD.java:20) at com.pi4j.library.gpiod@2.7.0/com.pi4j.library.gpiod.internal.GpioDContext.initialize(GpioDContext.java:47) at com.pi4j.plugin.gpiod@2.7.0/com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalOutputProviderImpl.initialize(GpioDDigitalOutputProviderImpl.java:78) at com.pi4j.plugin.gpiod@2.7.0/com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalOutputProviderImpl.initialize(GpioDDigitalOutputProviderImpl.java:47) at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.initializeProvider(DefaultRuntimeProviders.java:276) at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.add(DefaultRuntimeProviders.java:252) at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.add(DefaultRuntimeProviders.java:232) at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.initialize(DefaultRuntimeProviders.java:357) at com.pi4j@2.7.0/com.pi4j.runtime.impl.DefaultRuntime.initialize(DefaultRuntime.java:318) at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContext.<init>(DefaultContext.java:113) at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContext.newInstance(DefaultContext.java:76) at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContextBuilder.build(DefaultContextBuilder.java:309) at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContextBuilder.build(DefaultContextBuilder.java:49) at com.pi4j@2.7.0/com.pi4j.Pi4J.newAutoContext(Pi4J.java:70) at com.pi4j.example@0.0.1/com.pi4j.example.MinimalExample.main(MinimalExample.java:91) Exception in thread "main" java.lang.UnsatisfiedLinkError: Pi4J was unable to extract and load the native library [/lib/aarch64/pi4j-gpiod/libgpiod.so] from the embedded resources inside this JAR [/home/pi/maven/pi4j-example-minimal/target/distribution/./pi4j-library-gpiod-2.7.0.jar]. to a temporary location on this system.  You can alternatively define the 'pi4j.library.path' system property to override this behavior and specify the library path. UNDERLYING EXCEPTION: [java.lang.UnsatisfiedLinkError]=/tmp/libgpiod14998985341386605622.so: /lib/aarch64-linux-gnu/libc.so.6: version GLIBC_2.33' not found (required by /tmp/libgpiod14998985341386605622.so)
at com.pi4j.library.gpiod@2.7.0/com.pi4j.library.gpiod.util.NativeLibraryLoader.load(NativeLibraryLoader.java:200)
at com.pi4j.library.gpiod@2.7.0/com.pi4j.library.gpiod.internal.GpioD.(GpioD.java:20)
at com.pi4j.library.gpiod@2.7.0/com.pi4j.library.gpiod.internal.GpioDContext.initialize(GpioDContext.java:47)
at com.pi4j.plugin.gpiod@2.7.0/com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalOutputProviderImpl.initialize(GpioDDigitalOutputProviderImpl.java:78)
at com.pi4j.plugin.gpiod@2.7.0/com.pi4j.plugin.gpiod.provider.gpio.digital.GpioDDigitalOutputProviderImpl.initialize(GpioDDigitalOutputProviderImpl.java:47)
at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.initializeProvider(DefaultRuntimeProviders.java:276)
at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.add(DefaultRuntimeProviders.java:252)
at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.add(DefaultRuntimeProviders.java:232)
at com.pi4j@2.7.0/com.pi4j.provider.impl.DefaultRuntimeProviders.initialize(DefaultRuntimeProviders.java:357)
at com.pi4j@2.7.0/com.pi4j.runtime.impl.DefaultRuntime.initialize(DefaultRuntime.java:318)
at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContext.(DefaultContext.java:113)
at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContext.newInstance(DefaultContext.java:76)
at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContextBuilder.build(DefaultContextBuilder.java:309)
at com.pi4j@2.7.0/com.pi4j.context.impl.DefaultContextBuilder.build(DefaultContextBuilder.java:49)
at com.pi4j@2.7.0/com.pi4j.Pi4J.newAutoContext(Pi4J.java:70)
at com.pi4j.example@0.0.1/com.pi4j.example.MinimalExample.main(MinimalExample.java:91)
```

## Unexpected Results on Electronic Components

If your software starts OK, and the log output shows that everything works as expected, but you still don't get the desired result on the connected electronic component, check:

* Are all the required wires connected?
* Are they connected correctly?
* Did you check the orientation of the pin numbering, where is pin 1?