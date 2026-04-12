# Smart Viewer v4.2 — Inspection & Correction Couleur Temps Réel

*Smart Viewer* est un système d'inspection industrielle embarqué conçu pour détecter et corriger en temps réel les défauts d'impression couleur sur une ligne de production (sachets imprimés).
Le système est déployé chez *ROTOTECA Engineering* et a contribué à une amélioration de l'efficacité de production de **+15 à +27 %**.

L'architecture est *distribuée* : un Raspberry Pi 5 assure le traitement d'image et l'interface opérateur, tandis qu'un Raspberry Pi Pico W pilote 4 moteurs pas-à-pas NEMA23 (via drivers TB6600) pour la correction physique des décalages couleur (Rouge, Vert, Bleu, Jaune). Les deux nœuds communiquent par *RS485*, choisi pour sa fiabilité sur 8 mètres en environnement industriel perturbé (EMI).

---

## Objectifs du projet

- Inspecter la qualité couleur des impressions en sortie de machine ;
- Corriger les décalages de repérage couleur (RVBJ) via des moteurs pilotés à distance ;
- Synchroniser la cadence caméra avec la vitesse de la ligne (capteur d'impulsion) ;
- Offrir une interface opérateur tactile intuitive et réactive sous charge.

---

## Approche technique

Le traitement d'image repose sur *OpenCV* et *Picamera2* (capteur IMX519).
La valeur du projet réside dans :

- l'architecture distribuée RPi5 + Pico W avec communication RS485 ;
- le protocole binaire 7 octets avec checksum et acquittement ;
- le multithreading strict séparant UI, traitement image et commandes moteur ;
- l'éclairage LED synchronisé avec la capture (0.2 ms ON par frame → 99.6 % de réduction thermique) ;
- la conception hardware complète : 4 PCB sur mesure (Altium Designer) et boîtier 3D.

---

## Architecture

```
Raspberry Pi 5 (contrôleur principal)
├── CameraApp (PyQt5 GUI — camera_app.py)
├── CameraManager (threaded Picamera2 — camera_manager.py)
├── FramerateCalculator (pulse → FPS — framerate_calculator.py)
├── GpioHandler (capteur impulsion GPIO 25 — gpio_handler.py)
├── LED Ring WS2812B ×16 (SPI GPIO 10 — led_controller.py)
├── Moteur local (PWM GPIO 12 — déplacement caméra)
└── RS485Controller (rs485_controller.py)
        ↓ UART + MAX485 (câble blindé 8m)
    Pico W (pico_motor_controller.py)
        ↓ 4× TB6600 drivers
    4× Moteurs NEMA23 (correction R/G/B/Y)
```

---

## Technologies

| Catégorie | Technologies |
|---|---|
| Langage | Python 3 (RPi5), MicroPython (Pico W) |
| Interface | PyQt5 — tactile 1920×1080 |
| Vision | OpenCV, Picamera2, capteur IMX519 (RGB888) |
| Communication | RS485 (pyserial), UART, protocole binaire 7 octets |
| Moteurs | 4× NEMA23 + TB6600, PWM hardware |
| Éclairage | WS2812B (16 LEDs) via SPI |
| Hardware | GPIO (gpiozero), MAX485, 74HCT245N |
| PCB | Altium Designer |
| 3D | Modélisation boîtier (fichiers STEP) |

---

## Fonctionnalités clés

1. **Caméra live** — 20 FPS synchronisé avec la vitesse machine via capteur d'impulsion
2. **Correction couleur** — 4 moteurs indépendants pour le repérage RVBJ
3. **RS485 distant** — câble blindé 8m, protocole binaire avec checksum et acquittement
4. **Interface tactile** — clavier virtuel, zoom, palette 30 couleurs, pipette
5. **Éclairage synchronisé** — strobing LED (0.2 ms ON → 99.6 % réduction thermique)
6. **Mode simulateur** — test complet sans matériel (`RS485_USE_SIMULATOR = True`)

---

## Problèmes rencontrés & solutions

### 1. Synchronisation vision / actionneurs
**Problème** : Latence entre la détection d'un défaut et la correction physique.
**Solution** : Architecture multithreading avec bus de messages interne séparant le pipeline de traitement image du pipeline de commande moteur.

### 2. Stabilité de l'interface sous charge
**Problème** : Le traitement OpenCV en temps réel saturait le thread UI.
**Solution** : Isolation stricte des threads UI et traitement, avec queue thread-safe pour la communication inter-threads.

### 3. Fiabilité du lien RS485
**Problème** : Pertes de trames lors de rafales de commandes.
**Solution** : Protocole de communication avec acquittement et retry automatique implémenté côté MicroPython sur le Pico W.

### 4. Calibration couleur
**Problème** : Variabilité des conditions lumineuses affectant la détection.
**Solution** : Algorithme de calibration automatique au démarrage avec profil de référence réglable par l'opérateur.

---

## Résultats & apprentissages

| Résultat | Détail |
|---|---|
| 📈 **Impact production** | +15 à +27 % d'efficacité de production chez ROTOTECA, réduction des rebuts liés aux défauts couleur |
| 🔄 **Architecture distribuée** | Le découpage RPi5 + Pico W s'est révélé plus robuste et maintenable qu'une solution monolithique, permettant la mise à jour de chaque nœud indépendamment |
| ⚡ **Temps réel validé** | Le multithreading Python, combiné à l'architecture distribuée, suffit pour atteindre les contraintes temps réel sans recourir au C++ |

---

## Matériel

### Composants principaux
- Raspberry Pi 5
- Raspberry Pi Pico W
- Caméra IMX519 (1920×1080)
- 4× Moteurs NEMA23 + Drivers TB6600
- 2× Modules MAX485 (RS485)
- LED Ring WS2812B (16 LEDs)
- Convertisseur de niveau 74HCT245N
- Alimentation 24V
- Résistances de terminaison 120Ω
- Câble RS485 blindé (8m)
- Écran tactile

### PCB conçus (Altium Designer)
1. **pcb-camera** — Carte caméra principale
2. **dc-motor-controller** — Contrôleur LED + moteur
3. **2in1-flex-board** — Carte flex combinée
4. **GPIO et Moteur-control** — Carte contrôle GPIO/moteur

---

## Historique des versions

| Version | Description |
|---|---|
| v1 | Premier prototype — caméra + GPIO + clavier virtuel |
| v3.0 | Architecture modulaire (camera_manager, gpio_handler séparés) |
| v3.1 | Stabilisation, simulateur de sacs, configuration externalisée |
| v3.2.1 | Amélioration du contrôle moteur couleur |
| v3.4 | Affinements et corrections |
| v4.0 | **Architecture RS485** — Pico W, MAX485, protocole binaire |
| v4.2 | **Version actuelle** — PWM hardware, SPI LED, synchronisation LED-framerate, optimisation thermique |

---

## Images pour le portfolio

Les images suivantes sont à inclure dans la présentation portfolio :

1. **smart-viewer-architecture.png** — Schéma d'architecture globale (RPi5 ↔ RS485 ↔ Pico W ↔ TB6600 ↔ NEMA23 + caméra + LED + écran). *À créer avec draw.io ou Figma.*
2. **smart-viewer-main.png** — Capture ou mockup de l'interface PyQt5 (vue caméra live + panneau correction couleur).
3. **smart-viewer-pcb.png** — Rendus 3D des 4 PCB Altium sur une même image. *Disponible dans `pcb-altium/`.*
4. **smart-viewer-3d.png** — Rendu 3D du boîtier/assemblage. *Disponible dans `3d fini/`.*
5. **smart-viewer-rs485.png** — Schéma du protocole RS485 (trame 7 octets, flux RPi5 → MAX485 → câble → MAX485 → Pico W, acquittement). *À créer avec draw.io.*
6. **smart-viewer-hardware.png** — Photo du montage réel ou diagramme de câblage technique.
