# Gestionnaire d'énergie 8 ports

Le **Power Manager 8 ports** de [Catroniq](https://catroniq.com/gesterner8ports) mesure la consommation de jusqu'à 8 circuits de votre panneau électrique avec des pinces ampèremétriques (CT). Les mesures arrivent directement dans [Home Assistant](https://www.home-assistant.io/) grâce à [ESPHome](https://esphome.io/).

**[Voir le kit et la documentation sur catroniq.com](https://catroniq.com/gesterner8ports)**

![Power Manager 8 ports](https://raw.githubusercontent.com/djiesr/JLNTR2K4-power-manager/main/board.jpg)

## Fonctions

- 8 entrées pour pinces CT de 5 à 100 A (sortie 1 V, 0,5 V ou 0,333 V)
- Courant (A), puissance (kW) et énergie du jour (kWh) pour chaque circuit
- Circuits 120 V ou 240 V
- Réglage des pinces directement dans Home Assistant, sans modifier de code
- Écran OLED qui affiche les mesures en boucle
- Page web intégrée, utilisable même sans Home Assistant
- Compatible avec le tableau de bord Énergie de Home Assistant

## Installation

Branchez la carte à votre ordinateur avec un câble USB, puis cliquez sur le bouton ci-dessous. Le firmware s'installe directement depuis votre navigateur, puis la page vous demande votre réseau Wi-Fi.

<script type="module" src="https://unpkg.com/esp-web-tools@10.4.0/dist/web/install-button.js?module"></script>
<esp-web-install-button manifest="./manifest.json"></esp-web-install-button>

- Fonctionne avec **Chrome** ou **Edge** sur ordinateur (pas sur Firefox, Safari ni téléphone).
- Si la carte n'est pas détectée, installez le [pilote USB CH340](https://www.wch-ic.com/downloads/CH341SER_EXE.html), puis réessayez.

Une fois la carte connectée au Wi-Fi, Home Assistant la détecte automatiquement : ouvrez **Paramètres → Appareils et services** et cliquez sur **Configurer** sous ESPHome.

## Configuration des pinces

Par défaut, les 8 canaux sont à **None** (désactivés) pour éviter les valeurs au hasard sur les entrées sans pince. Pour chaque canal utilisé, ouvrez l'appareil dans Home Assistant, section **Configuration**, puis choisissez :

| Réglage | Valeurs | Description |
|---|---|---|
| CT Model | None, 5 A … 100 A | Calibre de la pince (inscrit sur la pince) |
| CT Output | 1 V, 0.5 V, 0.333 V | Tension de sortie de la pince à pleine charge |
| Circuit Voltage | 120 V, 240 V | 240 V pour un circuit à deux pôles (sécheuse, chauffe-eau, plinthes) |
| CT Correction | 50 à 150 % | Ajustement fin, à comparer avec une pince ampèremétrique de référence |

Les réglages sont conservés dans la carte, même après une panne de courant ou une mise à jour.

## Utilisateurs d'ESPHome

Vous pouvez aussi adopter la carte dans le tableau de bord ESPHome, ou copier le fichier YAML de votre modèle depuis le [dépôt GitHub](https://github.com/djiesr/JLNTR2K4-power-manager).

---

[catroniq.com](https://catroniq.com/gesterner8ports)
