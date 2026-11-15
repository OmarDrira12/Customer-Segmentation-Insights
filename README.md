# 🛒 Segmentation Non Supervisée des Clients E-Commerce (2026)

> **Qui sont vraiment mes clients ?** Découverte de profils comportementaux cachés grâce au clustering, à la réduction de dimension et à la détection d'anomalies, puis traduction en recommandations marketing actionnables.

![Python](https://img.shields.io/badge/Python-3.11-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-unsupervised-orange) ![Status](https://img.shields.io/badge/status-en%20cours-yellow)

---

## 📌 Contexte & problématique

Une plateforme e-commerce dispose de milliers de clients, mais traiter tout le monde de la même façon gaspille du budget marketing et passe à côté des clients à forte valeur.

**Question métier :** *peut-on identifier, sans aucune étiquette, des groupes de clients au comportement homogène, et comment agir différemment sur chacun ?*

**Objectifs :**
1. Segmenter la base clients (clustering).
2. Visualiser et interpréter les segments (réduction de dimension).
3. Détecter les comportements atypiques (fraude potentielle, clients VIP, churn silencieux).
4. Proposer une stratégie marketing par segment.

## 📂 Données

- **Source :** [E-Commerce Customer Behavior Dataset 2026](https://www.kaggle.com/datasets/datascikhan/e-commerce-customer-behavior-dataset-2026) (Kaggle, auteur : `datascikhan`)
- **Taille :** `[À COMPLÉTER : n lignes × n colonnes]`
- **Variables clés :** `[À COMPLÉTER : ex. âge, dépenses, fréquence d'achat, panier moyen, catégories, retours, canal, satisfaction…]`
- **Licence :** `[À COMPLÉTER depuis la page Kaggle]`

> ⚠️ Les données ne sont pas versionnées dans ce dépôt. Télécharge-les depuis Kaggle et place le CSV dans `data/raw/`.

## 🧭 Méthodologie

```
Données brutes → Nettoyage → Feature engineering → Standardisation
      → Réduction de dimension (PCA / UMAP) → Clustering → Validation
      → Profilage des segments → Détection d'anomalies → Recommandations
```

### 1. Exploration & nettoyage
- Valeurs manquantes, doublons, types, outliers
- Distributions, corrélations, déséquilibres

### 2. Feature engineering (le cœur de la valeur ajoutée)
- Variables **RFM** si les dates sont disponibles : Récence, Fréquence, Montant
- Ratios : panier moyen, taux de retour, part de remise utilisée
- Encodage des catégorielles (one-hot / target-free), transformation log des variables asymétriques
- Standardisation (`StandardScaler` ou `RobustScaler`)

### 3. Réduction de dimension
| Méthode | Usage |
|---|---|
| PCA | Variance expliquée, décorrélation avant clustering |
| t-SNE / UMAP | Visualisation 2D des segments |

### 4. Clustering (comparaison de plusieurs algorithmes)
| Algorithme | Pourquoi |
|---|---|
| K-Means | Baseline rapide et interprétable |
| Gaussian Mixture | Appartenance probabiliste, clusters elliptiques |
| Clustering hiérarchique | Dendrogramme, structure imbriquée |
| DBSCAN / HDBSCAN | Clusters de forme libre + détection du bruit |

**Choix du nombre de clusters :** méthode du coude, score de silhouette, Davies-Bouldin, Calinski-Harabasz, BIC/AIC (GMM), et **stabilité** par ré-échantillonnage (bootstrap + indice de Rand ajusté).

### 5. Détection d'anomalies
Isolation Forest, Local Outlier Factor et distance de Mahalanobis pour repérer les clients atypiques.

### 6. Profilage & interprétation
- Moyennes/médianes par segment, radar charts, heatmaps
- Nom parlant par segment (ex. « Chasseurs de promos », « Fidèles premium », « Dormants »)
- Arbre de décision peu profond *uniquement pour expliquer* les clusters (pas pour prédire)

## 📊 Résultats

> `[À COMPLÉTER après les analyses]`

| Segment | Taille | Caractéristiques | Action recommandée |
|---|---|---|---|
| Segment 1 | x % | … | … |
| Segment 2 | x % | … | … |
| Segment 3 | x % | … | … |

**Métriques retenues :** silhouette = `…`, Davies-Bouldin = `…`, k optimal = `…`

**Insights clés :**
- `[ex. 18 % des clients génèrent 52 % du chiffre d'affaires]`
- `[ex. un segment à forte activité mais fort taux de retour]`

## 💡 Recommandations business
- 🎯 **Ciblage :** campagnes différenciées par segment
- 🔁 **Rétention :** relance des segments à risque avant le churn
- 💎 **Montée en gamme :** offres de cross-sell pour les segments à fort potentiel
- 🚨 **Contrôle :** revue des anomalies détectées

## 🗂️ Structure du projet

```
.
├── data/
│   ├── raw/              # CSV Kaggle (non versionné)
│   └── processed/
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_feature_engineering.ipynb
│   ├── 03_dimensionality_reduction.ipynb
│   ├── 04_clustering.ipynb
│   ├── 05_anomaly_detection.ipynb
│   └── 06_segment_profiling.ipynb
├── src/                  # fonctions réutilisables
├── reports/figures/
├── requirements.txt
└── README.md
```

## 🚀 Installation & exécution

```bash
git clone https://github.com/<ton-user>/<ton-repo>.git
cd <ton-repo>
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt

# Téléchargement des données (API Kaggle configurée)
kaggle datasets download -d datascikhan/e-commerce-customer-behavior-dataset-2026 -p data/raw --unzip

jupyter lab
```

**requirements.txt (suggestion) :** `pandas numpy scikit-learn matplotlib seaborn plotly umap-learn hdbscan scipy jupyterlab`

## 🛠️ Stack
Python · pandas · scikit-learn · UMAP · HDBSCAN · Plotly · Jupyter

## ⚖️ Limites & pistes d'amélioration
- Le clustering dépend fortement des variables choisies et de leur échelle
- Vérifier si les données sont synthétiques : les segments peuvent être moins marqués qu'en réel
- Pistes : clustering de séquences d'achats, modèle de CLV par segment, application Streamlit pour explorer les segments, A/B test des actions marketing

## 👤 Auteur
**[Ton Nom]** · [LinkedIn](https://linkedin.com/in/...) · [Portfolio](https://...)

---
*Projet réalisé à des fins pédagogiques et de portfolio.*
