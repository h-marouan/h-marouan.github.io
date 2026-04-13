


### 👨‍💻 Auteur

Marouan HAMZA

Ingénieur en génie électrique & informatique industrielle

📧 Contact : [marouan.hamza@outlook.com]

🔗 LinkedIn : [https://www.linkedin.com/in/marouan-hamza/]


# 🧠 OptiQt

**OptiQt** est une plateforme modulaire en Python dédiée à l’optimisation, la simulation et le pilotage intelligent de systèmes CNC, de vision industrielle et de génération de G-code.  
Le projet est structuré pour être **modulaire**, **lisible** et **facilement intégrable** dans des environnements industriels ou de recherche.

---



## 🚀 Objectifs du projet

- Fournir une **base logicielle claire et extensible** pour le développement d’applications de vision et de contrôle CNC.
- Intégrer des modules de :
  - **Vision** : acquisition caméra, traitement d’image, extraction de contours.
  - **CNC** : génération de G-code, communication série, contrôle du mouvement.
  - **Simulation** : visualisation et tests hors ligne.
  - **Interface utilisateur** : GUI ergonomique basée sur Qt.


---



## 🧩 Architecture du projet

OptiQt/

│

├── main.py # Point d'entrée principal du programme

│

├── config/ # Paramètres généraux du projet

│

 └── settings.py

│

├── core/ # Noyau logique du projet

│ ├── logger.py

│ ├── file_manager.py

│ ├── gcode_generator.py

│ ├── math_tools.py

│ ├── contour_extractor.py

│ └── simulation.py

│

├── vision/ # Gestion de la vision industrielle

│ ├── camera_manager.py

│ └── image_processing.py

│

├── cnc/ # Contrôle machine et communication

│ ├── motion_controller.py

│ ├── serial_interface.py

│ └── hardware/

│ ├── hardware_rpi.py

│ └── hardware_unoq.py

│

├── ui/ # Interface graphique (Qt)

│ ├── gui_main.py

│ ├── gui_components.py

│ └── gui_styles.py

│

├── tests/ # Tests unitaires

│ └── test_gcode.py

│

├── requirements.txt # Liste des dépendances Python

└── README.md # Ce fichier 





### 📦 Contenu du fichier requirements.txt

Voici la version minimale à inclure à la racine du projet :

numpy
opencv-python
pyserial
PyQt5
matplotlib
scipy
pytest




🧭 Explication des dépendances :
=======



### 🧭 Explication des dépendances :

Module	Utilisation principale
numpy	Calculs mathématiques et manipulation de tableaux
opencv-python	Traitement d'image et vision industrielle
pyserial	Communication série avec la machine CNC
PyQt5	Interface graphique (GUI)
matplotlib	Visualisation, simulation et tracés
scipy	Outils mathématiques avancés
pytest	Tests unitaires automatiques



### 🧠 Utilisation

Démarrage du projet :

python OptiQt/main.py
Exemple de sortie console :
bash
Copier le code
> Initializing OptiQt...
> Loading configuration...
> Camera system ready.
> CNC connection established.
> GUI launched successfully.
🧪 Tests unitaires
Pour exécuter les tests :
