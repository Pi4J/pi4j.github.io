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

Always make sure that you log errors in the terminal or into a file! When the Pi4J library initializes, a lot of useful info is outputted. A **successful start** looks like this:

```shell
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

### Error `Pi4J provider [xxx-yy] could not be found`

You can get this error with a new application, or after you upgraded your code base to use Pi4J 2.6.0 or newer.

From version 2.6.0 on, each IO-Type has a single provider loaded. For example, you can no longer have `linuxfs-i2c` and `pigpio-i2c` loaded at the same time. When your application starts, you can check the logging output which will show the decisions used to select which providers are loaded. For example:

```bash
DefaultRuntime - Ignoring provider DIGITAL_INPUT RaspberryPi Digital Input (GPIO) Provider with priority 0 as lower priority than GpioD Digital Input (GPIO) Provider which has priority 150
DefaultRuntime - Ignoring provider DIGITAL_OUTPUT RaspberryPi Digital Output (GPIO) Provider with priority 0 as lower priority than GpioD Digital Output (GPIO) Provider which has priority 150
```

If you encounter this error, and the provider used in your code is not available, edit your `pom.xml to contain the provider you require and remove the other provider of the same IO-Type.

See [Choosing an I/O Provider](/documentation/providers/) for a more complete explanation.

### Error `GLIBC_2.33 not found`

When the error `GLIBC_2.33 not found` is shown in the startup log, you need to update the Operating System as the required dependencies are not available to communicate with the GPIOs.

```shell
[main] ERROR com.pi4j.library.gpiod.util.NativeLibraryLoader - Unable to load [libgpiod.so] using path: [/lib/aarch64/pi4j-gpiod/libgpiod.so]
java.lang.UnsatisfiedLinkError: /tmp/libgpiod14998985341386605622.so: /lib/aarch64-linux-gnu/libc.so.6: version GLIBC_2.33' not found (required by /tmp/libgpiod14998985341386605622.so) at java.base/jdk.internal.loader.NativeLibraries.load(Native Method) at java.base/jdk.internal.loader. 
... 
Exception in thread "main" java.lang.UnsatisfiedLinkError: Pi4J was unable to extract and load the native library [/lib/aarch64/pi4j-gpiod/libgpiod.so] from the embedded resources inside this JAR [/home/pi/maven/pi4j-example-minimal/target/distribution/./pi4j-library-gpiod-2.7.0.jar]. to a temporary location on this system.  You can alternatively define the 'pi4j.library.path' system property to override this behavior and specify the library path. 
```

### Error `pigpio initialisation failed`

For some Pi4J functionality, `root` privileges are required. If you get an error like this, you need to execute your application with `sudo`:

```shell
[main] INFO com.pi4j.util.Console -
[main] WARN com.pi4j.library.pigpio.impl.PiGpioNativeImpl - PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
Exception in thread "main" java.lang.reflect.UndeclaredThrowableException
...
Caused by: java.lang.reflect.InvocationTargetException
...
Caused by: com.pi4j.library.pigpio.PiGpioException: PIGPIO ERROR: PI_INIT_FAILED; pigpio initialisation failed
```

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
