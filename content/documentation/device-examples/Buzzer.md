---
title: Buzzer
weight: 208
tags: ["Buzzer"]
---
### Description
The [Buzzer](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
You can take any Buzzer you find. Like for example this one: [Buzzer](https://www.berrybase.de/sensoren-module/audio-schall/ky-012-aktives-buzzer-modul)
The Template Class gives you the option to play a note, and to create your own little melodies to play. The buzzer is controlled via a PWM output. The dutycycle is fixed at 50% and with the frequency the desired sound can be reproduced.

### Layout
![Buzzer Layout](/assets/documentation/device-examples/Layout-Buzzer.png)

### Code
A simple example on how to use the Buzzer-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
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
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas
- An application, which sounds if you walk by, like an alarm.
- An application, where you use many of them to create a beautiful sounding melody.
