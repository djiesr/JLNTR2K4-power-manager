# Gestionnaire d'énergie 8 ports

Le **Power Manager 8 ports** de [Catroniq](https://catroniq.com/gesterner8ports) mesure la consommation de jusqu'à 8 circuits de votre panneau électrique avec des pinces ampèremétriques (CT). Les mesures arrivent directement dans [Home Assistant](https://www.home-assistant.io/) grâce à [ESPHome](https://esphome.io/).

**[Voir le kit et la documentation sur catroniq.com](https://catroniq.com/gesterner8ports)**

![Power Manager 8 ports](https://raw.githubusercontent.com/djiesr/JLNTR2K4-power-manager/main/board.jpg)

## Fonctions

- 8 entrées pour pinces CT de 5 à 100 A (sortie 1 V, 0,5 V ou 0,333 V)
- Courant (A), puissance (kW) et énergie du jour (kWh) pour chaque circuit
- Circuits 120 V, 240 V (Amérique du Nord) ou 230 V (Europe)
- Réglage des pinces directement dans Home Assistant, sans modifier de code
- Écran OLED qui affiche les mesures en boucle
- Page web intégrée, utilisable même sans Home Assistant
- Compatible avec le tableau de bord Énergie de Home Assistant

## Installation

Branchez la carte à votre ordinateur avec un câble USB, puis cliquez sur le bouton ci-dessous. Le firmware s'installe directement depuis votre navigateur, puis la page vous demande votre réseau Wi-Fi.

<script type="module" src="https://unpkg.com/esp-web-tools@10.4.0/dist/web/install-button.js?module"></script>
<esp-web-install-button manifest="./manifest.json"></esp-web-install-button>

- Fonctionne avec **Chrome** ou **Edge** sur ordinateur (pas sur Firefox, Safari ni téléphone).
- Pas besoin de savoir si votre carte est un ESP8266 ou un ESP32 : le bouton détecte la puce et installe le bon firmware.
- Si la carte n'est pas détectée :
  1. Vérifiez votre câble USB. Plusieurs câbles (souvent ceux fournis avec des écouteurs ou des lampes) servent seulement à la recharge et ne transportent pas les données. Essayez un câble qui permet de transférer des fichiers vers un téléphone.
  2. Installez le [pilote USB CH340](https://www.wch-ic.com/downloads/CH341SER_EXE.html), puis débranchez et rebranchez la carte.

Une fois la carte connectée au Wi-Fi, Home Assistant la détecte automatiquement : ouvrez **Paramètres → Appareils et services** et cliquez sur **Configurer** sous ESPHome.

## Configuration des pinces

Dans Home Assistant, chaque connecteur apparaît comme un appareil séparé (**PM A0** à **PM A7**), relié à la carte. Il regroupe ses mesures (courant, puissance, énergie) et ses réglages.

Par défaut, les 8 canaux sont à **None** (désactivés) pour éviter les valeurs au hasard sur les entrées sans pince. Pour chaque connecteur utilisé, ouvrez son appareil dans Home Assistant, section **Configuration**, puis choisissez :

| Réglage | Valeurs | Description |
|---|---|---|
| CT Model | None, 5 A … 100 A | Calibre de la pince (inscrit sur la pince) |
| CT Output | 1 V, 0.5 V, 0.333 V | Tension de sortie de la pince à pleine charge |
| Circuit Voltage | 120 V, 240 V, 230 V | Tension du circuit (voir ci-dessous) |
| CT Correction | 50 à 150 % | Ajustement fin, à comparer avec une pince ampèremétrique de référence |

Les réglages sont conservés dans la carte, même après une panne de courant ou une mise à jour.

Astuce : renommez l'appareil d'un connecteur dans Home Assistant (par exemple « Sécheuse ») et toutes ses mesures suivent.

### Quelle tension choisir ?

| Circuit | Pinces | Circuit Voltage |
|---|---|---|
| Amérique du Nord, circuit 120 V (prises, éclairage) | 1 pince | 120 V |
| Amérique du Nord, 240 V sans neutre (plinthes, chauffe-eau, thermopompe) | 1 pince sur **un seul** des deux fils | 240 V |
| Amérique du Nord, 240 V avec neutre (sécheuse, cuisinière) | 1 pince : approximation correcte · 2 pinces (une par fil) : mesure exacte | 1 pince : 240 V · 2 pinces : 120 V chacune, puis additionner |
| Entrée principale du panneau | 2 pinces, une par phase | 120 V chacune, puis additionner |
| Europe (monophasé) | 1 pince | 230 V |

**Important :** ne refermez jamais une pince autour des deux fils d'un même circuit. Le courant circule en sens inverse dans chaque fil, les deux s'annulent et la pince lit 0.

## Utilisateurs d'ESPHome

Vous pouvez aussi adopter la carte dans le tableau de bord ESPHome, ou copier le fichier YAML de votre modèle depuis le [dépôt GitHub](https://github.com/djiesr/JLNTR2K4-power-manager).

Pour choisir le bon fichier, regardez le module installé sur la carte :

| | ESP8266 (D1 mini) | ESP32 (D1 mini32) |
|---|---|---|
| Inscription sur la puce métallique | ESP-12F / ESP8266 | ESP32-WROOM |
| Broches | 2 rangées de 8 (16 broches) | 2 rangées doubles de chaque côté (40 broches) |
| Fichier YAML | `power-manager-8c-esp8266-d1-mini.yaml` | `power-manager-8c-esp32-d1-mini.yaml` |
---

[catroniq.com](https://catroniq.com/gesterner8ports)
