---
title: Building an I/O Instance
weight: 100
---

A GPIO can be configured with Pi4J in different ways, either short for default behavior, a bit longer with additional settings, or with a full custom configuration using a building pattern.

## I/O Initialization Examples

Before we can initialize an I/0, the Pi4J context must be initialized. The `Pi4J` static class includes a few helper context creators for the most common use cases.  The `newAutoContext()` method will automatically load all available Pi4J extensions found in the application's classpath which may include `Platforms` and `I/O Providers`.

```java
var pi4j = Pi4J.newAutoContext();
```

### DigitalInput

Here are a few examples of the different possibilities to initialize a digital input object:

```java
// Shortest way
var button = pi4j.din().create(INTEGER_PIN_ADDRESS);

// Is equal to
var button = pi4j.digitalInput().create(INTEGER_PIN_ADDRESS);

// The create method can be called with more parameters
var button = pi4j.din().create(INTEGER_PIN_ADDRESS, STRING_ID);
var button = pi4j.din().create(INTEGER_PIN_ADDRESS, STRING_ID, STRING_NAME);
var button = pi4j.din().create(INTEGER_PIN_ADDRESS, STRING_ID, STRING_NAME, STRING_DESCRIPTION);

// Or you can use a configuration builder
var buttonConfig = DigitalInput.newConfigBuilder(pi4j)
        .id("button")
        .name("Press button")
        .address(PIN_BUTTON)
        .pull(PullResistance.PULL_DOWN)
        .debounce(3000L);
var button = pi4j.create(buttonConfig);
``` 

### DigitalOutput

The examples above are also applicable for an output:

```java
// Shortest way
var led = pi4j.dout().create(INTEGER_PIN_ADDRESS);

// Is equal to
var led = pi4j.digitalOutput().create(INTEGER_PIN_ADDRESS);

// The create method can be called with more parameters, see above

// Or you can use a configuration builder
var ledConfig = DigitalOutput.newConfigBuilder(pi4j)
        .id("my-dout")
        .name("My LED")
        .address(PIN_LED)
        .shutdown(DigitalState.LOW)
        .initial(DigitalState.HIGH);
var led = pi4j.create(ledConfig);
``` 

### PWM, SPI, I2C, Serial

The same methodology is available for other types of I/O's:

```java
// Shortest way
var pwm = pi4j.pwm().create(INTEGER_PIN_ADDRESS);
var spi = pi4.spi().create(STRING_ID);
var i2c = pi4j.i2c().create(INTEGER_BUS, INTEGER_DEVICE);
var serial = pi4j.serial().create(STRING_ID);

// Or using the config builder, for example, I2C:
var i2cConfig = I2C.newConfigBuilder(pi4j)
        .id("my-i2c")
        .bus(I2C_BUS)
        .device(I2C_ADDRESS)
        .build();
var i2c = pi4j.i2c().create(i2cConfig);
```

## newConfigBuilder parameters

### id

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
var led = (DigitalOutput) pi4j.io("my-led");
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

### name and description

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

## Reuse the config 

The config object can be reused to create multiple GPIOs by overriding the `address` (and `id` if used) for each I/O instance:

```java
var config = DigitalOutput.newConfigBuilder(pi4j)
        .provider("linuxfs-digital-output")
        .shutdown(DigitalState.LOW)
        .initial(DigitalState.LOW);

var pin0 = pi4j.create(config.address(0).id("my-led"));
var pin1 = pi4j.create(config.address(1).id("my-relay"));
var pin2 = pi4j.create(config.address(2).id("my-lock"));
var pin3 = pi4j.create(config.address(3).id("my-pump"));
```
