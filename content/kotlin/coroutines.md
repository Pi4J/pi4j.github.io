---
title: Coroutines Support
description: "Coroutines for Pi4J 
-Kotlin"
weight: 48
---

## pi4jAsync

Same with the `pi4j` DSL, you can create a pi4j block to execute within a `CoroutineScope` using the `pi4jAsync` DSL.

```kotlin
pi4jAsync {
    delay(100) // suspended call
    describe()
}
```
Inside `pi4jAsync` you have access to a newly created auto context and you can run your code in the provided `CoroutineScope`.

## Custom CoroutineScope
You can also use a custom `CoroutineScope` instance.
```kotlin
pi4jAsync(CoroutineScope(Dispatchers.Default)) {
    delay(100) // suspended call
    describe()
}
```

## Minimal Example with Coroutines
{{% notice info %}}
This is a the same as the [minimal example](/kotlin/minimal-kotlin-example/), but leveraging Kotlin's Coroutines
{{% /notice %}}

``` kotlin
private const val PIN_BUTTON = 24 // PIN 18 = BCM 24
private const val PIN_LED = 22 // PIN 15 = BCM 22
private var pressCount = 0

pi4jAsync {
    console {
        digitalInput(PIN_BUTTON) {
            id("button")
            name("Press button")
            pull(PullResistance.PULL_DOWN)
            debounce(3000L)
            piGpioProvider()
        }.onLow {
            pressCount++
            +"Button was pressed for the ${pressCount}th time"
        }

        digitalOutput(PIN_LED) {
            id("led")
            name("LED Flasher")
            shutdown(DigitalState.LOW)
            initial(DigitalState.LOW)
            piGpioProvider()
        }.run {
            while (pressCount < 5) {
                +"LED ${state()}"
                toggle()
                delay(500L / (pressCount + 1))
            }
        }
    }
}
```
