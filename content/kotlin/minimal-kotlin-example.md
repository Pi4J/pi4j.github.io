---
title: Minimal Kotlin Pi4J example
description: "Pi4J Kotlin DSL & API Example"
weight: 46
---

{{% notice info %}}
Full Example on GitHub: [https://github.com/Pi4J/pi4j-kotlin/blob/master/example/src/main/kotlin/MinimalExample.kt](https://github.com/Pi4J/pi4j-kotlin/blob/master/example/src/main/kotlin/MinimalExample.kt)
{{% /notice %}}

{{% notice tip %}}
For full documentation, visit the [Kotlin Docs](https://pi4j.com/kotlin/kotlin-api-docs/)
{{% /notice %}}

This is a minimal working example, make sure to check it out from the link above for the full introduction and comments.

It does exactly the same functionality of the Minimal Example [using the Java API](/getting-started/minimal-example-application/):

> The application will toggle an LED on/off and each time you press the button, the toggling speed increases. When you have pushed the button 5 times, the application stops.

{{< vimeo 525570174 >}}

## Wiring

This minimal example application uses this wiring:

![Wiring of a LED and button for the minimal example application](/assets/getting-started/minimal/led-button_bb.png)

## Code


```kotlin
const val PIN_BUTTON = 24 // PIN 18 = BCM 24
const val PIN_LED = 22 // PIN 15 = BCM 22
var pressCount = 0

console {
  title("<-- The Pi4J Project -->", "Minimal Example project")
  pi4j {
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
    }
    
    digitalOutput(PIN_LED) {
        id("led")
        name("LED Flasher")
        shutdown(DigitalState.LOW)
        initial(DigitalState.LOW)
        piGpioProvider()
      }.run {
        while (pressCount < 5) {
          if (isHigh) {
            +"LED low"
            low()
          } else {
            +"LED high"
            high()
          }
          Thread.sleep((500L / (pressCount + 1)))
        }
      }
    }
  }
}
```

## Building & Running the application

You can simply run the example app using gradle on the target device (Raspberry Pi for example):
``` shell
./gradlew :example:run
```