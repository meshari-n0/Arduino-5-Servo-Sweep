# Arduino 5 Servo Sweep

This project demonstrates controlling **5 servo motors simultaneously** using an Arduino Uno.  
All servos move together in a smooth sweeping motion, then stop at a fixed position.

---

## 📷 Wiring Diagram

![Wiring Diagram](images/wiring.png)

---

## 🔌 Components

- Arduino Uno
- 5x Servo Motors (SG90 or similar)
- Breadboard
- Jumper wires

---

## ⚙️ How It Works

1. All 5 servos move from **0° → 180°**
2. Then move back from **180° → 0°**
3. This motion repeats for **2 seconds**
4. After that, all servos stop at **90°**
5. Program halts completely

---

## 🧠 Pins Configuration

| Servo | Arduino Pin |
|------|------------|
| Servo 1 | 8 |
| Servo 2 | 9 |
| Servo 3 | 10 |
| Servo 4 | 11 |
| Servo 5 | 12 |

---

## 💻 Code

```cpp
#include <Servo.h>

Servo servo1;
Servo servo2;
Servo servo3;
Servo servo4;
Servo servo5;

int pos = 0;

void setup() {
  servo1.attach(8);
  servo2.attach(9);
  servo3.attach(10);
  servo4.attach(11);
  servo5.attach(12);
}

void loop() {

  // Sweep for 2 seconds
  unsigned long startTime = millis();

  while (millis() - startTime < 2000) {

    for (pos = 0; pos <= 180; pos += 5) {
      moveAll(pos);
      delay(15);
    }

    for (pos = 180; pos >= 0; pos -= 5) {
      moveAll(pos);
      delay(15);
    }
  }

  // Hold at 90 degrees
  moveAll(90);

  while (true); // stop program
}

void moveAll(int angle) {
  servo1.write(angle);
  servo2.write(angle);
  servo3.write(angle);
  servo4.write(angle);
  servo5.write(angle);
}
