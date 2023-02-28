# Midterm Project

**Aim:** Create interactive work utilizing Sxxds (Glass objects). My aim is to utilize an input of weight to generate an output of sound.

## Sketch

**Goal 1:** Get bone transducer conductor to work.

![Image](image1.png)

Getting bone transducer conductor to work was a success but lm833n amplifier chip isn’t strong enough. Also realized putting together a functional circuit on breadboard proved not to be the best for functionality.

My next step is to order preassembled circuit with an amplifier chip with more wattage than lm833n then do setup to ensure functional.

![Image](image2.png)

Attempted code that would that should play 3 different sounds based on different weight variation code failed but also was advised by rob to pause on code.

include <Arduino.h>
include "pitches.h"

// Calibrating the load cell

// HX711 circuit wiring
const int LOADCELL_DAT_PIN = 2;
const int LOADCELL_CLK_PIN = 3;

HX711 scale;

// Threshold weights for specific sounds (in grams)
const long SOUND_1_WEIGHT = 100^150;
const long SOUND_2_WEIGHT = 150^200;
const long SOUND_3_WEIGHT = 200^250;

void setup() {
Serial.begin(57600);
scale.begin(LOADCELL_DAT_PIN, LOADCELL_CLK_PIN);
}

void loop() {

if (scale.is_ready()) {
scale.set_scale();
Serial.println("Tare... remove any weights from the scale.");
delay(5000);
scale.tare();
Serial.println("Tare done...");
Serial.print("Place a known weight on the scale...");
delay(5000);
long reading = scale.get_units(10);
Serial.print("Result: ");
Serial.println(reading);

scss
Copy code
// Compare reading to threshold values and output sound
if (reading >= SOUND_1_WEIGHT && reading < SOUND_2_WEIGHT) {
  tone(8, NOTE_C4, 50);
} else if (reading >= SOUND_2_WEIGHT && reading < SOUND_3_WEIGHT) {
  tone(8, NOTE_D4, 50);
} else if (reading >= SOUND_3_WEIGHT) {
  tone(8, NOTE_E4, 50);
}
}
else {
Serial.println("HX711 not found.");
}
delay(1000);
}

vbnet
Copy code

The bone transducer wasn't powerful enough to generate the loud enough sound and vibrations needed. This will be for a later aspect of the project now and will be replaced by regular speakers. Speakers are in the process of being sourced. Bone… also had to be rewired due to faulty wires.

**Load cell:** Load cell is responsible for calibrating and changing force/weight into electrical readings that are sent to the Arduino.

![Image](image3.png)

Load cells require an amplifier in order to send the low electrical signals to the Arduino.

![Image](image4.png)

Load cell and HX711 amplifier chip soldering was a success. HX711 and load cell later experienced hardware failure, now awaiting replacement cell.

![Image](image5.png)

Obtained new load cell, time to check if load cell functions
