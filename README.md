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

