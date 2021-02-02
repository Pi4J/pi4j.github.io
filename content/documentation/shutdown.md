---
title: Shutting down the Pi4J Context
weight: 150
---

At the end of our application, the context needs to be shutdown to release the I/O and clean up the used resources.

```
# Start of program
var pi4j = Pi4J.newAutoContext();

# YOUR CODE GOES HERE

# End of program
pi4j.shutdown();
```