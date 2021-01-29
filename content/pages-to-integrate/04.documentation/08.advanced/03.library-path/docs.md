---
title: 'Native Library Path'
taxonomy:
    category:
        - docs
visible: true
---

#### Overview 

Some Pi4J plugins, such as the Pi4J PiGpio Provider plugin, depend on native JNI libraries to communicate with the underlying system.  By default Pi4J embeds these native libraries as resources inside the plugin's JAR file.  At runtime Pi4J extracts the native library into a temporary directory so the JVM can load the library from the filesystem.  Upon termination the temporary file is automatically removed.  

This automatic extration behavior works well for most users; however, there are certain edge cases where this may fail.  On failure, its common to see a `UnsatisfiedLinkError` on startup of your application or when you create a Pi4J context.  Edge cases such as the following may require customization of the runtime to deal with native library loading.

* Systems that do not support a writable temporary directory (`/tmp`) may encounter the `UnsatisfiedLinkError` and fail to load the native library.
* Systems with very strict security policies may encounter the `UnsatisfiedLinkError` and fail to load the native library if unable to extract the resource from the JAR at runtime.
* Users attempting to use Pi4J under Android may also experience the `UnsatisfiedLinkError` and fail to load the native library.

---

#### Explicitly Define the Library Path

In the event of a failure to extract and load the embedded native library from the JAR file at runtime, a user can override this default behavior by defining the system property: `pi4j.library.path`.

##### Usage:
```
pi4j.library.path=(system|/some/directory)
``` 

##### Values:
| Property Value |  Description |
| --- | --- |
| `system` | The default system defined library path for the JVM (`java.library.path`) will be used to resolve the native libraries. |
| `local` | Native libraries will be resolved in the same local directory as the plugin JAR file on the file system. |
| absolute file path<br/>(`/some/directory`) | This user defined library path (_absolute filesystem path_) will be used to resolve the native libraries. |

##### Examples:
The `pi4j.library.path` system property can be assigned in the command line used to launch your Java application using the `-D` flag.
```
java --Dpi4j.library.path="system" ...
-or-
java --Dpi4j.library.path="local" ...
-or-
java --Dpi4j.library.path="/some/directory" ...

```

The `pi4j.library.path` system property can be assigned in your code at startup and prior to creating a Pi4J Context.
```
System.setProperty("pi4j.library.path", "/some/directory");
-or-
System.setProperty("pi4j.library.path", "system");
-or-
System.setProperty("pi4j.library.path", "local");
```

!!! **Note:** &nbsp;&nbsp; For more details about the native library loading behavior, please see the [`NativeLibraryLoader.java`](https://github.com/Pi4J/pi4j-v2/blob/master/libraries/pi4j-library-pigpio/src/main/java/com/pi4j/library/pigpio/util/NativeLibraryLoader.java) class:  https://github.com/Pi4J/pi4j-v2/blob/master/libraries/pi4j-library-pigpio/src/main/java/com/pi4j/library/pigpio/util/NativeLibraryLoader.java

---

#### Where To Get The Native Libraries

The Pi4J native libraries can be obtained by extracting the architecture specific `libpi4j-xxx.so` file from the plugin JAR file's resources.  

Additionally, the Pi4J native libraries are published as independant artifacts in the Maven Repository:
https://oss.sonatype.org/#nexus-search;quick~pi4j-library-pigpio


