---
title: I²C Kotlin DSL
description: "I²C DSL Pi4J-Kotlin"
weight: 49
---

{{% notice info %}}
Feel free to checkout the [Pi4J docs on I²C](/documentation/io-examples/i2c/)
{{% /notice %}}

## Installation

Add LinuxFs dependency
```kotlin
dependencies {
    implementation("com.pi4j:pi4j-plugin-linuxfs:2.2.1")
}
```

## I²C DSL

```kotlin
i2c(1, 0x3f) {
    id("TCA9534")
    linuxFsI2CProvider()
}.use { tca9534Dev ->
  // use here. Will auto close
}
```

## Writing
```kotlin

i2c(1, 0x3f) {
    id("TCA9534")
    linuxFsI2CProvider()
}.use { tca9534Dev ->
  val newState = tca9534Dev.setPin(currentState, pin = 8, TCA9534_REG_ADDR_OUT_PORT)
}
```

## Minimal I²C Example

{{% notice info %}}
This is the Kotlin DSL version of the same [I²C example here](/documentation/io-examples/i2c#code-example), but leveraging the Kotlin DSL
{{% /notice %}}

```kotlin
private const val TCA9534_REG_ADDR_OUT_PORT: Int = 0x01
private const val TCA9534_REG_ADDR_CFG: Int = 0x03

fun main() {
    pi4j {
        i2c(1, 0x3f) {
            id("TCA9534")
            linuxFsI2CProvider()
        }.use { tca9534Dev ->
            val config = tca9534Dev.readRegister(TCA9534_REG_ADDR_CFG)
            check(config >= 0) {
                "Failed to read configuration from address 0x${"%02x".format(TCA9534_REG_ADDR_CFG)}"
            }

            var currentState = tca9534Dev.readRegister(TCA9534_REG_ADDR_OUT_PORT)
            if (config != 0x00) {
                println(
                    "TCA9534 is not configured as OUTPUT, setting register 0x${"%02x".format(TCA9534_REG_ADDR_CFG)} to 0x00"
                )
                currentState = 0x00
                tca9534Dev.writeRegister(TCA9534_REG_ADDR_OUT_PORT, currentState)
                tca9534Dev.writeRegister(TCA9534_REG_ADDR_CFG, 0x00)
            }

            tca9534Dev.run {
                // bit 8, is pin 1 on the board itself, so set pins in reverse:
                console {
                    currentState = setPin(currentState, 8, TCA9534_REG_ADDR_OUT_PORT)
                    +"Setting TCA9534 to new state  ${currentState.binStr()}"
                    sleep(500L)
                    currentState = setPin(currentState, 8, TCA9534_REG_ADDR_OUT_PORT, false)
                    +"Setting TCA9534 to new state  ${currentState.binStr()}"
                    sleep(500L)
                    currentState = setPin(currentState, 7, TCA9534_REG_ADDR_OUT_PORT)
                    +"Setting TCA9534 to new state  ${currentState.binStr()}"
                    sleep(500L)
                    currentState = setPin(currentState, 7, TCA9534_REG_ADDR_OUT_PORT, false)
                    +"Setting TCA9534 to new state  ${currentState.binStr()}"
                    sleep(500L)
                }
            }
        }
    }
}
```
