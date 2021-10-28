---
title: Creating a Pi4J Context
weight: 70
---

The context is an immutable runtime object that holds the configured state and manages the lifecycle of a Pi4J instance. 
It includes all loaded plugins, providers, platforms, I/O instance registry, environmental configuration and runtime 
objects including executor thread pools,  I/O event listeners, etc.   

Terminating/destroying the context stops and releases all resources, threads, listeners, and provisioned I/O instances 
held by the context. 

Version 1 was implemented using a static singleton, while **version 2 uses a "Context" to avoid static singletons**. 

## Creating a Context

A Pi4J Context can be created automatically (accepting all default context configurations) or manually (builder) 
allowing users to customize the context configuration.

### Automatic
An auto context includes AUTO-DETECT BINDINGS enabled which will load all detected Pi4J extension libraries 
(Platforms and Providers) in the class path.

``` java
var pi4j = Pi4J.newAutoContext();
```

### Builder
If you need more flexibility are specific use-cases, the builder can be used to define all the parameters of the 
context, for example when you want to use your own providers, use mocked instances for testing...:

``` java
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

## More information

### Use a single Context instance

A **single `Context` instance must be created in your application and shared between the classes**. A `Context` object contains 
all the runtime and management state of the I/O. If you would use multiple `Context` objects and attempt to reuse certain 
I/O hardware or I/O providers it's possible that they could conflict or get out of sync. 

### Get GPIO handlers from the Context

The `Context` maintains a reference to each I/O instance created, until `pi4j.shutdown()` is called.

Somewhere you will need to `create()` your I/O instance giving it a unique ID (String). If you try to call `create()` 
a second time with the same ID, you will get an `IOAlreadyExistsException`.

``` java
pi4j.digitalOutput().create(1, "my-gpio");
```

Elsewhere in your application, you can get access to existing I/O instances using the Context's `io()` or `getIO()` methods.

``` java
if (pi4j.hasIO("my-gpio")) {  
    DigitalOutput myOutput = pi4j.io("my-gpio");
}
```

Additional methods to access the registered I/O instances can be obtained through the `Registry` class.

``` java
pi4j.registry().*
```
