<div align="center">

# 🪞 BioMirror

### *Le miroir intelligent qui analyse votre bien-être en silence, chaque matin.*

**Projet de Fin d'Études — 2025/2026**

[![Status](https://img.shields.io/badge/Status-In%20Development-yellow)]()
[![License](https://img.shields.io/badge/License-Academic-blue)]()
[![Privacy](https://img.shields.io/badge/Privacy-Edge%20AI-green)]()

[📹 Vidéo de Pitch](#) • [📊 Business Plan](#) • [🎯 Étude de Marché](./docs/Etude_de_Marche.pdf) • [💼 Modèle Économique](./docs/Modele_Economique.pdf)

</div>

---

## 📖 Table des matières

- [À propos du projet](#-à-propos-du-projet)
- [L'équipe](#-léquipe)
- [Architecture technique](#-architecture-technique)
- [Structure du repository](#-structure-du-repository)
- [Technologies utilisées](#-technologies-utilisées)
- [Installation & Lancement](#-installation--lancement)
- [Points forts du POC](#-points-forts-du-poc)
- [Axes d'amélioration & Perspectives](#-axes-damélioration--perspectives)
- [Documents & Livrables](#-documents--livrables)
- [Cadre légal & Éthique](#-cadre-légal--éthique)
- [Contact](#-contact)

---

## 🎯 À propos du projet

**BioMirror** est un miroir intelligent connecté qui analyse, chaque matin et sans aucun effort, les signaux visuels de bien-être de l'utilisateur — fatigue, stress, hydratation, rythme cardiaque — directement sur son reflet, en garantissant que **son visage ne quitte jamais sa salle de bain** grâce à un traitement 100% local (Edge AI).

### Le problème
- Les **wearables** (Oura, Apple Watch) imposent une contrainte d'usage permanente et sont régulièrement oubliés.
- Les **applications mobiles** de bien-être sont abandonnées par 70% des utilisateurs en moins de 30 jours (fatigue de l'engagement actif).
- Les solutions existantes envoient les **données biométriques sensibles dans le Cloud**, posant des risques RGPD majeurs.

### Notre solution
Un miroir qui s'intègre **passivement** à la routine matinale. L'utilisateur fait ce qu'il fait déjà : se regarder dans le miroir. Le système analyse, croise et restitue en quelques secondes un score de vitalité personnalisé, accompagné de recommandations de bien-être.

> ⚠️ **BioMirror est un outil d'auto-évaluation du bien-être quotidien — il ne constitue pas un dispositif médical et ne remplace en aucun cas l'avis d'un professionnel de santé.**

---

## 👥 L'équipe

> 📌 *Chaque membre de l'équipe est référent d'un pôle stratégique, tout en contribuant collectivement à la dimension hardware du projet, qui constitue le socle commun de notre prototype.*

<table>
<tr>
<td align="center" width="33%">

### 💼 Kaoutar Boubkari
**Lead Business — Stratégie & Marché**

📧 [boubkarikaoutar1@gmail.com](#)

**Responsabilités principales :**
- Étude de marché & validation stratégique
- Analyse concurrentielle (directe & indirecte)
- Définition des personas (B2C & B2B)
- Stratégie Go-To-Market (B2B2C)
- Positionnement produit & branding
- Pitch investisseurs (vidéo VC)

**Co-responsabilité :**
- 🔧 Hardware — intégration capteurs & écran tactile

</td>
<td align="center" width="33%">

### 💰 Yahya Rmili
**Lead Business — Finance & Opérations**

📧 [rmiliyahya2@gmail.com](#)
🔗 [@RmiliYahya1](https://github.com/RmiliYahya1) — *Owner du repository*

**Responsabilités principales :**
- Business Plan financier complet
- Compte de résultat prévisionnel
- Plan de financement
- Budget de trésorerie prévisionnel
- Modèle économique (B2C + B2B)
- Cadre légal, RGPD & Loi 09-08
- Gestion du repository GitHub

**Co-responsabilité :**
- 🔧 Hardware — Edge Device (Jetson Nano / RPi)

</td>
<td align="center" width="33%">

### 🧠 Majdouline Sabri
**Lead IA & Computer Vision**

📧 [majdoulinesb1@gmail.com](#)

**Responsabilités principales :**
- Architecture du pipeline de traitement IA
- Entraînement et fine-tuning des modèles
  - ResNet18 (émotions / stress)
  - MobileNetV2 (fatigue, yeux)
  - EfficientNet-B0 (peau)
- Implémentation de l'algorithme rPPG-POS
- Constitution et préparation des datasets
- Évaluation des performances (accuracy, precision, recall, F1-score)
- Fusion pondérée des scores

**Co-responsabilité :**
- 🔧 Hardware — intégration logicielle Edge ↔ caméra
- 📱 Soutien sur l'app mobile & UX

</td>
</tr>
</table>

### 🤝 Pôle Hardware — Responsabilité partagée

L'intégration hardware du miroir BioMirror est une **responsabilité collective des trois membres de l'équipe**, chacun intervenant sur sa sous-zone :

| Sous-zone Hardware | Référent |
|--------------------|----------|
| Capteurs & écran tactile (couche matérielle) | Kaoutar |
| Edge Device & déploiement embarqué (Jetson / RPi) | Yahya |
| Intégration logicielle Edge ↔ caméra (pipeline d'acquisition) | Majdouline |

> 💡 **Note :** Cette répartition reflète les domaines de référence pour la soutenance. Dans la pratique, chaque membre contribue de manière transverse aux autres pôles, et toutes les décisions stratégiques sont prises collégialement.

---

## 🏗️ Architecture technique

### Pipeline global de traitement

```
[1] Acquisition vidéo (caméra miroir)
        ↓
[2] Détection & Alignement (MediaPipe FaceMesh)
        ↓
[3] Extraction des zones d'intérêt (visage, yeux, peau)
        ↓
[4] Analyse parallèle par modules IA :
    • Émotions / Stress    → ResNet18  (FER2013, RAF-DB, AffectNet)
    • Fatigue Globale      → MobileNetV2 (Facial Expression of Fatigue)
    • Analyse des Yeux     → MobileNetV2 (CelebA)
    • Analyse de la Peau   → EfficientNet-B0 (SD-198, CelebA)
    • Rythme Cardiaque     → rPPG-POS Algorithm (MCD-rPPG)
        ↓
[5] Fusion pondérée des scores
        ↓
[6] Génération du diagnostic bien-être personnalisé
        ↓
[7] Affichage sur miroir + synchronisation app mobile
```

### Architecture en 4 couches

| Couche | Rôle | Technologies |
|--------|------|--------------|
| **1. Matérielle (Mirror)** | Capture, affichage, interaction | Caméra RGB HD, capteur IR, micro, écran tactile, Jetson Nano / RPi |
| **2. Traitement Local (Edge)** | Pré-traitement et inférence légère | OpenCV, MediaPipe, modèles légers ONNX |
| **3. Traitement Cloud** | Modèles lourds, fusion, recommandations | Serveur IA (PyTorch), base sécurisée |
| **4. Application Mobile** | Suivi, historique, recommandations | Android (Kotlin), Room DB |

### Sécurité & Confidentialité (Privacy-by-Design)

- 🔐 **Edge AI prioritaire** : aucune image faciale brute ne quitte le miroir
- 🔐 Chiffrement des données en transit (TLS) et au repos (AES)
- 🔐 Anonymisation des résultats stockés
- 🔐 Consentement utilisateur explicite à l'onboarding
- 🔐 Conformité native **RGPD** (UE) et **Loi 09-08** (Maroc)

---

## 📁 Structure du repository

> ⚠️ **Statut actuel :** le repository est en phase de structuration. La majorité des dossiers seront populés au fur et à mesure de l'avancée du POC. La structure cible est documentée ci-dessous.

```
Bio_Mirror/
│
├── README.md                       # Ce fichier
├── LICENSE
├── .gitignore
│
├── docs/                           # 📚 Documentation projet
│   ├── Etude_de_Marche.pdf
│   ├── Modele_Economique.pdf
│   ├── Business_Plan.pdf           # (à venir)
│   ├── Pipeline_Architecture.png
│   └── Pitch_Deck.pdf              # (à venir)
│
├── ai_models/                      # 🧠 Modèles IA & entraînement
│   ├── emotion_stress/             # ResNet18
│   ├── fatigue/                    # MobileNetV2
│   ├── eye_analysis/               # MobileNetV2
│   ├── skin_analysis/              # EfficientNet-B0
│   ├── rppg/                       # Algorithme rPPG-POS
│   ├── datasets/                   # Scripts de préparation
│   └── notebooks/                  # Notebooks d'expérimentation
│
├── edge/                           # ⚡ Code embarqué (Jetson / RPi)
│   ├── capture/                    # Acquisition vidéo
│   ├── preprocessing/              # MediaPipe, alignement
│   ├── inference/                  # Inférence locale (ONNX)
│   └── display/                    # Interface miroir
│
├── backend/                        # ☁️ Serveur Cloud (FastAPI)
│   ├── api/
│   ├── models/
│   ├── database/
│   └── security/
│
├── mobile/                         # 📱 Application Android (Kotlin)
│   ├── app/
│   └── ...
│
├── tests/                          # 🧪 Tests unitaires & intégration
│
└── deploy/                         # 🚀 Docker, Kubernetes, CI/CD
    ├── docker/
    └── k8s/
```

---

## 🛠️ Technologies utilisées

### Intelligence Artificielle & Computer Vision
- **Python 3.10+**
- **PyTorch** — entraînement des modèles
- **TensorFlow / TFLite** — déploiement embarqué
- **OpenCV** — traitement d'image
- **MediaPipe** — détection des landmarks faciaux
- **ONNX Runtime** — inférence optimisée sur Edge

### Backend & Cloud
- **FastAPI** — API REST
- **PostgreSQL** — base de données
- **Docker & Kubernetes** — déploiement et orchestration

### Mobile
- **Kotlin** — développement Android
- **Room DB** — stockage local

### Edge Hardware
- **NVIDIA Jetson Nano** *ou* **Raspberry Pi 4**
- Caméra RGB HD + capteur IR optionnel

### Datasets
- FER2013, RAF-DB, AffectNet (émotions)
- Facial Expression of Fatigue (fatigue)
- CelebA (yeux, peau)
- SD-198 (analyse cutanée)
- MCD-rPPG (rythme cardiaque)
- Dataset propriétaire BioMirror (en constitution)

---

## ⚙️ Installation & Lancement

> ⚠️ **En cours de développement.** 

### Prérequis
- Python 3.10 ou supérieur
- Git
- (Optionnel) Docker & Docker Compose
- (Pour l'Edge) Jetson Nano ou Raspberry Pi 4 avec Ubuntu 22.04

### Installation

```bash
# 1. Cloner le repository
git clone https://github.com/RmiliYahya1/Bio_Mirror.git
cd Bio_Mirror

# 2. Créer un environnement virtuel Python
python -m venv venv
source venv/bin/activate     # Linux / macOS
# venv\Scripts\activate       # Windows

# 3. Installer les dépendances
pip install -r requirements.txt

# 4. Télécharger les poids des modèles pré-entraînés
python scripts/download_models.py
```

### Lancement du POC

```bash
# Démarrer le pipeline d'inférence en local (mode démo webcam)
python edge/main.py --mode demo --source webcam

# Démarrer le backend API
cd backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000

# Lancer l'application mobile (Android Studio requis)
cd mobile
./gradlew assembleDebug
```

### Lancement avec Docker

```bash
docker-compose up --build
```

---

## ✨ Points forts du POC

### 1. **Zéro friction d'usage**
Le POC démontre une intégration totalement passive à la routine matinale : aucun bouton à appuyer, aucune action à initier. La simple présence du visage devant le miroir déclenche l'analyse.

### 2. **Privacy-by-Design**
L'inférence des modèles légers (détection visage, alignement, extraction ROI) s'effectue **intégralement sur l'Edge Device**. Aucune image faciale brute ne transite vers le Cloud — seules les métriques anonymisées sont synchronisées.

### 3. **Approche multi-signaux holistique**
Croisement simultané de **3 biomarqueurs visuels** (peau, yeux, micro-expressions) + 1 signal physiologique (rPPG), produisant un indicateur de vitalité unique sur le marché.

### 4. **Constance environnementale**
Conditions d'analyse identiques à chaque utilisation grâce à un éclairage LED calibré (5500K) et une distance fixe — supériorité hardware par rapport aux applications smartphone.

### 5. **Positionnement légal solide**
Outil d'auto-évaluation du bien-être (non-médical) — lexique produit, disclaimers et CGU rigoureusement structurés pour éviter toute requalification au titre du règlement EU 2017/745 (MDR).

### 6. **Architecture modulaire et évolutive**
Chaque module IA est indépendant, permettant de mettre à jour, remplacer ou enrichir un seul composant sans impacter le reste du pipeline.

---

## 🚧 Axes d'amélioration & Perspectives

### Limitations connues du POC actuel

| Limitation | Description | Pistes de mitigation |
|------------|-------------|----------------------|
| **Sensibilité à l'éclairage** | Variations de luminosité ambiante peuvent fausser l'analyse cutanée et oculaire | Calibration LED 5500K systématique, normalisation logicielle |
| **Robustesse rPPG** | Les mouvements importants du visage perturbent l'extraction du signal cardiaque | Filtrage temporel adaptatif, fenêtres glissantes |
| **Datasets limités pour l'hydratation** | Peu de datasets publics labellisés sur l'hydratation cutanée | Collecte propriétaire avec consentement, partenariats académiques |
| **Biais algorithmiques potentiels** | Risque de précision inférieure sur les phototypes IV-VI | Augmentation des datasets équilibrés (Fitzpatrick17k), audit de biais |
| **Non-certifié dispositif médical** | Ne peut pas (et ne souhaite pas) émettre d'alerte médicale | Positionnement bien-être assumé, disclaimers à 3 niveaux |

### Perspectives d'évolution

#### Court terme (6-12 mois)
- [ ] Industrialisation du prototype hardware
- [ ] Optimisation des modèles pour inférence < 200ms sur Jetson Nano
- [ ] Tests utilisateurs sur 50+ profils variés
- [ ] Premier pilote B2B en hôtellerie de luxe

#### Moyen terme (1-2 ans)
- [ ] Module **AgeTech** pour seniors autonomes
- [ ] Intégration vocale (assistant bien-être)
- [ ] Recommandations adaptatives par apprentissage continu
- [ ] Extension à 3 nouveaux marchés (UAE, Espagne, Suisse)

#### Long terme (2-3+ ans)
- [ ] Démocratisation grand public via baisse des coûts
- [ ] Partenariats avec marques cosmétiques (sans conflit d'intérêt)
- [ ] Module Corporate Wellness pour entreprises (QVT)
- [ ] Recherche académique : publication des résultats anonymisés

---

## 📚 Documents & Livrables

| Document | Statut | Lien |
|----------|--------|------|
| 📄 Étude de Marché & Validation Stratégique | ✅ Disponible | [Voir le PDF](./docs/Etude_de_Marche.pdf) |
| 💰 Modèle Économique | ✅ Disponible | [Voir le PDF](./docs/Modele_Economique.pdf) |
| 📊 Business Plan complet | 🚧 En cours | *(À venir)* |
| 🎬 Vidéo de pitch (12 min) | 🚧 En cours | *(À venir)* |
| 🖼️ Pitch Deck | 🚧 En cours | *(À venir)* |
| 🏗️ Schéma d'architecture technique | ✅ Disponible | [Voir l'image](./docs/Pipeline_Architecture.png) |

---

## ⚖️ Cadre légal & Éthique

BioMirror est rigoureusement positionné comme un **outil d'auto-évaluation du bien-être quotidien**, hors du périmètre du Règlement Européen EU 2017/745 (MDR — Medical Device Regulation).

### Engagements éthiques
- 🚫 BioMirror **ne diagnostique pas** de maladie
- 🚫 BioMirror **ne prescrit pas** de traitement
- 🚫 BioMirror **ne stocke pas** d'images faciales dans le Cloud
- 🚫 BioMirror **ne vend pas** de produits cosmétiques (intégrité algorithmique)
- ✅ Conformité **RGPD** et **Loi 09-08** (Maroc)
- ✅ Disclaimers structurés sur 3 niveaux (onboarding, contextuel, CGU/CGV)
- ✅ Consentement utilisateur explicite et révocable

> 📖 Pour plus de détails, consulter la section *"Positionnement Légal de BioMirror"* dans [l'étude stratégique](./docs/Etude_de_Marche.pdf).

---

## 🎓 Contexte académique

**Projet de Fin d'Études (PFE)** — Année universitaire 2025/2026

**Encadrants :** Michel Buffa, Nathalie Sauvage

**Évaluation finale :** Mi-juin 2026 — Session Q&A sur la base de la vidéo de pitch, du Business Plan et du POC.

---

## 📬 Contact

Pour toute question concernant le projet BioMirror :

- 🌐 **Repository GitHub :** [github.com/RmiliYahya1/Bio_Mirror](https://github.com/RmiliYahya1/Bio_Mirror)
- 📧 **Kaoutar Boubkari :** [boubkarikaoutar1@gmail.com](mailto:boubkarikaoutar1@gmail.com)
- 📧 **Yahya Rmili :** [rmiliyahya2@gmail.com](mailto:rmiliyahya2@gmail.com)
- 📧 **Majdouline Sabri :** [majdoulinesb1@gmail.com](mailto:majdoulinesb1@gmail.com)

---

<div align="center">

**🪞 BioMirror — La clarté avant la journée.**

*Made with ❤️ by Yahya, Kaoutar & Majdouline*

</div>
