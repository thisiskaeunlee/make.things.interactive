/*
  Arduino Starter Kit example
  Project 13 - Touch Sensor Lamp with Sound
  This sketch is written to accompany Project 13 in the Arduino Starter Kit
  Parts required:
  - 1 megohm resistor
  - metal foil or copper mesh
  - 220 ohm resistor (* for RED LED — will need to be different if using a different coloured LED)
  - LED
  - Speaker
  Software required:
  - BobaBlox library by BobaBlox
    https://github.com/BobaBlox/BobaBlox
  - CapacitiveSensor library by Paul Badger
    http://www.arduino.cc/playground/Main/CapacitiveSensor
  created 18 Sep 2012
  by Scott Fitzgerald
  http://www.arduino.cc/starterKit
  This example code is part of the public domain.
*/


#include <BobaBlox.h>
#include <CapacitiveSensor.h>

// create an instance of the library
// pin 4 sends electrical energy
// pin 3 senses senses a change
CapacitiveSensor capSensor = CapacitiveSensor(4, 3);

// pin the LED is connected to
const int ledPin = 12; 
// pin the speaker is connected to
const int speakerPin = 2;

// threshold for turning the lamp on
int threshold = 1100;

// Flag to detect if the sensor is touched once
bool touchedOnce = false;

void setup() {
// open a serial connection
Serial.begin(9600);
// set the LED pin and speaker pin as outputs
pinMode(ledPin, OUTPUT); 
pinMode(speakerPin, OUTPUT); 
}
// function to play melody
void playmelody() {
// play a tone at 1000 Hz for 100 milliseconds
tone(speakerPin, 1000, 100);
//play the notes and the duration of each note is 125 milliseconds
tone(speakerPin, 262, 125); // the frequency value of C4 is 262HZ
delay(150);
tone(speakerPin, 294, 125); // the frequency value of D4 is 294HZ
delay(150);
tone(speakerPin, 330, 125); // the frequency value of E4 is 330HZ
delay(150);
tone(speakerPin, 349, 125); // the frequency value of F4 is 349HZ
delay(150);
tone(speakerPin, 392, 125); // the frequency value of G4 is 392HZ
delay(150);
tone(speakerPin, 440, 125); // the frequency value of A4 is 440HZ
delay(150);
tone(speakerPin, 494, 125); // the frequency value of B4 is 494HZ
delay(150);
tone(speakerPin, 523, 125); // the frequency value of C4 is 523HZ
delay(500);
}

void loop() {
// store the value reported by the sensor in a variable
long sensorValue = capSensor.capacitiveSensor(30);

// print out the sensor value
Serial.println(sensorValue);

// if the value is greater than the threshold
if (sensorValue > threshold) { // the plant is touched
// turn the LED on
digitalWrite(ledPin, HIGH);

// if the plant is touched once
if (!touchedOnce) {
touchedOnce = true;
playmelody();
} 
// the plant is touched for the second time
else {
touchedOnce = false;
// Play the melody in reverse
tone(speakerPin, 523, 125); // C5
delay(150);
tone(speakerPin, 494, 125); // B4
delay(150);
tone(speakerPin, 440, 125); // A4
delay(150);
tone(speakerPin, 392, 125); // G4
delay(150);
tone(speakerPin, 349, 125); // F4
delay(150);
tone(speakerPin, 330, 125); // E4
delay(150);
tone(speakerPin, 294, 125); // D4
delay(150);
tone(speakerPin, 262, 125); // C4
delay(500);
}
} else {
// turn the LED off and stop the melody
digitalWrite(ledPin, LOW);
noTone(speakerPin);
}
delay(10);
}
