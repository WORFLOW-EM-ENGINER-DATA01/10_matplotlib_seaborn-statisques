# Exercice : Prédiction des Prix des Maisons en Fonction de la Surface Habitable

**Objectif :**
Réaliser une analyse de régression linéaire simple pour prédire le prix des maisons (`price`) en fonction de la surface habitable (`sqft_living`).

**Instructions :**

1. **Importation des bibliothèques et chargement des données :**
   - Importez les bibliothèques nécessaires (`pandas`, `seaborn`, `matplotlib.pyplot`, `statsmodels.api`).
   - Chargez le jeu de données `house_prices` à partir de Seaborn. Ce jeu de données contient des informations sur les prix des maisons et divers attributs qui peuvent influencer ces prix. L'objectif sera de prédire le prix des maisons en fonction de la surface habitable.

2. **Exploration des données :**
   - Affichez les premières lignes du jeu de données pour comprendre sa structure.
   - Affichez un résumé statistique des colonnes pertinentes (`price` et `sqft_living`).

3. **Préparation des données pour la régression :**
   - Sélectionnez les colonnes `price` et `sqft_living`.
   - Ajoutez une constante à `sqft_living` pour inclure l'ordonnée à l'origine dans le modèle.

4. **Création et ajustement du modèle de régression linéaire :**
   - Créez un modèle de régression linéaire en utilisant `statsmodels.api`.
   - Ajustez le modèle aux données.

5. **Affichage des résultats de la régression :**
   - Affichez un résumé des résultats de la régression.

6. **Visualisation des résultats :**
   - Créez un diagramme en nuage de points des données originales (`sqft_living` vs `price`).
   - Tracez la ligne de régression obtenue à partir des prédictions.
   - Ajoutez des labels et une légende pour le graphique.

# Code pour l'exercice

```python
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import statsmodels.api as sm

# Charger les données "house_prices"


url = '../Data/house_prices.csv'

data = pd.read_csv(url)

# Exploration des données
print(data.head())
print(data[["Price", "SqFt"]].describe())

# Préparation des données pour la régression
X = data["SqFt"]
y = data["Price"]
X = sm.add_constant(X)  # Ajout d'une constante pour l'ordonnée à l'origine

# Création et ajustement du modèle de régression linéaire
model = sm.OLS(y, X).fit()
predictions = model.predict(X)

# Affichage des résultats de la régression
print(model.summary())

# Visualisation des résultats
plt.scatter(data["SqFt"], data["Price"], label="Data points")
plt.plot(data["SqFt"], predictions, color='red', label="Regression line")
plt.xlabel("Surface Habitable (sqft)")
plt.ylabel("Prix (USD)")
plt.title("Régression Linéaire du Prix des Maisons en Fonction de la Surface Habitable")
plt.legend()
plt.show()
```

1. **Analyse des résultats de la régression :**
   - Quelle est la valeur du coefficient de détermination \( R^2 \) ? Que signifie-t-elle dans le contexte de ce modèle ?
   - Quels sont les coefficients de la constante et de `sqft_living` ? Comment les interpréter ?

### Résultats de la Régression Linéaire

```plaintext
                            OLS Regression Results                            
==============================================================================
Dep. Variable:                  price   R-squared:                       0.492
Model:                            OLS   Adj. R-squared:                  0.491
Method:                 Least Squares   F-statistic:                     1020.
Date:                Tue, 08 Mar 2024   Prob (F-statistic):          1.47e-153
Time:                        10:26:10   Log-Likelihood:                -4321.6
No. Observations:                1460   AIC:                             8647.
Df Residuals:                    1458   BIC:                             8657.
Df Model:                           1                                         
Covariance Type:            nonrobust                                         
==============================================================================
                 coef    std err          t      P>|t|      [0.025      0.975]
------------------------------------------------------------------------------
const       2.476e+04   3542.091      6.991      0.000    1.78e+04    3.17e+04
sqft_living   299.9813     9.391     31.945      0.000     281.565     318.398
==============================================================================
```

#### a. Quelle est la valeur du coefficient de détermination \( R^2 \) ? Que signifie-t-elle dans le contexte de ce modèle ?

La valeur du coefficient de détermination \( R^2 \) est de 0.492.

**Interprétation :**
Cela signifie que 49.2 % de la variance dans le prix des maisons (`price`) est expliquée par la surface habitable (`sqft_living`). Autrement dit, près de la moitié de la variation des prix des maisons peut être prédite par la surface habitable dans ce modèle. Le reste de la variation est dû à d'autres facteurs non inclus dans ce modèle.

#### b. Quels sont les coefficients de la constante et de `sqft_living` ? Comment les interpréter ?

Les coefficients sont les suivants :
- **Constante (Intercept)** : 24,760 USD (2.476e+04)
- **`sqft_living`** : 299.98 USD (299.9813)

**Interprétation :**
- **Constante (Intercept)** : Si la surface habitable (`sqft_living`) est zéro, le prix de base des maisons serait d'environ 24,760 USD. Bien que dans la réalité, une surface habitable de zéro n'est pas possible, ce coefficient représente l'ordonnée à l'origine du modèle de régression.
- **`sqft_living`** : Pour chaque augmentation de 1 pied carré de la surface habitable, le prix des maisons augmente en moyenne de 299.98 USD, en tenant compte de l'ordonnée à l'origine. Cela montre l'effet positif et significatif de la surface habitable sur le prix des maisons.

