---
title: JavaFX GUI and MVC template
weight: 90
tags: ["Digital Input", "Digital Output", "JavaFX"]
---

{{% notice note %}}
GITHUB PROJECT: [https://github.com/Pi4J/pi4j-template-javafx](https://github.com/Pi4J/pi4j-template-javafx)
{{% /notice %}}

The FHNW University created a template project which is now part of the Pi4J example repositories.

The goal of this project is to:

* Provide a clear step-by-step how to prepare your Raspberry Pi
* Provide multiple test and start applications
* Explain the use of a MVC-model (Model-View-Controller) to clearly split data, actions and user interface
* Explain the use of JUnit test


# Example applications

## HelloFX

A simple application to test if the JavaFX libraries are installed correctly. 
Should not be used as a template for one's own JavaFX applications.

## Wiring

The two other example applications use an LED and a button. 
These must be wired as is shown in the following diagram:

![Wiring](https://github.com/Pi4J/pi4j-template-javafx/raw/master/assets/led-button_bb.png)

## MinimalPi4J

The MinimalPi4j application is a Pi4j only application without a GUI. 
This application is also only used to test the setup and can be deleted after testing.

Pressing the button should generate a message in the console.

Once the Pi4J setup has been tested, MinimalPi4J can be deleted.

### TemplateApp

This application shows the interaction between a JavaFX based Graphical User Interface (GUI) and the Raspberry Pi 
connected sensors and actuators, the Physical User Interface (PUI).

This application is to be used as a template for one's own applications. This includes the existing test cases.

![GUI application started from IntelliJ IDEA](/assets/getting-started/template-javafx-mvc/running-gui.png)

You should first get to know and understand the example. For your own applications you should then copy the the `TemplateApp` 
and modify it for your project, however without violating the rules of the MVC concept.

### TemplatePUIApp

The MVC concept should also be used for applications without a GUI.

When developing PUI only applications, or when adding the GUI later, then one should use the `TemplatePUIApp` as template.

## The MVC concept

The classic Model-View-Controller concept contains in addition to the starter class at least 3 more classes. The interaction is clearly defined:

![Model-View-Controller concept](https://github.com/Pi4J/pi4j-template-javafx/raw/master/assets/mvc-concept.png)

- _Model classes_
    - contain the complete state which is to be visualized, thus these classes are called _Presentation-Model_
    - are completely separate to the Controller and View classes, i.e. they may not interact with those classes

- _Controller classes_
    - define the entire functionality, i.e. the so-called actions, in the form of methods
    - manage the model classes by definition of the business logic
    - have no access to the view classes

- _View classes_
    - only calls methods on the controller, i.e. triggering actions
    - are notified of the model of state changes
        - observes the state of the model
    - never change the model directly

- _Starter class._
    - Is a subclass of `javafx.application.Application`. Instantiates the three other classes and starts the application.

In our case at least two view classes exist:
- _GUI class._ The Graphical-User-Interface. JavaFX based implementation of the visualisation of the UI on the screen.
- _PUI class._ The Physical-User-Interface. Pi4J based implementation of the sensors and actors. Uses `Component` classes, as is used in  [CrowPi-Example](https://github.com/Pi4J/pi4j-example-crowpi).

GUI and PUI are completely separated from each other, i.e a GUI button to turn an LED on has no direct access to the LED component of the PUI. Instead the GUI button triggers a corresponding action in the controller which then sets the on state property in the model. The PUI listening on this state then turns the actual LED on or off.

GUI and PUI work with the same identical controller and thus also the same identical model.

It is important that one understands this concept and then apply the concepts to one's own project. Should you have questions, contact the Pi4j team.

In the MVC concept, every user interaction traverses the exact same cycle:

![MVC Concept](https://github.com/Pi4J/pi4j-template-javafx/raw/master/assets/mvc-interaction.png)



