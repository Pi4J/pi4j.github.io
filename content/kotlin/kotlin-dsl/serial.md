---
title: Serial Kotlin DSL
description: "SERIAL (UART/RS232) DSL Pi4J-Kotlin"
weight: 50
---

{{% notice tip %}}
Feel free to checkout the [Pi4J docs on Serial](/documentation/io-examples/serial/)
{{% /notice %}}

## Installation

Add PiGPIO dependency
```kotlin
dependencies {
    implementation("com.pi4j:pi4j-plugin-pigpio:2.3.0")
}
```

## Serial DSL

```kotlin
serial("/dev/ttyS0") {
    use_9600_N81()
    dataBits_8()
    parity(Parity.NONE)
    stopBits(StopBits._1)
    flowControl(FlowControl.NONE)
    piGpioSerialProvider()
}.open {
  // use here. 
}
```

## Minimal Serial Example

{{% notice info %}}
This is the Kotlin DSL version of the same [Serial example here](/documentation/io-examples/serial#code-example), but leveraging the Kotlin DSL
{{% /notice %}}

```kotlin

serial("/dev/ttyS0") {
    // ..
}.open {
    console {
        +"Waiting till serial port is open"
        while (!isOpen) {
            print(".")
            sleep(250)
        }
        println()
        +"Serial port is open"
        startDaemon {
            inputStream.bufferedReader().use {
                while (true) {
                    if (available() != 0) sleep(10)
                    else buildString {
                        (0 until available()).forEach { _ ->
                            readByte().let { b ->
                                // All non-string bytes are handled as line breaks
                                if (b < 32) return@forEach
                                else append(b.toInt().toChar())
                            }
                        }
                    }.also { +"Data: '$it'" }
                }
            }
        }
        while (isOpen) sleep(500)
    }
}
```

And `startDaemon` is defined as:
``` kotlin
fun startDaemon(runnable: Runnable) = Thread(runnable).apply {
    isDaemon = true
    start()
}
```