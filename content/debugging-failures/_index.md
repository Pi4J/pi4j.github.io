---
title: Debugging Failures
weight: 37
tags: ["Pi4J OS"]
aliases:
  - /getting-started/crowpi/crowpi-os
  - /getting-started/crowpi/crowpi-os/
---

Combining software with hardware can fail on many levels. You need the correct version of the Operating Systems, the good version of the Pi4J library, the wiring between the Raspberry Pi and the electronic components must be correct, and so on...

## Startup Failures

Always make sure that you log errors in the terminal or into a file! When the Pi4J library initializes, a lot of useful info is outputted. A **successful start** looks like this:

```shell
Pi4J - New auto context
Pi4J - New context builder
BoardInfoHelper - Detected OS: Name: Linux, version: 6.6.20+rpt-rpi-v8, architecture: aarch64
BoardInfoHelper - Detected Java: Version: 25, runtime: 25+36-LTS, vendor: Azul Systems, Inc., vendor version: Zulu25.28+85-CA
BoardInfoHelper - Detected board type MODEL_4_B by code: c03112
DefaultContext - Detected board model: Raspberry Pi 4 Model B
DefaultContext - Running on: Name: Linux, version: 6.6.20+rpt-rpi-v8, architecture: aarch64
DefaultContext - With Java version: Version: 25, runtime: 25+36-LTS, vendor: Azul Systems, Inc., vendor version: Zulu25.28+85-CA
DefaultRuntime - Initializing Pi4J context/runtime...
...
DefaultRuntime - Pi4J context/runtime successfully initialized.
```

### Error `Pi4J provider [xxx-yy] could not be found`

You can get this error when the code (or a code example you copied) explicitly requests a provider ID that isn't loaded, for instance a leftover `.provider("pigpio-i2c")` call from a V4 project that hasn't been migrated yet. Since Pi4J V5 only ships the `ffm-*` and `mock-*` providers, remove the `.provider(...)` call (or update it to the `ffm-*`/`mock-*` id) so the auto-loaded provider is used.

See [Choosing an I/O Provider](/documentation/providers/) for a more complete explanation.

### Error: `Could not execute cat /proc/cpuinfo | grep 'Revision' | awk '{print $3}' to detect the board model`

This error occurs in Pi4J **version 2.7.0**, due to a problem where a shell command is used to detect the board model, but fails with a permission error (`IOException: Cannot run program "sh": error=13, Permission denied`).

**Solutions:**
1. **Upgrade to Pi4J Version 2.7.1 or Newer:**
In version 2.7.1, this issue has been resolved. The `/proc/cpuinfo` file is read directly in Java without using shell commands, avoiding the permission issue entirely.

2. **Grant Execution Permission to** `jspawnhelper`:
If upgrading is not immediately possible, you can manually fix the issue by ensuring the `jspawnhelper` utility in the Java runtime has execution permissions. Run the following command:

```shell
chmod +x JAVA_HOME/lib/jspawnhelper
```

Replace `JAVA_HOME` with the actual path to your Java installation. This ensures that Java can execute shell commands without permission errors.

## Unexpected Results on Electronic Components

If your software starts OK, and the log output shows that everything works as expected, but you still don't get the desired result on the connected electronic component, check:

* Are all the required wires connected?
* Are they connected correctly?
* Did you check the orientation of the pin numbering, where is pin 1?

## Related to functionality existing in V4, but no longer included in V5

### Error `GLIBC_2.33 not found`

This error was shown in the startup log of the GpioD provider (removed in V5) when the required kernel dependencies were not available:

```shell
[main] ERROR com.pi4j.library.gpiod.util.NativeLibraryLoader - Unable to load [libgpiod.so] using path: [/lib/aarch64/pi4j-gpiod/libgpiod.so]
java.lang.UnsatisfiedLinkError: /tmp/libgpiod14998985341386605622.so: /lib/aarch64-linux-gnu/libc.so.6: version GLIBC_2.33' not found (required by /tmp/libgpiod14998985341386605622.so) at java.base/jdk.internal.loader.NativeLibraries.load(Native Method) at java.base/jdk.internal.loader. 
... 
Exception in thread "main" java.lang.UnsatisfiedLinkError: Pi4J was unable to extract and load the native library [/lib/aarch64/pi4j-gpiod/libgpiod.so] from the embedded resources inside this JAR [/home/pi/maven/pi4j-example-minimal/target/distribution/./pi4j-library-gpiod-2.7.0.jar]. to a temporary location on this system.  You can alternatively define the 'pi4j.library.path' system property to override this behavior and specify the library path. 
```

### Error `pigpio initialisation failed`

The PiGpio provider (removed in V5) required `root` privileges for some functionality. If you got an error like this, you needed to execute your application with `sudo`:

```shell
[main] INFO com.pi4j.util.Console -
[main] WARN com.pi4j.library.pigpio.impl.PiGpioNativeImpl - PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
Exception in thread "main" java.lang.reflect.UndeclaredThrowableException
...
Caused by: java.lang.reflect.InvocationTargetException
...
Caused by: com.pi4j.library.pigpio.PiGpioException: PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
```
