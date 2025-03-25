---
title: Shutdown (cleanup)
weight: 150
---

Pi4J has a `shutdown` method that can be used for two different purposes.

## End Of Application

At the end of our application, the context needs to be shutdown to release the I/O and clean up the used resources.

```java
# Start of program
var pi4j = Pi4J.newAutoContext();

# YOUR CODE GOES HERE

# End of program
pi4j.shutdown();
```

## Reuse of a GPIO

When you want to reuse a GPIO, it must be shutdown to clean it up. This can be done by shutting down the GPIO itself and providing the `ID` to the `shutdown` method. As an example, check [this unit test](https://github.com/Pi4J/pi4j/blob/develop/pi4j-test/src/test/java/com/pi4j/test/registry/RegistryTest.java#L77):

```java
@Test
public void testShutdownAndRecreate() throws Pi4JException {
    var inputConfig = DigitalInput.newConfigBuilder(pi4j)
            .id("DIN-3")
            .name("DIN-3")
            .address(3);

    // create a new input, then shutdown
    var input = pi4j.create(inputConfig);

    input.shutdown(pi4j);
    pi4j.shutdown(input.id());

    // shouldn't fail when recreating
    input = pi4j.create(inputConfig);

    // or shutting down
    pi4j.shutdown(input.id());
}
```

    