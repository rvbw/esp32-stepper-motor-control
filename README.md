# ESP32 Stepper Motor Control with Acceleration

## Overview
This project demonstrates how to control a bipolar stepper motor using an ESP32 and A4988 stepper motor driver.

The motor performs:
1. One full rotation clockwise
2. One full rotation counterclockwise
3. Gradual acceleration from low speed to maximum speed

This project introduces stepper motor control concepts such as step signals, direction control, and acceleration techniques.

---

## Components
- ESP32
- Bipolar Stepper Motor
- A4988 Stepper Motor Driver
- Jumper Wires

---

## Circuit Connection

### ESP32 to A4988:
- STEP → GPIO 26
- DIR  → GPIO 27
- VDD  → 3.3V or 5V
- GND  → GND

### Motor Power:
- VMOT → External Power (5V recommended in simulation)
- GND  → GND

### Stepper Motor:
- A1, A2 → Coil 1
- B1, B2 → Coil 2

---

## Code

```cpp
#define STEP_PIN 26
#define DIR_PIN  27

int stepsPerRevolution = 800;

void setup() {
  pinMode(STEP_PIN, OUTPUT);
  pinMode(DIR_PIN, OUTPUT);
}

void loop() {

  // Clockwise
  digitalWrite(DIR_PIN, LOW);

  for (int i = 0; i < stepsPerRevolution; i++) {
    int speedDelay = 8000 - (i * 8);

    digitalWrite(STEP_PIN, HIGH);
    delayMicroseconds(speedDelay);
    digitalWrite(STEP_PIN, LOW);
    delayMicroseconds(speedDelay);
  }

  delay(1000);

  // Counterclockwise
  digitalWrite(DIR_PIN, HIGH);

  for (int i = 0; i < stepsPerRevolution; i++) {
    int speedDelay = 8000 - (i * 8);

    digitalWrite(STEP_PIN, HIGH);
    delayMicroseconds(speedDelay);
    digitalWrite(STEP_PIN, LOW);
    delayMicroseconds(speedDelay);
  }

  delay(3000);
}
