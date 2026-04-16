# bidabi-clone-alone

Pipeline complet de collecte, entraînement et évaluation d'un modèle de classification d'images alimentaires basé sur ResNet-18.

## Description

Ce projet réalise trois grandes étapes :
1. Collecte automatique d'images de produits alimentaires via l'API OpenFoodFacts
2. Entraînement d'un modèle ResNet-18 avec fine-tuning complet
3. Évaluation approfondie avec métriques, courbes ROC et visualisations

## Prérequis

- Python 3.12
- Windows 10/11
- Git
- DVC

## Structure du projet

- src/asyscrapper.py : scrapper asynchrone pour collecter les images
- src/classificator.py : pipeline complet d'entraînement ResNet-18
- src/data_loader.py : chargement et prétraitement des données
- data/raw/images/ : images brutes organisées par catégorie
- data/raw/*.csv : métadonnées des produits collectés
- best_model_resnet18_finetuned.pth.dvc : modèle entraîné versionné avec DVC
- requirements.txt : dépendances Python

## Installation

1. Cloner le projet :
git clone https://github.com/YanisTounsi/bidabi-clone-alone.git
cd bidabi-clone-alone

2. Créer et activer l'environnement virtuel :
python -m venv .venv
.venv\Scripts\activate

3. Installer les dépendances :
pip install -r requirements.txt
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu
pip install dvc

4. Restaurer les données et le modèle :
dvc pull

## Collecter de nouvelles données

Dans src/asyscrapper.py, modifier la variable CATEGORY :
CATEGORY = "milk"  # ou "bread", "butter", "sugar"

Puis lancer :
python src/asyscrapper.py

## Lancer l'entraînement

python src/classificator.py

## Détails du modèle

- Architecture : ResNet-18 avec fine-tuning complet
- Taille des images : 256x256
- Batch size : 32
- Epochs max : 20 avec early stopping (patience=3)
- Optimiseur : Adam (lr=1e-5, weight_decay=1e-4)
- Augmentations : MixUp, rotation, flip, ColorJitter, GaussianBlur
- Séparation : 60% train / 20% val / 20% test

## Métriques d'évaluation

- Courbe de loss train/val
- Accuracy par epoch
- Matrice de confusion
- Courbes ROC par classe
- Accuracy par classe
- Visualisation t-SNE des embeddings

## Versionnement des données avec DVC

Les données et le modèle sont versionnés avec DVC :
dvc add data/raw
dvc add best_model_resnet18_finetuned.pth
dvc push

## Historique des versions

- v1.0 : Version initiale — sparse checkout et nouveau dépôt
- v2.0 : Scrapper corrigé — données RAW collectées pour milk
- v2.1 : Dataset RAW versionné avec DVC
- v3.0 : Pipeline d'entraînement ResNet-18 complet avec DVC

## Auteur

YanisTounsi
