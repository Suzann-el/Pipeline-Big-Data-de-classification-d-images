# 🍎 Fruits! — Pipeline Big Data de classification d'images

> Architecture Big Data sur AWS pour la classification d'images de fruits à grande échelle, dans une optique de montée en charge.

---

## 🎯 Contexte

Dans le cadre du développement d'une application mobile de reconnaissance de fruits, ce projet pose les fondations d'une **architecture Big Data scalable** capable de traiter un volume croissant d'images. L'enjeu n'est pas seulement la classification — c'est de construire un pipeline distributé prêt pour la production.

---

## ⚙️ Ce que fait le projet

- **Extraction de features** via un modèle **MobileNet** (transfer learning) distribué sur cluster Spark
- **Broadcast des poids** du modèle TensorFlow sur les workers PySpark (optimisation mémoire)
- **Réduction de dimension** par PCA en PySpark
- **Pipeline bout-en-bout** : ingestion S3 → traitement EMR → features prêtes pour classification
- **Conformité RGPD** : infrastructure déployée sur des serveurs en territoire européen (région AWS `eu-west`)

---

## 🛠️ Stack

| Couche | Outils |
|--------|--------|
| Big Data | `PySpark` `AWS EMR` |
| Stockage | `AWS S3` |
| Accès & sécurité | `AWS IAM` |
| Deep Learning | `TensorFlow` `MobileNet` |
| Réduction de dimension | `PCA (PySpark MLlib)` |
| Environnement | `Jupyter on EMR` |

---

## 🏗️ Architecture

```
Images (S3)
    │
    ▼
AWS EMR (cluster Spark)
    ├── Chargement des images depuis S3
    ├── Broadcast des poids MobileNet sur les workers
    ├── Extraction de features (Transfer Learning)
    └── Réduction PCA
         │
         ▼
    Features vectorisées (S3)
```

---

## 📁 Structure du projet

```
├── notebooks/
│   └── pipeline_pyspark.ipynb   # Pipeline complet commenté
├── src/
│   └── preprocessing.py         # Fonctions de traitement
└── README.md
```

---

## ⚠️ Note sur les coûts AWS

L'instance EMR a été maintenue active **uniquement pendant les phases de test et de démonstration** afin de limiter les coûts. Les scripts sont conçus pour être relancés à la demande.

---

## 📂 Données

Jeu de données d'images de fruits labelisées — [Fruits 360 sur Kaggle](https://www.kaggle.com/datasets/moltean/fruits)
