---
title: Pi4J Kotlin DSL
description: "Pi4J Kotlin DSL & API Example & Documentation"
weight: 45
---

Pi4J-Kotlin (aka Pi4K) is an implementation on top of Pi4J to facilitate the development of Kotlin applications for the Raspberry Pi that can interact with the GPIOs.

Kotlin makes extensive use of Domain Specific Language (DSL) to provide APIs that are cleaner, easier to read, and more structured. The DSLs provided here on top of Pi4J make it very easy to use this library in a Kotlin application. These Kotlin DSLs don't introduce added runtime overhead of a new layer when used. DSL builders are always inlined on Compile-Time.

### Installation
Install the Pi4J dependency and `pi4j-ktx` in your app's `build.gradle.ktx` file:
``` kotlin
dependencies {
    implementation("com.pi4j:pi4j-ktx:2.4.0") // Kotlin DSL
    implementation("com.pi4j:pi4j-core:2.3.0")
    implementation("com.pi4j:pi4j-plugin-raspberrypi:2.3.0")
    implementation("com.pi4j:pi4j-plugin-pigpio:2.3.0")
}
```

If you want to use the [Console DSL](kotlin-api-docs/#console) to [log with SLF4J](/documentation/logging/), add the dependency:

``` kotlin
implementation("org.slf4j:slf4j-api:1.7.32")
implementation("org.slf4j:slf4j-simple:1.7.32")
```

### GitHub projects:

* Kotlin Interface & DSL for Pi4J V2: [Pi4J-Kotlin](https://github.com/Pi4J/pi4j-kotlin)  
* For Pi4J V1 Kotlin Bindings, check [Pi4K](https://github.com/mhashim6/Pi4K)