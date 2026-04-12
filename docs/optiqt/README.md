


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


## ⚙️ Installation

### 1️⃣ Cloner le dépôt

```bash
git clone https://github.com/h-marouan/OptiQt.git
cd OptiQt


2️⃣ Créer un environnement virtuel
bash
python -m venv .venv

Sous Windows :
bash
=======



## ⚙️ Installation



### 1️⃣ Cloner le dépôt

git clone https://github.com/h-marouan/OptiQt.git

cd OptiQt






###  2️⃣ Créer un environnement virtuel

python -m venv .venv

Sous Windows :


.venv\Scripts\activate


Sous Linux / macOS :

bash
source .venv/bin/activate

3️⃣ Installer les dépendances

bash
=======

source .venv/bin/activate






###  3️⃣ Installer les dépendances


pip install -r requirements.txt




📦 Contenu du fichier requirements.txt
=======




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



🧠 Utilisation
Démarrage du projet :

bash
=======




### 🧠 Utilisation

Démarrage du projet :

>>>>>>> fb1d2e37bed1c7bd6609854a9cb432fd728628cf
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


bash
pytest tests/
Tu peux ajouter des tests dans tests/ au fur et à mesure du développement (par ex. pour tester la génération de G-code ou le traitement d’image).

💡 Contributions
Les contributions sont les bienvenues !
Avant de soumettre une Pull Request :

=======


pytest tests/
Tu peux ajouter des tests dans tests/ au fur et à mesure du développement (par ex. pour tester la génération de G-code ou le traitement d’image).







### 💡 Contributions

Les contributions sont les bienvenues !
Avant de soumettre une Pull Request :



Crée une branche :

bash
git checkout -b feature/ma-fonction
Vérifie les tests :


=======



bash
pytest
Respecte la structure du code et les docstrings.


📄 Licence
Projet distribué sous licence MIT — voir le fichier LICENSE.

👨‍💻 Auteur
Marouan HAMZA
Ingénieur en génie électrique & informatique industrielle
📧 Contact : [marouan.hamza@outlook.com]
🔗 LinkedIn : [https://www.linkedin.com/in/marouan-hamza/]

🌟 Remarques
=======






### 👨‍💻 Auteur

Marouan HAMZA

Ingénieur en génie électrique & informatique industrielle

📧 Contact : [marouan.hamza@outlook.com]

🔗 LinkedIn : [https://www.linkedin.com/in/marouan-hamza/]








### 🌟 Remarques


Le projet est actuellement en phase de structuration.

L’objectif est de construire une base solide pour le futur développement de modules réels (vision, CNC, optimisation…).

Chaque module contient déjà un fichier Python avec docstring minimal, prêt à être implémenté.


🛠️ Comment utiliser ce projet dans ton environnement
=======








### 🛠️ Comment utiliser ce projet dans ton environnement


🔹 Étape 1 : Extraire le ZIP
Décompresse le dossier OptiQt_skeleton.zip que tu as téléchargé.

🔹 Étape 2 : Ouvrir dans ton IDE
Ouvre le dossier OptiQt/ dans VS Code ou PyCharm.
Le fichier main.py est le point d’entrée : tu peux y mettre ton code de test principal.

🔹 Étape 3 : Lancer ton environnement virtuel
Active ton environnement .venv et installe les dépendances (voir section Installation ci-dessus).

🔹 Étape 4 : Commencer le développement

=======


Tu peux implémenter progressivement chaque module :

core/gcode_generator.py → génération de G-code

vision/image_processing.py → analyse d’image

cnc/motion_controller.py → envoi des commandes moteur

ui/gui_main.py → interface utilisateur



🎯 En résumé :

Télécharge le projet → Crée ton venv → Installe les dépendances → Lance main.py → Développe et teste tes modules.
=======



### 🎯 En résumé :

Télécharge le projet → Crée ton venv → Installe les dépendances → Lance main.py → Développe et teste tes modules.
