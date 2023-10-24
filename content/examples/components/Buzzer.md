---
title: Buzzer
weight: 210
tags: ["Buzzer"]
---

### Description

The [Buzzer](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog/components/Buzzer.java) is a template class, that you can use in your own Java-project.

The Template Class gives you the option to play a note, and to create your own little melodies to play. The buzzer is controlled via a PWM output. The dutycycle is fixed at 50% and with the frequency the desired sound can be reproduced.

### Layout

![Buzzer Layout](/assets/examples/components/components/Layout-Buzzer.png)

{{< gallery >}}
{{< figure link="/assets/examples/components/components/pictures/BuzzerActiveBreadboard.png" caption="Buzzer Acitve Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/examples/components/components/pictures/BuzzerActive.png" caption="Buzzer Active" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code

A simple example on how to use the Buzzer-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components):

```java
public class Buzzer_App implements Application {

    //this is how you compose a simple melody
    //Piano baseline of Seven Nation Army by the white Stripes
    private final List<Buzzer.Sound> melody = List.of(
            new Buzzer.Sound(E7   , 11),
            new Buzzer.Sound(PAUSE, 1),
            new Buzzer.Sound(E7   , 2),
            new Buzzer.Sound(PAUSE, 2),
            new Buzzer.Sound(G6   , 2),
            new Buzzer.Sound(PAUSE, 3),
            new Buzzer.Sound(E7   , 2),
            new Buzzer.Sound(PAUSE, 4),
            new Buzzer.Sound(D6   , 2),
            new Buzzer.Sound(PAUSE, 3),
            new Buzzer.Sound(C7   , 16),
            new Buzzer.Sound(B5   , 8),
            new Buzzer.Sound(PAUSE, 8)
    );

    private final List<Buzzer.Sound> imperialMarch = List.of(
            new Buzzer.Sound(G4,  8),
            new Buzzer.Sound(G4,  8),
            new Buzzer.Sound(G4,  8),
            new Buzzer.Sound(DS4, 6),
            new Buzzer.Sound(AS4, 2),
            new Buzzer.Sound(G4,  8),
            new Buzzer.Sound(DS4, 6),
            new Buzzer.Sound(AS4, 2),
            new Buzzer.Sound(G4, 16));

    @Override
    public void execute(Context pi4j) {
        System.out.println("Buzzer demo started");

        //initialising the buzzer
        Buzzer buzzer = new Buzzer(pi4j, PIN.PWM13);

        //playing a simple tone
        System.out.println("playing note b6 for 1 sec");
        buzzer.playTone(1976, Duration.ofSeconds(1));

        //relax for 1 second
        buzzer.silence(Duration.ofSeconds(1));

        System.out.println("start playing melody");
        buzzer.playMelody(60, melody);

        delay(Duration.ofSeconds(3));

        //first melody is stopped and second is played
        buzzer.playMelody(103, imperialMarch);

        buzzer.awaitEndOfMelody();
        System.out.println("Second melody has finished");

        buzzer.reset();

        System.out.println("buzzer demo finished");
    }
}
```

### Further application

The class is implemented in the sample project [Theremin](https://github.com/DieterHolz/RaspPiTheremin).

### Further project ideas

- An application, which triggers if you walk by and starts beeping, like an alarm.
- An application, where you use many of them to create a beautiful sounding melody.
