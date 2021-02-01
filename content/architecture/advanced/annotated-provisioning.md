---
title: 'Annotated provisioning'
---

Next to the declarative approach, Java annotations are available for the configuration of I/O provisioning instead of the hard-coded approach offered in V1.  

This implementation still needs to be further fine-tuned and unified somehow to make things cleaner and more straightforward, but would provide a way to initialize a I/O for instance like this:

```
@Register(0)
@Address("my.digital.input.pin.zero")
@Name("My Digital Input Pin")
@Debounce(300000) // microseconds
@WithProvider(type=PiGpioDigitalInputProvider.class)
private DigitalInput input;
```