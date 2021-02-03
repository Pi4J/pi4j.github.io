---
title: 'Annotated provisioning'
---

{{% notice warning %}}To simplify the initial V2 version, the DI implementation has be removed so it could be
refactored and extended later. It is still available in the branch
[#22-annotations](https://github.com/Pi4J/pi4j-v2/tree/feature/%2322-annotations){{% /notice %}}

Next to the declarative approach, Java annotations are available for the configuration of I/O provisioning instead 
of the hard-coded approach offered in V1.  

This implementation still needs to be further fine-tuned and unified somehow to make things cleaner and more 
straightforward, but would provide a way to initialize a I/O for instance like this:

```java
@Register(0)
@Address("my.digital.input.pin.zero")
@Name("My Digital Input Pin")
@Debounce(300000) // microseconds
@WithProvider(type=PiGpioDigitalInputProvider.class)
private DigitalInput input;
```