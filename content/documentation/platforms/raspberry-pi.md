---
title: 'Raspberry Pi'
---

Pi4J was originally designed for the Raspberry Pi. As of V5, the [FFM provider](/documentation/providers/ffm/) talks to the Linux kernel directly, so Pi4J also runs on other Linux-based SBCs — see [Using Pi4J on other brands](/sbc/using-pi4j-on-other-brands/).

No separate platform plugin is needed for the Raspberry Pi; adding [pi4j-core](/documentation/) and [pi4j-plugin-ffm](/documentation/providers/ffm/) is enough.

## Related to functionality existing in V4, but no longer included in V5

Previous versions of Pi4J required a separate `pi4j-plugin-raspberrypi` dependency (the Raspberry Pi Platform Plugin), which has been removed in V5:

```
    <dependency>
        <groupId>com.pi4j</groupId>
        <artifactId>pi4j-plugin-raspberrypi</artifactId>
        <version>${pi4j.version}</version>
    </dependency>
```
