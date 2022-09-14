---
title: Minimal Kotlin Pi4J example
weight: 46
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-kotlin/blob/master/example/src/main/kotlin/MinimalExample.kt](https://github.com/Pi4J/pi4j-kotlin/blob/master/example/src/main/kotlin/MinimalExample.kt)
{{% /notice %}}

{{% notice note %}}
For full documentation, visit the [Kotlin Docs](https://pi4j.com/kotlin/kotlin-api-docs/)
{{% /notice %}}

This is a minimal working example, make sure to check it out from the link above for the full introduction and comments. 


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
