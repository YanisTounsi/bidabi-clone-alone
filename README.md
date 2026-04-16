# bidabi-clone-alone

Pipeline complet de classification d'images de produits alimentaires avec ResNet-18.

## Description

Ce projet collecte des images de produits alimentaires depuis OpenFoodFacts, entraîne un modèle de classification ResNet-18 et évalue ses performances.

## Structure du projet

- src/asyscrapper.py : collecte des données depuis OpenFoodFacts
- src/classificator.py : pipeline d'entraînement ResNet-18
- src/data_loader.py : chargement des données
- data/raw/ : dataset brut versionné avec DVC
- best_model_resnet18_finetuned.pth.dvc : modèle versionné avec DVC

## Installation

python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
pip install torch torchvision --index-url https://download.pytorch.org/whl/cpu

## Collecter les données

Dans src/asyscrapper.py, changer CATEGORY puis lancer :
python src/asyscrapper.py

## Restaurer les données avec DVC

dvc pull

## Lancer l'entraînement

python src/classificator.py

## Versions

- v1.0 : Version initiale du projet
- v2.0 : Scrapper corrigé et données RAW collectées
- v2.1 : Dataset RAW versionné avec DVC
- v3.0 : Pipeline d'entraînement ResNet-18 complet

## Auteur

YanisTounsi
