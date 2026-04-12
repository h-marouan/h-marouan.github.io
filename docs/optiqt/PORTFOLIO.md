# OptiQt v1.0 — Framework Modulaire Vision & CNC

*OptiQt* est un framework modulaire Python dédié à la vision industrielle et au pilotage de machines CNC, conçu pour le traitement automatisé de verres optiques.
Le système détecte les contours et perçages d'un verre à partir d'une image, génère le G-code correspondant et pilote une machine CNC via Arduino UNO — le tout depuis une interface tactile PyQt6.

Développé chez *ROTOTECA Engineering*, ce framework a servi de base technique pour d'autres solutions industrielles (prévention incendie, interfaces HMI), validant sa réutilisabilité.

---

## Objectifs du projet

- Extraire automatiquement les contours et perçages d'un verre optique par traitement d'image (OpenCV) ;
- Générer du G-code optimisé à partir des résultats de vision, avec compensation d'outil (polygon offset) ;
- Piloter une machine CNC via communication série (Arduino UNO) ;
- Offrir une interface opérateur tactile intuitive, utilisable sur Raspberry Pi en mode kiosque.

---

## Architecture en 4 couches

Le projet est structuré en couches indépendantes, facilitant la maintenance, les tests unitaires et l'extension :

| Couche | Rôle | Modules |
|---|---|---|
| **Core** | Moteur applicatif | contour_extractor, gcode_generator, simulation, math_tools, file_manager |
| **Vision** | Traitement d'image | camera_manager, image_processing |
| **CNC** | Communication machine | motion_controller, serial_interface, hardware_rpi, hardware_unoq |
| **UI** | Interface opérateur | gui_main (PyQt6), gui_components, gui_styles, virtual_keyboard |

---

## Technologies

Python · OpenCV · PyQt6 · PySerial · NumPy · SciPy · Matplotlib · Pytest · Arduino UNO · G-code · Raspberry Pi

---

## Fonctionnalités clés

1. **Extraction de contours** — détection Canny + segmentation adaptative sur images de verres optiques
2. **Détection de perçages** — identification automatique des trous avec validation taille foret vs diamètre
3. **Génération G-code** — trajectoires optimisées avec compensation d'outil (polygon offset), variantes WITH/WITHOUT offset
4. **3 profils matériaux** — Verre Minéral, Polycarbonate, CR39 avec paramètres CNC dédiés (vitesse broche, avance, profondeur de passe)
5. **Pilotage CNC** — communication série Arduino UNO (COM3, 9600 baud), homing G28, déplacements G1
6. **Mode simulation** — exécution complète sans matériel connecté (`SIMULATION_MODE = True`)
7. **Interface tactile** — clavier virtuel intégré, styles QSS personnalisés, conçu pour mode kiosque RPi

---

## Problèmes rencontrés & solutions

### 1. Couplage fort entre vision et CNC
**Problème** : Les premières versions mélangeaient traitement image et génération G-code, rendant les tests difficiles.
**Solution** : Introduction de l'architecture en 4 couches avec interfaces bien définies entre chaque module.

### 2. Précision de la génération G-code
**Problème** : Les contours extraits par OpenCV contenaient du bruit entraînant des trajectoires imprécises.
**Solution** : Pipeline de post-traitement (lissage de courbe, simplification de polygone, filtrage adaptatif).

### 3. Testabilité du code de pilotage machine
**Problème** : Impossible de tester sans une machine physique connectée.
**Solution** : Couche d'abstraction de la communication série avec mock injectable pour les tests unitaires Pytest + mode simulation intégré.

### 4. Gestion des perçages
**Problème** : Risque de casse foret si le diamètre du trou détecté est inférieur au foret sélectionné.
**Solution** : Validation automatique taille foret vs diamètre de perçage, avec dédoublonnage des trous détectés.

---

## Résultats & apprentissages

| Résultat | Détail |
|---|---|
| 🏗️ **Architecture pérenne** | La modularité en 4 couches facilite l'ajout de nouveaux algorithmes de vision et de nouveaux types de machines sans modifier le noyau applicatif |
| 🧪 **Couverture de tests** | L'introduction de Pytest et du mock série a révélé plusieurs bugs de précision dans la génération G-code, améliorant significativement la qualité des trajectoires |
| 🔌 **Polyvalence industrielle** | Le framework a servi de base pour d'autres solutions industrielles (prévention incendie, interfaces HMI), validant sa réutilisabilité |

---

## Images pour le portfolio

1. **optiqt-architecture.png** — Schéma des 4 couches (Core → Vision → CNC → UI) avec flux de données. *À créer avec draw.io.*
2. **optiqt-main.png** — Capture ou mockup de l'interface PyQt6 (image verre + contours + panneau G-code).
3. **optiqt-contour.png** — Exemple de traitement : image brute → contours extraits → G-code généré (montage 3 étapes).
4. **optiqt-gcode.png** — Visualisation d'une trajectoire G-code générée (plot Matplotlib).
5. **optiqt-hardware.png** — Schéma de câblage Arduino UNO ↔ CNC ou photo du setup.
