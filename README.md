                                  Comparaison CNN From Scratch vs Transfer Learning – Chats vs Chiens

# Objectif

Ce projet compare deux approches de classification d’images sur le dataset **Cats vs Dogs** :

#1. CNN from scratch : architecture personnalisée (4 blocs convolutifs + BatchNorm + Dropout).
#2. Transfer learning : ResNet18 pré‑entraîné sur ImageNet, fine‑tuné sur notre dataset.

L’objectif est de mesurer l’impact du transfert d’apprentissage sur la convergence ,les performances (accuracy, précision, rappel) et la robustesse face à un petit jeu de données.

# Organisation des données
Cat_Dog_data/
├── train/
│   ├── cat/      # images de chats
│   └── dog/      # images de chiens
└── test/
    ├── cat/
    └── dog/ 
Les données sont aussi disponibles sur Kaggle

# Hyperparamètres importants :

Batch size : 32

Learning rate : 0.001 (Adam) ou 0.01 (SGD)

Epochs : 15

Dropout : Dropout2d(0.25) après chaque bloc conv, Dropout(0.5) puis Dropout(0.3) dans le classifieur.

Batch Normalization : après chaque convolution, avant ReLU.

Scheduler : StepLR (réduction par 10 tous les 5 epochs)

# Particularités du transfer learning :

Base pré‑entraînée : ResNet18 (ImageNet)

Fine‑tuning partiel : seules les couches layer4 et la tête sont entraînées (les autres sont gelées).

Learning rate réduit : 1e-4 (Adam) ou 1e-3 (SGD) pour ne pas dégrader les caractéristiques.

#Évaluation 
Les meilleurs modèles sont automatiquement sauvegardés sous forme de fichiers .pth (dans le répertoire courant ou sur Google Drive).

#Limites & pistes d’amélioration
Limites actuelles
Dataset modeste : quelques centaines d’images par classe (selon la version téléchargée). Les résultats pourraient encore s’améliorer avec plus de données.

Augmentation limitée : seuls flip horizontal et variations de couleurs. D’autres techniques (rotation, zoom, cutout) pourraient réduire le surapprentissage.

Architecture from scratch simple : pas de blocs résiduels ni de connexions skip. Une architecture plus profonde (ex. 6 blocs) pourrait améliorer les performances, au prix de la complexité.
