# 🚗 Capteur de véhicule

## 📄 Description
Le but de ce projet est de concevoir un système simple et efficace permettant de détecter, à l’aide d’un capteur, la présence d’un véhicule. Ce système peut être utilisé pour améliorer le stationnement, renforcer la sécurité routière, ou automatiser des barrières.

## 🎯 Objectif
Créer un système embarqué basé sur Arduino capable d’indiquer la proximité d’un véhicule en allumant des LEDs de différentes couleurs, tout en ajustant le rythme sonore d’un buzzer selon la distance.

## 🧰 Matériel utilisé
- Carte Arduino UNO  
- Capteur ultrason HC-SR04  
- Bande de 21 LEDs WS2812  
- Buzzer passif  
- Breadboard  
- Câbles de connexion  
- Câble USB  
- Senseur Shield (facultatif)

## ⚙️ Principe de fonctionnement
Le système mesure la distance entre le capteur ultrason et un obstacle (véhicule). Il réagit de la manière suivante :

| Distance mesurée | LEDs allumées | Couleur des LEDs | Fréquence du buzzer |
|------------------|----------------|------------------|----------------------|
| <= 10 cm         | 21             | Rouge            | Très rapide          |
| <= 20 cm         | 15             | Orange           | Rapide               |
| <= 30 cm         | 10             | Vert foncé        | Moyenne              |
| <= 40 cm         | 5              | Vert clair        | Lente                |
| > 40 cm          | 0              | Aucune            | Aucune               |

## 💻 Code Arduino


#include <FastLED.h>

const int trigPin = A2;
const int echoPin = A3;
const int buzzerPin = 2;
const int NUM_LEDS = 21;
const int DATA_PIN = 4;

CRGB leds[NUM_LEDS];

float duration, distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  FastLED.addLeds<WS2812, DATA_PIN, RGB>(leds, NUM_LEDS);
}

void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = (duration * 0.0343) / 2;

  int ledCount = 0;
  int buzzerDelay = 0;

  for (int i = 0; i < NUM_LEDS; i++) {
    leds[i] = CRGB(0, 0, 0);
  }

  if (distance <= 10) {
    ledCount = 21;
    for (int i = 0; i < ledCount; i++) {
      leds[i] = CRGB(255, 0, 0); // Rouge
    }
    buzzerDelay = 300;
  }
  else if (distance <= 20) {
    ledCount = 15;
    for (int i = 0; i < ledCount; i++) {
      leds[i] = CRGB(255, 165, 0); // Orange
    }
    buzzerDelay = 500;
  }
  else if (distance <= 30) {
    ledCount = 10;
    for (int i = 0; i < ledCount; i++) {
      leds[i] = CRGB(0, 100, 0); // Vert foncé
    }
    buzzerDelay = 700;
  }
  else if (distance <= 40) {
    ledCount = 5;
    for (int i = 0; i < ledCount; i++) {
      leds[i] = CRGB(0, 255, 0); // Vert clair
    }
    buzzerDelay = 900;
  }

  if (buzzerDelay > 0) {
    digitalWrite(buzzerPin, HIGH);
    delay(buzzerDelay);
    digitalWrite(buzzerPin, LOW);
  }

  FastLED.show();
  delay(300);
}
