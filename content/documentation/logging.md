---
title: Logging with SLF4J
weight: 60
---

Pi4J uses SLF4J for logging. To include it in your project, add this Maven dependency:

```
<dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-simple</artifactId>
        <version>2.0.0-alpha0</version>
</dependency>
```

There are different ways to configure the logging output, as described on [the SLF4J website](http://www.slf4j.org/manual.html), but the shortest is probably with this property in your main-method:

```
 public static void main(String[] args) throws Exception {
        // Configure default lolling level, accept a log level as the first program argument
        System.setProperty("org.slf4j.simpleLogger.defaultLogLevel", "INFO");
        
        // Your code comes here
}
```