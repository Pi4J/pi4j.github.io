---
title: Using Board Info
weight: 99
---

{{% notice tip %}}
GITHUB Sources of BoardInfoHelper.java and the data model: [pi4j/pi4j-core/src/main/java/com/pi4j/boardinfo/util/BoardInfoHelper.java](https://github.com/Pi4J/pi4j/blob/develop/pi4j-core/src/main/java/com/pi4j/boardinfo/util/BoardInfoHelper.java)
{{% /notice %}}

Since V2.6.0, the new class `BoardInfoHelper` provides the following info:

* Type of Raspberry Pi board as a `BoardInfo` object.
* If the system uses a RP1 chip with `usesRP1()` (Raspberry Pi 5 only at this moment).
* If the system is 32-bit or 64-bit with `is32bit()` and `is64bit()`.
* The amount of memory available and used by the JVM as a `JvmMemory` object.
* Info about volt, temperature, etc. as a `BoardReading` object.

The board info is used in some of the plugins to set the correct priority, based on the use of a Raspberry Pi 5 ([with RP1](https://www.raspberrypi.com/documentation/microcontrollers/rp1.html)) versus earlier board (without RP1).

## How the Board Model is Detected

### Previous Method (< 2.7.1 version)
In earlier versions, the board model was determined by reading the board version number from the `/proc/cpuinfo` file using shell commands:

```shell
$ cat /proc/cpuinfo | grep 'Revision' | awk '{print $3}'
```

### Updated Method (>= 2.7.1 version)
Starting with version 2.7.1, the board version number is determined programmatically in Java using the [CpuInfoReader](https://github.com/Pi4J/pi4j/blob/develop/pi4j-core/src/main/java/com/pi4j/boardinfo/datareader/CpuInfoReader.java) class. This method reads and processes the `/proc/cpuinfo` file to extract the CPU revision.


For instance, for a Raspberry Pi Compute 4, multiple version numbers are possible:

```java
COMPUTE_4("Compute Module 4", STACK_ON_COMPUTER,
        Arrays.asList("a03140", "b03140", "c03140", "d03140", "a03141", "b03141", "c03141", "d03141"),
        ...)
```

## Demo Use on api.pi4j.com

The new `BoardInfoHelper` class and the related enums and methods are used as the basis for the website [api.pi4j.com](https://api.pi4j.com) that visualizes all the info defined inside the library, like board info, header pins, type of pins, etc. This website runs on a Raspberry Pi board, so the [System Information screen](https://api.pi4j.com/system-information) show the info about that board using this new class.

{{< gallery >}}
{{< figure link="/assets/documentation/api-boards.png" caption="List of boards defined in the library" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/api-system-information.png" caption="System Information of the Raspberry Pi running the website" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

## Examples

### Example Code

```java
var console = new Console();
var pi4j = Pi4J.newAutoContext();

// ------------------------------------------------------------
// Output Pi4J Board information
// ------------------------------------------------------------
// When the Pi4J Context is initialized, a board detection is 
// performed. You can use this info in case you need board-specific
// functionality.
// OPTIONAL

// Display board information
console.println("Board model: " + pi4j.boardInfo().getBoardModel().getLabel());
console.println("Operating system: " + pi4j.boardInfo().getOperatingSystem());
console.println("Java versions: " + pi4j.boardInfo().getJavaInfo());

// Access additional info via BoardInfoHelper
console.println("Board model: " + BoardInfoHelper.current().getBoardModel().getLabel());
console.println("Raspberry Pi model with RP1 chip (Raspberry Pi 5): " + BoardInfoHelper.usesRP1());
console.println("OS is 64-bit: " + BoardInfoHelper.is64bit());
console.println("JVM memory used (MB): " + BoardInfoHelper.getJvmMemory().getUsedInMb());
console.println("Board temperature (°C): " + BoardInfoHelper.getBoardReading().getTemperatureInCelsius());

// Access throttled states
var throttledStates = BoardInfoHelper.getBoardReading().getThrottledStates();
console.println("Throttled states: ");
throttledStates.forEach(state -> console.println(" - " + state.name()));

console.println("Throttled states description: " + BoardInfoHelper.getBoardReading().getThrottledStatesDescription());
```

### Example Output

```bash
[main] INFO com.pi4j.util.Console - Board model: Raspberry Pi 4 Model B
[main] INFO com.pi4j.util.Console - Operating system: Name: Linux, version: 6.1.21-v8+, architecture: aarch64
[main] INFO com.pi4j.util.Console - Java versions: Version: 22, runtime: 22+36, vendor: Azul Systems, Inc., vendor version: Zulu22.28+91-CA

[main] INFO com.pi4j.util.Console - Board model: Raspberry Pi 4 Model B
[main] INFO com.pi4j.util.Console - Raspberry Pi model with RP1 chip (Raspberry Pi 5): false
[main] INFO com.pi4j.util.Console - OS is 64-bit: true
[main] INFO com.pi4j.util.Console - JVM memory used (MB): 10.910163879394531
[main] INFO com.pi4j.util.Console - Board temperature (°C): 61.3

[main] INFO com.pi4j.util.Console - Throttled states: 
[main] INFO com.pi4j.util.Console -  - UNDERVOLTAGE_DETECTED
[main] INFO com.pi4j.util.Console -  - SOFT_TEMPERATURE_LIMIT_ACTIVE
[main] INFO com.pi4j.util.Console - Throttled states description: Under-voltage detected, Soft temperature limit active
```

## Overriding the Detected Board

In case the detected board is wrong or unknown, you can override it since V3.0.1 with the following method. Make sure to do this before the Pi4J context is initialized, so the correct plugins are loaded.

```java
// With default GpioD chip
BoardInfoHelper.current().setBoardModel(BoardModel.GENERIC);
var pi4j = Pi4J.newAutoContext();

// Or if you want to use a specific chip name
BoardInfoHelper.current().setBoardModel(BoardModel.GENERIC);
var pi4j = Pi4J.newContextBuilder()
    .add(GpioDDigitalInputProvider.newInstance())
    .setGpioChipName("gpiochip2")
    .build();
```

Two generic boards where created for this use-case, but of course, you can also use one of the other [BoardModel](https://github.com/Pi4J/pi4j/blob/develop/pi4j-core/src/main/java/com/pi4j/boardinfo/definition/BoardModel.java) enum values.

```java
    // Generic model, this can be used to force the library
    // to load Raspberry Pi plugins on other board types
    GENERIC("Generic board compatible with Raspberry Pi 4", SINGLE_BOARD_COMPUTER,
        new ArrayList<>(),
        PiModel.MODEL_B,
        HeaderVersion.TYPE_3,
        LocalDate.now(),
        Soc.UNKNOWN,
        Cpu.UNKNOWN, 4,
        new ArrayList<>(),
        new ArrayList<>()),
    GENERIC_RP1("Generic board compatible with Raspberry Pi 5", SINGLE_BOARD_COMPUTER,
        new ArrayList<>(),
        PiModel.MODEL_B,
        HeaderVersion.TYPE_3,
        LocalDate.now(),
        Soc.UNKNOWN,
        Cpu.UNKNOWN, 4,
        new ArrayList<>(),
        new ArrayList<>(),
        new ArrayList<>(),
        true),
```


