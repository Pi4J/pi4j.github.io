---
title: LEDButton
weight: 208
tags: ["Buzzer"]
---
### Description
The [Buzzer](https://github.com/Pi4J/pi4j-example-components/tree/Dev-Arcade/src/main/java/com/pi4j/example/components) (src/main/java/com/pi4j/example/components) is a template class, that you can use in your own Java-project.
You can take any Buzzer you find. Like for example this one: [Buzzer](https://www.berrybase.de/sensoren-module/audio-schall/ky-012-aktives-buzzer-modul)
The Template Class gives you the option to play a note, and to create own little melodies to play. It's all controlled over a Frequency on the PWM.

### Layout
![Buzzer Layout](/assets/documentation/device-examples/Layout-Buzzer.png)

### Code
A simple example on how to use the Buzzer-Class from the [Hardware-Catalog](https://github.com/Pi4J/pi4j-example-components) :
```
//initialising the buzzer
Buzzer buzzer = new Buzzer(pi4j, PIN.PWM18);

//playing a simple note
buzzer.playTone(Buzzer.Note.B6.getFrequency(), 1000);

//shutting it down for 1 second
buzzer.playSilence(1000);

//Piano baseline of Seven Nation Army by the white Stripes
Buzzer.Sound[] melody = new Buzzer.Sound[]{
		new Buzzer.Sound(Buzzer.Note.E1, 11),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 1),
		new Buzzer.Sound(Buzzer.Note.E1, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 2),
		new Buzzer.Sound(Buzzer.Note.G1, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 3),
		new Buzzer.Sound(Buzzer.Note.E1, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 4),
		new Buzzer.Sound(Buzzer.Note.D1, 2),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 3),
		new Buzzer.Sound(Buzzer.Note.C1, 16),
		new Buzzer.Sound(Buzzer.Note.B0, 8),
		new Buzzer.Sound(Buzzer.Note.PAUSE, 8),
};

//playing the melody once, then shutting down for a second
buzzer.playMelody(1, melody);
buzzer.playSilence(1000);

//playing the melody 5 times repeatedly
buzzer.playMelody(1, 5, melody);
```

### Further application
The class is implemented in the two sample projects [Theremin](https://github.com/DieterHolz/RaspPiTheremin) and [Potobooth](https://github.com/DieterHolz/PhotoBooth).

### Further projetct ideas
- An application, which sounds if you walk by, like an alarm.
- An application, where you use many of them to create a beautiful sounding melody.
