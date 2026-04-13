### 👨‍💻 Auteur

Marouan HAMZA

Ingénieur en génie électrique & informatique industrielle

📧 Contact : [marouan.hamza@outlook.com]

🔗 LinkedIn : [https://www.linkedin.com/in/marouan-hamza/]


# Robot AI – Virtual Industrial Company

## 📌 Présentation générale

Ce projet consiste à concevoir un **robot intelligent autonome**, basé sur un **Raspberry Pi 5**, intégrant une **architecture multi-agents IA** s’appuyant sur des **modèles pré-entraînés (LLaMA, Mixtral, etc.) via Groq** pour la rapidité d’exécution.

Le robot représente une **entreprise virtuelle complète**, dans laquelle chaque agent IA joue un rôle professionnel précis (direction, ingénierie, marché, finance, etc.).  
Je conserve le rôle de **CEO et administrateur principal**, avec validation finale de toutes les décisions sensibles.

L’objectif final est de :
- analyser les besoins du **marché local (France)**,
- discuter de la faisabilité technique et économique des projets,
- définir les ressources nécessaires,
- produire une vision complète d’un projet industriel **livrable de bout en bout**.

Un projet réel déjà en cours servira de **premier cas d’étude** et de validation du système.

---

## 🎯 Philosophie du projet

- Je **n’entraîne pas de modèle IA** : j’utilise des **LLM pré-entraînés**.
- La valeur du projet réside dans :
  - l’architecture logicielle,
  - l’orchestration des agents,
  - la mémoire persistante,
  - la sécurité,
  - l’intégration matériel / logiciel.
- Le LLM est considéré comme un **cerveau puissant mais sans mémoire**.
- La mémoire, les règles, la cohérence et la sécurité sont gérées **par le système**.

---

## 🧠 Architecture fonctionnelle

Le robot est conçu comme un **chef d’orchestre intelligent** :

- perception (voix, vision),
- raisonnement multi-agents,
- mémoire long terme,
- interface visuelle,
- actions sur systèmes externes (PC, logiciels, APIs).

### Vue globale

Voix / Clavier / Vision
        ↓
    Input Router
        ↓
   Security Manager
        ↓
    Agent Manager
        ↓
  Agents IA (LLM)
        ↓
  Memory Manager
        ↓
UI / Actions / Rapports
 
---

## 🤖 Agents IA (entreprise virtuelle)

Tous les agents utilisent des **modèles pré-entraînés** (LLaMA, Mixtral, etc.).  
La différenciation se fait uniquement par :
- le prompt système,
- les outils autorisés,
- l’accès mémoire,
- le rôle métier.


### Rôles définis

- **CEO (moi)** : vision, validation finale, priorités
- **COO (agent principal)** : coordination globale, cohérence projet
- **Ingénieur technique** : faisabilité électronique, mécanique, systèmes
- **Ingénieur logiciel** : automatisation, APIs, scripts
- **Analyste marché** : besoins industriels, tendances, pain points
- **Finance** : coûts, ROI, prix de revient
- **Qualité / risques** : conformité, fiabilité, sécurité
- **Industrialisation** : production, tests, scalabilité
le modèle sera choisi selon le rôle de l'agent, exemple: pour un ingénieur logiciel le modèle le plus intelligent(Claude Sonnet 4) sera privilégié au plus rapide (LLaMA 3.3-70B)...

---

## 🧩 Composants matériels ciblés

Le robot final sera équipé de :

- **Raspberry Pi 5**
- **Écran 5 pouces** (HDMI ou DSI)
- **Caméra** (reconnaissance faciale)
- **Microphone**
- **Haut-parleur**
- **Bouton physique** (validation tâches sensibles)
- **LED RGB** (état système)
- Stockage SSD

### Rôle de l’écran
- affichage des calculs,
- graphes,
- tableaux,
- confirmations,
- dashboards système.

L’écran est une **interface d’observation et de validation**, jamais un bloqueur logique.

---

## 🔐 Sécurité et contrôle

Les actions sensibles (exécution sur PC, suppression de données, automatisation logicielle) nécessitent une **validation multi-niveaux** :

1. Reconnaissance faciale (administrateur)
2. Commande valide
3. Confirmation visuelle à l’écran
4. Bouton physique (optionnel mais recommandé)

---

## 🖥️ Développement PC → Raspberry Pi

Le développement commence volontairement sur **PC**, puis sera migré vers le Raspberry Pi.

Principe fondamental :
> Le cœur du système ne dépend jamais du matériel.

### Différences contrôlées

| Élément | PC | Raspberry Pi |
|------|----|---------------|
| Entrée | CLI / clavier | Micro |
| Caméra | Webcam | Caméra RPI |
| Écran | Fenêtre UI | Écran 5" |
| Agents | Identiques | Identiques |
| Mémoire | Identique | Identique |

La migration consiste uniquement à changer la **configuration**, jamais la logique.

---

## 💾 Mémoire et persistance

Les agents n’ont aucune mémoire native.  
Toute la mémoire est gérée par le système :

- mémoire entreprise,
- mémoire projet,
- résumés automatiques,
- historique de décisions.

Technologies prévues :
- SQLite (base)
- Vector DB (FAISS / Chroma) pour le contexte long terme

La mémoire est **persistante et transférable** entre machines.

---

## 🧱 Architecture logicielle

robot_ai/
│
├── main.py
│
├── config/
│ ├── system.yaml
│ ├── agents.yaml
│ └── security.yaml
│
├── core/
│ ├── agent_manager.py
│ ├── memory_manager.py
│ ├── security_manager.py
│ ├── event_bus.py
│
├── agents/
│ ├── ceo.py
│ ├── coo.py
│ ├── engineer.py
│ ├── software.py
│ ├── market.py
│ ├── finance.py
│ └── quality.py
│
├── perception/
│ ├── audio_in.py
│ ├── audio_out.py
│ ├── live_voice_mode.py
│ ├── speech_recognition.py
│ ├── text_to_speech.py
│ ├── keyboard_in.py
│ ├── vision.py
│ └── input_router.py
│
├── ui/
│ ├── screen_manager.py        # Gestionnaire principal (fenêtre PyQt6)
│ ├── dashboard.py             # Panneau conversation + contexte
| ├── avatar.py               # Agent animé (yeux/bouche)
| ├── charts.py               # Graphes + visualisations
| ├── notifications.py        # Système d'alertes
| ├── keyboard_virtual.py     # Clavier virtuel tactile
| └── styles.py               # CSS-like pour PyQt6
│
|
├── actions/
│ ├── pc_control.py
│ ├── api_calls.py
│ ├── system_actions.py
│ └── confirmations.py
│
├── hardware/
│ ├── gpio.py
│ ├── leds.py
│ └── buttons.py
│
├── data/
│ ├── memory.db
│ ├── vectors/
│ ├── logs/
│ ├── audio/
│ ├── conersations/
│ ├── profiles/
│ ├── logs/
│ └── projects/
│
└── tests/

---

## 🗺️ Roadmap

### Phase 1 – Fondations
- structure projet
- agent manager
- COO opérationnel
- mémoire persistante

### Phase 2 – Interaction
- CLI
- UI écran
- visualisation des résultats

### Phase 3 – Sécurité & perception
- caméra
- reconnaissance faciale
- règles d’accès

### Phase 4 – Automatisation
- contrôle PC
- interaction logiciels
- confirmations sécurisées

### Phase 5 – Migration RPI
- audio réel
- écran embarqué
- boîtier robot

---

## 🧠 Vision finale

Ce projet est un **outil de décision industrielle intelligent**, incarné physiquement par un robot, combinant :

- électronique,
- automatisation,
- intelligence artificielle,
- architecture logicielle propre,
- vision système.

---

## ⚠️ Notes importantes

- Le projet évoluera par modules.
- Chaque ajout doit être **non destructif**.
- Toute logique doit rester indépendante du matériel.
- La sécurité est prioritaire.

---

