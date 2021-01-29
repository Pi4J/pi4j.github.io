---
title: 'Choosing a Platform'
taxonomy:
    category:
        - docs
visible: true
---

Platforms are extensible service modules responsible for defining a set of default I/O providers and specific hardware capabilities for an embedded hardware system where Pi4J is deployed/running.

Technically speaking ... multiple platforms could be loaded into the runtime context, but only one will be considered the default platform for most I/O provisioning and operations. An example of this could be both a RaspberryPi Platform and Mock Platform are detected as plugins and loaded into the context, but only one will be determined at runtime to be the default platform used by the context.  

_TODO: some priority scheme will need to be implemented and invoked at runtime to resolve which is the best "platform" to accept as the default platform at runtime (on startup). _

The idea here is that a user could have multiple platform plugins in their directory but only one, theoretically the best suited, will be determined and used at runtime based on the runtime environment which makes it possible to develop, run and test on e.g. Windows with the MockPlatform and when finished run on the Raspberry Pi with the same generated jar's which use the RaspberryPiPlatform.  

Current supported platforms:

// TODO subpages