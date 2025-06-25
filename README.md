# 🚗 Obstacle Detection System using Ultrasonic Sensor & Arduino Uno

## 📌 Project Overview

This is a beginner-friendly project that uses an **ultrasonic sensor (HC-SR04)** with an **Arduino Uno** to detect obstacles in front of it — similar to how SONAR works. When an object comes within a certain range, the system triggers a visual or sound alert using LEDs or a buzzer.

Perfect for applications like:
- Basic robotics navigation
- Obstacle avoidance cars
- Blind spot monitoring
- Smart parking sensors

---

## 🎯 Objective

The goal is to **detect obstacles using sound waves (ultrasound)** and alert the system when an object is closer than a set distance (like <15 cm). This mimics SONAR functionality.

---

## ⚙️ Components Used

| Component              | Quantity |
|------------------------|----------|
| Arduino Uno            | 1        |
| HC-SR04 Ultrasonic Sensor | 1    |
| Buzzer (optional)      | 1        |
| Red LED                | 1        |
| Green LED (optional)   | 1        |
| Jumper Wires           | As needed |
| Breadboard             | 1        |
| USB Cable              | 1        |

---

## 🔌 Circuit Diagram

**Ultrasonic Sensor (HC-SR04) Connections:**

| Sensor Pin | Connects To     |
|------------|-----------------|
| VCC        | 5V (Arduino)    |
| GND        | GND (Arduino)   |
| TRIG       | Digital Pin 9   |
| ECHO       | Digital Pin 10  |

**Other Connections:**
- Red LED → Digital Pin 6 (via 220Ω resistor)
- Green LED → Digital Pin 5 (optional, for safe distance)
- Buzzer (optional) → Digital Pin 7

---

## 💡 Working Principle

- The ultrasonic sensor sends out a high-frequency sound wave.
- It listens for the echo that bounces back after hitting an object.
- The Arduino calculates the time taken and converts it into distance.
- If the distance is less than the threshold, the system alerts the user via LEDs or a buzzer.

---

## 🧾 Arduino Code

```cpp
#define trigPin 9
#define echoPin 10
#define redLed 6
#define greenLed 5
#define buzzer 7

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(redLed, OUTPUT);
  pinMode(greenLed, OUTPUT);
  pinMode(buzzer, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance < 15) {
    digitalWrite(redLed, HIGH);
    digitalWrite(buzzer, HIGH);
    digitalWrite(greenLed, LOW);
  } else {
    digitalWrite(redLed, LOW);
    digitalWrite(buzzer, LOW);
    digitalWrite(greenLed, HIGH);
  }

  delay(500);
}
