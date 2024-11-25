# Prédiction de Prix de l'Électricité – Challenge Data

Nous avons participer au challenge data **Prédiction de prix de l'électricité** organisé par **Elmy**. Ce projet vise à modéliser l'écart de prix entre deux marchés de l'électricité : le marché SPOT et le marché Intraday.

---

## 🎯 **Objectif du Projet**
Le but est de développer un modèle de machine learning supervisé capable de prédire le sens de l'écart de prix entre :
- Le **marché SPOT** : marché européen d'enchères permettant d'acheter de l'électricité la veille pour le lendemain.
- Le **marché Intraday** : marché européen boursier permettant d'acheter de l'électricité le jour même.

### Approches possibles :
1. **Régression** : Modéliser l'écart exact entre les deux prix.
2. **Classification** : Identifier si le prix Intraday sera supérieur ou inférieur au prix SPOT.

L'objectif principal est de prédire correctement le **sens de cet écart**.

---

## 📂 **Structure des Données**

### Index :
- `DELIVERY_START` : Date et heure de livraison de l'électricité.

### Variables explicatives :
- `load_forecast` : Prévision de consommation totale d'électricité en France.
- `coal_power_available`, `gas_power_available`, `nuclear_power_available` : Capacité totale de production d'électricité des centrales à charbon, gaz et nucléaire.
- `wind_power_forecasts_average`, `solar_power_forecasts_average` : Moyenne des prévisions de production d'électricité éolienne et solaire.
- `wind_power_forecasts_std`, `solar_power_forecasts_std` : Écart-type de ces prévisions.
- `predicted_spot_price` : Prévision du prix SPOT issue d’un modèle interne.

### Variable cible :
- `spot_id_delta` : Écart entre le VWAP des transactions sur le marché Intraday et le prix SPOT. 
  - **Positive** : Prix Intraday supérieur au prix SPOT.
  - **Négative** : Prix Intraday inférieur au prix SPOT.

---

## 📈 **Évaluation des Modèles**

La performance sera mesurée par la **Weighted Accuracy** :
- **Weighted Accuracy** = Proportion des prédictions correctes sur le sens (positif/négatif) de l'écart, pondérée par la valeur absolue des écarts observés.
- Plus l'écart est important, plus il est crucial de prédire correctement son sens.

---

## 🛠️ **Benchmark**

Un benchmark simple consiste à prédire que les prix sur le marché Intraday sont **toujours supérieurs** aux prix du marché SPOT. Historiquement, cette hypothèse est valable dans la majorité des cas.

---

## 📦 **Fichiers**

1. **Données d'entraînement :**
   - `x_train.csv` : Variables explicatives pour l’entraînement.
   - `y_train.csv` : Variable cible pour l’entraînement.

2. **Données de test :**
   - `x_test.csv` : Variables explicatives pour le test.

3. **Exemple de soumission :**
   - `example_submission.csv` : Exemple de soumission aléatoire.

---

## 🚀 **Contributions**

Vous êtes invités à contribuer à ce projet en :
- Explorant de nouvelles approches de modélisation (régressions, classifications, algorithmes avancés).
- Partageant des idées ou des insights dans les issues de ce dépôt.
  
---

## 🤝 **Remerciements**

Merci à **Elmy** et à **Challenge Data** pour l'organisation de ce projet. Ce challenge est une opportunité exceptionnelle de travailler sur des données réelles et d’apporter des solutions concrètes à des problématiques industrielles.
