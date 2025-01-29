---
title: 'What''s New in V.3'
weight: 22
---

Versions 3.0.0 is based on 2.8.0 (released in January 2025), but bumps the **Java version to 21** or newer! We [asked our users](https://github.com/Pi4J/pi4j/discussions/409) which minimal Java version we should use, but there was no one clear answer, as expected ;-)

The current, latest, Long Term Support (LTS) version of Java is version 21. So it makes sense to jump forward from 11 to 21. This will also prepare us for a the next LTS, which will be 25 in September 2025. Bumping to the latest LTS makes it possible to make use of many newer Java language and runtime improvements, simplify some of the code, etc.

We would like to move to Java 22 as this would allow us to easier call C code to interact with the GPIOs, thanks to [JEP 454: Foreign Function & Memory API](https://openjdk.org/jeps/454). Unfortanelty, 22 is not a LTS, so it would force us to bump the version every six months with each new release, up till 25.

[The sources of V3 can be found in the GitHub repository `pi4j/pi4j`](https://github.com/Pi4J/pi4j).

## What's New in 3.0?

Pi4J version 3.0.0 is a continuation of 2.8.0, but bumps the minimal Java version to 21.

## Sources

The Pi4J V.3 source code is available in this GitHub repository: [`pi4j/pi4j` GitHub Repository](https://github.com/Pi4J/pi4j)

```shell
git clone https://github.com/Pi4J/pi4j
```

Pi4J V.3 is not yet released, but can already use version `3.0.0-SNAPSHOT` for testing if you add the snapshot Maven repository to your pom-file.

```xml
<repositories>
    <repository>
        <id>oss-snapshots-repo</id>
        <name>Sonatype OSS Maven Repository</name>
        <url>https://oss.sonatype.org/content/groups/public</url>
        <releases>
            <enabled>false</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </repository>
</repositories>
```