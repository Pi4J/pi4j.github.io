---
title: Building an I/O Instance
weight: 100
---

A GPIO can be configured like in the following example:

```java
var ledConfig = DigitalOutput.newConfigBuilder(pi4j)
    .id("my-dout")
    .name("My Digital Output")
    .address(GPIO_PIN)
    .shutdown(DigitalState.LOW)
    .initial(DigitalState.HIGH)
    .provider("linuxfs-digital-output");
```

## id

The `id` field is used internally inside the Pi4J context/runtime to keep track of the instances. 
If you don't assign an `id`, Pi4J will create a unique ID string for the instance -- so its optional and only needed 
if you want to specify your own unique ID string. 

Additionally, you can retrieve the I/O instance from the Pi4J context anywhere else in your program if needed by the id. 
This can help in some cases where you only need to pass around the single Pi4J context, and you can still gain access to 
the I/O instances without having to track and pass around your own variable references. So even if your variable reference 
to an I/O instance goes out of scope, Pi4J will maintain a reference to the I/O instance internally until it is `shutdown()`.

```java
// Three ways to get existing LED output instance
DigitalOutput led = pi4j.io("my-led");
var led = (DigitalOutput)pi4j.io("my-led");
var led = pi4j.io("my-led", DigitalOutput.class);
```

Internally the I/O instances are maintained by the Registry. You can gain access to the Registry via the context. There 
are additional methods in registry to interrogate/discover/enumerate the created I/O instances at runtime.

```java
// Get the Pi4J I/O registry
Registry registry = pi4j.registry();

// Check to see if the LED output already exists (by id)
boolean myLedAlreadyExists = registry.exists("my-led");

// Get all digital output instances from the Pi4J I/O registry       
var outputs = registry.allByIoType(IOType.DIGITAL_OUTPUT);
```

## name and description

Fields like `name` and `description` are entirely optional and not used by Pi4J internally except to print if performing 
a `describe()` or `toString()` operation on Pi4J objects.

```java
// Create digital output I/O configuration
var config = DigitalOutput.newConfigBuilder(pi4j)
    .id("my-dout")
    .name("My Digital Output")
    .address(GPIO_PIN)
    .shutdown(DigitalState.LOW)
    .initial(DigitalState.HIGH)
    .provider("linuxfs-digital-output");

// Create digital output I/O instance using configuration
var output = pi4j.create(config);

// Print digital output object to system out
output.describe().print(System.out);

----

// ... CONSOLE OUTPUT
// > IO: "My Digital Output" {my-dout} <com.pi4j.plugin.linuxfs.provider.gpio.digital.LinuxFsDigitalOutput> {DOUT-26} 
```