---
title: 'Release Notes'
weight: 40
---

All releases of Pi4J V.2 are listed on [github.com/Pi4J/pi4j-v2/releases](https://github.com/Pi4J/pi4j-v2/releases).

## 2022-08-30 - V2.2.0

What an amazing achievement! No major issues were found in the previous release, but several small fixes were added by more people than ever before in the Pi4J-history. This is a real confirmation of the openness of this project and how a community can work together to further improve a project. 

A big thank you to everyone who experimented with Pi4J, took part in the discussions, filed an issue, created a merge request, added examples,...!

### New example implementations

Thanks to the work of FHNW students and @taartspi, the list of available example implementations has become larger and larger. We even moved them to their own section of this documentation website! Take a look at [Example implementations](/examples/) if you need a quick-start to use a buzzer, camera, LED strip, TCA9548, MCP4725,... or any of the other examples.

### Changes in V2.2.0

Multiple improvements were added in this release (and others are already in progress for the next one!):

* by [@taartspi](https://github.com/taartspi) to improve SPI initialization, see [#229](https://github.com/Pi4J/pi4j-v2/discussions/229)
* by [@haumacher](https://github.com/haumacher) regarding the use of ByteBuffers, see [#185](https://github.com/Pi4J/pi4j-v2/issues/185)
* by [@savageautomate](https://github.com/savageautomate) regarding the polarity of digital output, see [#93](https://github.com/Pi4J/pi4j-v2/issues/93)
* by [@gugrim](https://github.com/gugrim) to ensure positive values are returned from reading unless at end of file, see [#164](https://github.com/Pi4J/pi4j-v2/issues/164)
* by [@eitch](https://github.com/eitch) to also export LinuxFS I2C in module-info.java
* by [@eitch](https://github.com/eitch) to also copy native libs to distribution zip
* by [@hagen](https://github.com/hagen) to be able to configure sample rate and peripheral in PiGpio
* by Saskia Bikle to add an implementation of deregistration/shutdown for IO's
* by [@savageautomate](https://github.com/savageautomate) to add a new value "flags" too SPI implementation

All the differences can be checked by comparing with the previous release 2.1.1 via [this link](https://github.com/Pi4J/pi4j-v2/compare/2.1.1...2.2.0).

## Earlier release notes

Release notes of the previous releases of Pi4J V.2 are available on [github.com/Pi4J/pi4j-v2/releases](https://github.com/Pi4J/pi4j-v2/releases).