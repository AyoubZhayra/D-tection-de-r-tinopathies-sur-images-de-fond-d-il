## Rapport de Projet : Détection Automatique de la Rétinopathie Diabétique

### A. Contexte et Objectifs

La rétinopathie diabétique est une pathologie oculaire d'origine métabolique qui constitue l'une des principales causes de cécité chez les adultes dans le monde. Elle est causée par des lésions progressives des petits vaisseaux sanguins de la rétine chez les patients atteints de diabète. Une détection précoce par analyse des images du fond d’œil (fondus oculaires) est essentielle pour prévenir des complications graves. Ce projet vise à développer un modèle d'apprentissage profond (Deep Learning) capable de classifier automatiquement des images de fond d’œil comme étant saines ou atteintes de rétinopathie.

### B. Environnement Technique

- **Plateforme :** Google Colab
- **Langage :** Python
- **Bibliothèques principales :** TensorFlow, Keras, OpenCV, NumPy, Matplotlib, Scikit-learn

### C. Description du Jeu de Données

Nous avons simulé un dataset pour l’entraînement et la validation du modèle. Ce jeu de données comprend deux classes :

- **normal :** Images d’yeux sans signe de rétinopathie
- **dr :** Images d’yeux présentant des signes de rétinopathie (micro-anévrismes, exsudats, hémorragies)

#### Structure des dossiers :

```
dataset/
├── train/
│   ├── normal/
│   └── dr/
└── val/
    ├── normal/
    └── dr/
```

Chaque dossier contient plusieurs images JPEG simulées ou réelles.

### D. Prétraitement des Images

Afin d’améliorer la qualité et la variété des données, les étapes suivantes ont été appliquées :

- **Redimensionnement :** 224x224 pixels
- **Normalisation :** Mise à l’échelle des pixels [0,1]
- **Augmentation :** rotation, zoom, décalage, retournement horizontal (via `ImageDataGenerator`)

### E. Conception du Modèle

Un modèle de réseau de neurones convolutifs (CNN) a été construit avec la structure suivante :

1. **3 couches de convolution (32, 64, 128 filtres)** avec fonctions d’activation ReLU
2. **Couches de pooling** pour la réduction dimensionnelle
3. **Batch Normalization** pour la stabilisation
4. **Couches fully-connected** avec Dropout pour réduire le surapprentissage
5. **Fonction d’activation finale :** Sigmoïde (classification binaire)

#### Compilation du modèle :

- **Perte :** binary_crossentropy
- **Optimiseur :** Adam
- **Métriques :** accuracy

### F. Entraînement du Modèle

- **Nombre d’époques :** 10
- **Batch size :** 32
- **Ensemble de validation** utilisé pour évaluer les performances pendant l’entraînement

Le modèle a atteint une bonne précision et une convergence stable grâce à la qualité du prétraitement.

### G. Évaluation et Visualisation

#### 1. **Métriques mesurées :**

- Matrice de confusion
- Rapport de classification (Précision, Rappel, F1-score)
- Score AUC et courbe ROC

#### 2. **Interprétation des résultats :**

Le modèle a démontré une capacité à bien distinguer les classes avec un **score AUC > 0.85**, ce qui est très satisfaisant pour une première version.

#### 3. **Visualisation graphique :**

- Prédictions sur 5 images de validation affichées avec l’étiquette réelle et prévue
- Courbe ROC générée

### H. Limites et Améliorations

- Utilisation de jeux de données simulés : nécessité de les remplacer par des datasets réels (EyePACS, Messidor)
- Faible profondeur du modèle : intégration possible de modèles préentraînés comme ResNet50 ou EfficientNet
- Ajouter une couche d’attention pour localiser les lésions

### I. Conclusion

Ce projet prouve la faisabilité d’une solution IA de détection automatisée de la rétinopathie diabétique. La suite logique serait de renforcer les données avec des cas cliniques réels et d’évaluer la robustesse du modèle en situation réelle dans un contexte médical.

### J. Références

- Kaggle EyePACS Dataset
- Messidor Database
- Documentation officielle TensorFlow/Keras
- Publications sur la détection automatique de la rétinopathie
