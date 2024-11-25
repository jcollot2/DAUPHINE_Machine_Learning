# Prédiction de prix de l'électricité

**Auteurs :** Arthur Frachon - Jeanne Collot 
**Cadre :** Dauphine - cours de Machine Learning
**Date :** 2024
**Challenge Data :** [Enoncé](https://challengedata.ens.fr/challenges/140)  


## 📌 Sujet

**Contexte :** Elmy, producteur et fournisseur d'électricité, souhaite prévoir si les prix de l'électricité sur le marché Intraday seront supérieurs ou inférieurs à ceux du marché SPOT. L'objectif est de modéliser l'écart de prix (spot_id_delta) en utilisant une classification supervisée.

**Métrique :** Weighted Accuracy (pondération par la magnitude des écarts observés).

---

## 🔍 Données

- **Index :** `DELIVERY_START` (date et heure de livraison).  
- **Features principales :**
  - Prévisions de charge (`load_forecast`), capacité des centrales (charbon, gaz, nucléaire).  
  - Moyennes et écarts-types des prévisions d'énergie renouvelable (solaire, éolien).  
  - Prix SPOT prédit (`predicted_spot_price`).

- **Cible :** `spot_id_delta` = Intraday - SPOT.

---

## ❓Problématique

Prédire si `spot_id_delta` est positif ou négatif via des modèles de classification.

---

## 🛠️ Préparation et Exploration des Données

### 1) Nettoyage
- Gestion des valeurs manquantes via imputation ou suppression.
- Ajout de nouvelles features basées sur des décalages temporels (par exemple, prix SPOT à l'heure précédente).

### 2) Normalisation
- Normalisation des features numériques avec `StandardScaler`.

### 3) Analyse
- Matrices de corrélation montrant une forte dépendance entre `spot_id_delta` et `predicted_spot_price`.

---

## 📉 Méthodes Explorées

### 1) Benchmark
- Une régression logistique simple est utilisée comme référence, avec une Weighted Accuracy de **0.643**.

### 2) Modèles Non Supervisés
- **ACP :** Réduction dimensionnelle pour visualisation et analyse.  
- **KMeans :** Clustering avec ajout de features basées sur les moyennes des clusters. Weighted Accuracy : **0.739**.

### 3) Modèles Supervisés
- **Random Forest Classifier :** Modèle de classification atteignant une Weighted Accuracy de **0.814** après optimisation.

### 4) Deep Learning
- **Réseaux de Neurones Standards :** Performances modérées (~0.643 Weighted Accuracy).  
- **LSTM :** Utilisation pour capter les relations temporelles, mais résultats encore limités (0.421).

---

## 🏆Résultats

| Modèle                   | Méthode         | Weighted Accuracy |
|--------------------------|-----------------|--------------------|
| Logistic Regression      | Baseline        | 0.643             |
| KMeans                   | Mean Clusters   | 0.739             |
| Random Forest Classifier | Clusters        | **0.814**         |
| Random Forest Regressor  | Standard        | **0.874**         |
| LSTM                     | Standard        | 0.421             |

---

## 🎯Conclusion

- Les modèles supervisés (notamment Random Forest) surpassent les approches non supervisées et Deep Learning.
- L'ajout de features via clustering améliore la précision.
- Les données nécessitent davantage de signaux explicatifs pour exploiter pleinement le potentiel des méthodes avancées.
