---
title: 'Dependency injection'
taxonomy:
    category:
        - docs
visible: false
---

Along with the annotated I/O configuration the ability to support I/O provisioning via dependency injection also makes a lot of sense. There is some basic brute-force stuff working but this needs more work to make this a compatible implementation for Spring or CDI. 

```
@Inject
private Context pi4j;

// register a digital input listener to listen for any value changes on the digital input pin
@Register(DIGITAL_INPUT_PIN_ID)
private DigitalStateChangeListener changeListener = event -> System.out.println(" (LISTENER #1) :: " + event);

// setup a digital input event listener to listen for any value changes on the digital input
// using a custom method with a single event parameter
@OnEvent(DIGITAL_INPUT_PIN_ID)
private void onDigitalInputChange(DigitalStateChangeEvent event){
    System.out.println(" (LISTENER #2) :: " + event);
}
```