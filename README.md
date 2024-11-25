# Prévision du prix des Marchés Électriques

**Auteurs :** Arthur Frachon - Jeanne Collot  
**Challenge Data :** [Enoncé](https://challengedata.ens.fr/challenges/140)  


## 1) Sujet

**Contexte :** Elmy, producteur et fournisseur d'électricité, souhaite prévoir si les prix de l'électricité sur le marché Intraday seront supérieurs ou inférieurs à ceux du marché SPOT. L'objectif est de modéliser l'écart de prix (spot_id_delta) en utilisant une classification supervisée.

**Métrique :** Weighted Accuracy (pondération par la magnitude des écarts observés).

---

## 2) Données

- **Index :** `DELIVERY_START` (date et heure de livraison).  
- **Features principales :**
  - Prévisions de charge (`load_forecast`), capacité des centrales (charbon, gaz, nucléaire).  
  - Moyennes et écarts-types des prévisions d'énergie renouvelable (solaire, éolien).  
  - Prix SPOT prédit (`predicted_spot_price`).

- **Cible :** `spot_id_delta` = Intraday - SPOT.

---

## 3) Problématique

Prédire si `spot_id_delta` est positif ou négatif via des modèles de classification.

---

## 4) Préparation et Exploration des Données

### 4.1) Nettoyage
- Gestion des valeurs manquantes via imputation ou suppression.
- Ajout de nouvelles features basées sur des décalages temporels (par exemple, prix SPOT à l'heure précédente).

### 4.2) Normalisation
- Normalisation des features numériques avec `StandardScaler`.

### 4.3) Analyse
- Matrices de corrélation montrant une forte dépendance entre `spot_id_delta` et `predicted_spot_price`.

---

## 5) Méthodes Explorées

### 5.1) Benchmark
- Une régression logistique simple est utilisée comme référence, avec une Weighted Accuracy de **0.643**.

### 5.2) Modèles Non Supervisés
- **ACP :** Réduction dimensionnelle pour visualisation et analyse.  
- **KMeans :** Clustering avec ajout de features basées sur les moyennes des clusters. Weighted Accuracy : **0.739**.

### 5.3) Modèles Supervisés
- **Random Forest Classifier :** Modèle de classification atteignant une Weighted Accuracy de **0.814** après optimisation.

### 5.4) Deep Learning
- **Réseaux de Neurones Standards :** Performances modérées (~0.643 Weighted Accuracy).  
- **LSTM :** Utilisation pour capter les relations temporelles, mais résultats encore limités (0.421).

---

## 6) Résultats

| Modèle                   | Méthode         | Weighted Accuracy |
|--------------------------|-----------------|--------------------|
| Logistic Regression      | Baseline        | 0.643             |
| KMeans                   | Mean Clusters   | 0.739             |
| Random Forest Classifier | Clusters        | **0.814**         |
| Random Forest Regressor  | Standard        | **0.874**         |
| LSTM                     | Standard        | 0.421             |

---

## 7) Conclusion

- Les modèles supervisés (notamment Random Forest) surpassent les approches non supervisées et Deep Learning.
- L'ajout de features via clustering améliore la précision.
- Les données nécessitent davantage de signaux explicatifs pour exploiter pleinement le potentiel des méthodes avancées.
