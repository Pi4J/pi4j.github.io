---
title: Buzzer
weight: 210
tags: ["Buzzer"]
---
### Description
The [Buzzer](https://github.com/Pi4J/pi4j-example-components/tree/main/src/main/java/com/pi4j/catalog) (src/main/java/com/pi4j/catalog) is a template class, that you can use in your own Java-project.

The Template Class gives you the option to play a note, and to create your own little melodies to play. The buzzer is controlled via a PWM output. The dutycycle is fixed at 50% and with the frequency the desired sound can be reproduced.

### Layout
![Buzzer Layout](/assets/documentation/device-examples/components/Layout-Buzzer.png)

{{< gallery >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/BuzzerActiveBreadboard.png" caption="Buzzer Acitve Breadboard" caption-position="center" caption-effect="fade" >}}
{{< figure link="/assets/documentation/device-examples/components/pictures/BuzzerActive.png" caption="Buzzer Active" caption-position="center" caption-effect="fade" >}}
{{< /gallery >}}
{{< load-photoswipe >}}

### Code
A simple example on how to use the Buzzer-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```java
//initialising the buzzer
Buzzer buzzer = new Buzzer(pi4j, PIN.PWM18);

//playing a simple note
System.out.println("playing note b6 for 1 sec");
buzzer.playTone(Buzzer.Note.B6.getFrequency(), 1000);

//shutting it down for 1 second
buzzer.playSilence(1000);

//Piano baseline of Seven Nation Army by the white Stripes
Buzzer.Sound[] melody = new Buzzer.Sound[]{
		new Buzzer.Sound(Buzzer.Note.E7, 11),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 1),
		new Buzzer.Sound(Buzzer.Note.E7, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 2),
		new Buzzer.Sound(Buzzer.Note.G6, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 3),
		new Buzzer.Sound(Buzzer.Note.E7, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 4),
		new Buzzer.Sound(Buzzer.Note.D6, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 3),
		new Buzzer.Sound(Buzzer.Note.C7, 16),
		new Buzzer.Sound(Buzzer.Note.B5, 8),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 8),
};

//playing the melody once, then shutting down for a second
System.out.println("playing melody once");
buzzer.playMelody(60, melody);
delay(1000);

//playing the melody 5 times repeatedly
System.out.println("playing melody 5 times");
System.out.println("playing in a different thread, so the app is moving on");
buzzer.playMelody(60, 5, melody);
System.out.println("waiting for melody to finish");
delay(3000);
```

### Further application
The class is implemented in the sample project [Theremin](https://github.com/DieterHolz/RaspPiTheremin).

### Further project ideas
- An application, which triggers if you walk by and starts beeping, like an alarm.
- An application, where you use many of them to create a beautiful sounding melody.
