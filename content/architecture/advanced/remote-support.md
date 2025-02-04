---
title: 'Remote support'
---

One of the big features on the wish-list for V2+: native support for remote I/O capability. Predominantly to support 
the ability for a user to perform development work on their desktop/laptop and be able to run their project with 
remote support slaving the I/O to a daemon running on the Raspberry Pi (or other supported SBC).

{{% notice warning %}}TO BE DECIDED: the V2+ codebase does support this currently by using the PiGpio daemon.  
This may be an OK place to start for the first release, but a separate Pi4J daemon may be ideal for a long term 
solution to capture some of the edge cases and provide remote I/O capability no matter which underlying I/O library 
is being used. {{% /notice %}}