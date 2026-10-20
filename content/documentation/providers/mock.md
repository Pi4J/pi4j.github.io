---
title: Mock Provider
weight: 92
tags: ["Mock"]
---

The Mock plugin provides fake I/O implementations for every I/O type supported by Pi4J. It's used by Pi4J's own unit and integration tests, and it's useful in your own application when you want to write and run tests without real hardware attached, or when developing on a machine that isn't a Raspberry Pi (or other SBC).

Providers in the Mock plugin:

* mock-digital-input
* mock-digital-output
* mock-i2c
* mock-spi
* mock-pwm

## Dependencies

To use the Mock provider include the following dependency:

``` xml
<dependency>
    <groupId>com.pi4j</groupId>
    <artifactId>pi4j-plugin-mock</artifactId>
    <version>${pi4j.version}</version>
</dependency>
```

## Loading the Mock Providers

Mock providers are **not** loaded by `Pi4J.newAutoContext()` when running on a Raspberry Pi, so a real deployment never accidentally picks up fake I/O. On any other machine (for example your development laptop), `newAutoContext()` auto-detects and loads the Mock providers, since there's no real hardware to talk to.

To explicitly request the Mock providers regardless of the board you're running on, build the Context with `autoDetectMockPlugins()`:

```java
Context pi4j = Pi4J.newContextBuilder()
    .autoDetectMockPlugins()
    .autoDetectPlatforms()
    .build();
```

See [Creating a Pi4J Context](/documentation/create-context/) for more details and alternative ways to create a Context with specific providers.
