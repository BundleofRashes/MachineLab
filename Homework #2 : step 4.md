#include <Servo.h>

class Flasher {
  int ledPin;
  unsigned long onTime, offTime;
  int ledState;
  unsigned long previousMillis;

public:
  Flasher(int pin, unsigned long on, unsigned long off)
  : ledPin(pin), onTime(on), offTime(off), ledState(LOW), previousMillis(0)
  {
    pinMode(ledPin, OUTPUT);
    digitalWrite(ledPin, ledState);
  }

  void Update() {
    unsigned long now = millis();

    if (ledState == HIGH && (now - previousMillis) >= onTime) {
      ledState = LOW;
      previousMillis = now;
      digitalWrite(ledPin, ledState);
    } else if (ledState == LOW && (now - previousMillis) >= offTime) {
      ledState = HIGH;
      previousMillis = now;
      digitalWrite(ledPin, ledState);
    }
  }
};

class Sweeper {
  Servo servo;
  int pos;
  int increment;
  unsigned long updateInterval;
  unsigned long lastUpdate;

public:
  Sweeper(unsigned long intervalMs)
  : pos(0), increment(1), updateInterval(intervalMs), lastUpdate(0) {}

  void Attach(int pin) { servo.attach(pin); }

  void SetInterval(unsigned long intervalMs) {
    updateInterval = intervalMs;
  }

  void Update() {
    unsigned long now = millis();
    if (now - lastUpdate >= updateInterval) {
      lastUpdate = now;

      pos += increment;
      servo.write(pos);

      if (pos >= 180 || pos <= 0) {
        increment = -increment;
      }
    }
  }
};

const int buttonPin = 2;   // INPUT_PULLUP: pressed = LOW
const int potPin    = A0;  // potentiometer wiper
const int servoPin1 = 9;
const int servoPin2 = 10;

// Pot controls sweep speed by changing the step interval (ms)
const unsigned long MIN_INTERVAL_MS = 2;   // fastest
const unsigned long MAX_INTERVAL_MS = 40;  // slowest

Flasher led1(11, 123, 400);
Flasher led2(12, 350, 350);
Flasher led3(13, 200, 222);

Sweeper sweeper1(15);
Sweeper sweeper2(25);

void setup() {
  Serial.begin(9600);
  pinMode(buttonPin, INPUT_PULLUP);

  sweeper1.Attach(servoPin1);
  sweeper2.Attach(servoPin2);
}

void loop() {
  bool buttonPressed = (digitalRead(buttonPin) == LOW);

  int pot = analogRead(potPin); // 0..1023
  unsigned long intervalMs = map(pot, 0, 1023, MIN_INTERVAL_MS, MAX_INTERVAL_MS);

  // Apply pot speed to both servos
  sweeper1.SetInterval(intervalMs);
  sweeper2.SetInterval(intervalMs);

  if (buttonPressed) {
    sweeper1.Update();
    sweeper2.Update();
    led1.Update(); // only blinks while pressed (keep/remove as you want)
  }

  led2.Update();
  led3.Update();
}

