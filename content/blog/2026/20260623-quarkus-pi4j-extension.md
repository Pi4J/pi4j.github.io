---
title: "Quarkus Pi4J Extension"
date: 2026-06-23
tags: ["Quarkus"]
---

2026-06-23 by Igor De Souza

## Bringing Raspberry Pi Development to Quarkus with the Quarkus Pi4J Extension

Java developers building applications for Raspberry Pi often face a common challenge: combining hardware access with modern application frameworks.

The [Quarkus Pi4J extension](https://foojay.io/today/bringing-raspberry-pi-development-to-quarkus-with-the-quarkus-pi4j-extension/) connects two complementary technologies: [Pi4J](https://www.pi4j.com/) for hardware access on the Raspberry Pi, and [Quarkus](https://quarkus.io/) as a modern, cloud-native Java framework. Together they make it easier to build production-ready IoT and edge computing applications with clean, maintainable hardware control.

### What the extension does

The extension automatically configures and manages the Pi4J `Context`, the core component responsible for hardware access and device lifecycle. Instead of setting this up by hand, developers inject it through CDI (Contexts and Dependency Injection), which removes a lot of boilerplate and lets you focus on your application logic.

### Key features

- **Automatic initialization:** Quarkus takes care of creating and managing the Pi4J `Context`.
- **Externalized configuration:** GPIO mappings can be defined through application properties, so you can change pin assignments without recompiling.
- **Annotation-based injection:** Reference GPIO pins by address or by a logical name.
- **Health monitoring:** Integration with Quarkus Health for operational visibility.
- **Lifecycle management:** Automatic initialization and graceful shutdown.
- **REST API integration:** Combine hardware control with web services.

### A small example

Injecting the Pi4J `Context` and controlling an LED becomes as simple as:

```java
@ApplicationScoped
public class LedService {
    @Inject
    Context pi4j;

    public void turnOnLed() {
        var led = pi4j.digitalOutput().create(22);
        led.high();
    }
}
```

### Why it matters

By bringing Pi4J into the Quarkus ecosystem, the extension makes Raspberry Pi development much more approachable for enterprise Java developers. It enables sophisticated IoT solutions such as smart homes, monitoring systems, and robotics, while keeping modern development practices and deployment flexibility across multiple devices with different hardware configurations.

Read the full article on Foojay: [Bringing Raspberry Pi Development to Quarkus with the Quarkus Pi4J Extension](https://foojay.io/today/bringing-raspberry-pi-development-to-quarkus-with-the-quarkus-pi4j-extension/) by Igor De Souza.
