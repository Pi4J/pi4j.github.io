---
title: I/O Registry
weight: 140
---

An additional V2+ feature is an I/O registry where all I/O instances that have been created can be maintained, managed, re-accessed, etc. As the library keeps track of all the created I/O instances, they become publicly accessible through a registry where users can interrogate, iterate, identify and access all created I/O instances that Pi4J is managing.

This is very useful for add-ons/plugins that want to provide runtime information about the state of all I/O, for example a web app illustrating the current state of I/O. 

The registry is responsible for managing I/O instance lifecycles and provides a means for your program to easily access any I/O instance using its unique identifier.