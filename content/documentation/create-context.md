---
title: 'Creating a Pi4J Context'
---

The context is an immutable runtime object that holds the configured state and manages the lifecycle of a Pi4J instance. It includes all loaded plugins, providers, platforms, I/O instance registry, environmental configuration and runtime objects including executor thread pools,  I/O event listeners, etc.   

Terminating/destroying the context stops and releases all resources, threads, listeners, and provisioned I/O instances held by the context. 

Version 1 was implemented using a static singleton, while version 2 uses a "Context" to avoid static singletons. 

A Pi4J Context can be created automatically (accepting all default context configurations) or manually (builder) allowing users to customize the context configuration.

# Automatic
An auto context includes AUTO-DETECT BINDINGS enabled which will load all detected Pi4J extension libraries (Platforms and Providers) in the class path.

```
var pi4j = Pi4J.newAutoContext();
```

# Builder
If you need more flexibility are specific use-cases, the builder can be used to define all the parameters of the context, for example when you want to use your own providers, use mocked instances for testing...:

```
Context pi4j = Pi4J.newContextBuilder()
   .add(new MockPlatform())
   .add(MockAnalogInputProvider.newInstance(),
      MockAnalogOutputProvider.newInstance(),
      MockSpiProvider.newInstance(),
      MockPwmProvider.newInstance(),
      MockSerialProvider.newInstance(),
      MockI2CProvider.newInstance(),
      MockDigitalInputProvider.newInstance(),
      MockDigitalOutputProvider.newInstance())
   .add(new MyCustomADCProvider(/* implements AnalogInputProvider, id="my-adc-prov" */))
   .add(new MyCustomSPIProvider(/* implements SpiProvider, id="my-spi-prov" */))
   .build();
```
