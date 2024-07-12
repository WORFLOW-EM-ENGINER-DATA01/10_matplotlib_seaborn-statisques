# Exercice : Prédiction des Prix des Maisons en Fonction de la Surface Habitable

**Objectif :**
Réaliser une analyse de régression linéaire simple pour prédire le prix des maisons (`Price`) en fonction de la surface habitable (`SqFt`).

**Instructions :**

1. **Importation des bibliothèques et chargement des données :**
   - Importez les bibliothèques nécessaires (`pandas`, `seaborn`, `matplotlib.pyplot`, `statsmodels.api`).
   - Chargez le jeu de données `house_prices` à partir de Seaborn. Ce jeu de données contient des informations sur les prix des maisons et divers attributs qui peuvent influencer ces prix. L'objectif sera de prédire le prix des maisons en fonction de la surface habitable.

2. **Exploration des données :**
   - Affichez les premières lignes du jeu de données pour comprendre sa structure.
   - Affichez un résumé statistique des colonnes pertinentes (`Price` et `SqFt`).

3. **Préparation des données pour la régression :**
   - Sélectionnez les colonnes `Price` et `SqFt`.
   - Ajoutez une constante à `SqFt` pour inclure l'ordonnée à l'origine dans le modèle.

4. **Création et ajustement du modèle de régression linéaire :**
   - Créez un modèle de régression linéaire en utilisant `statsmodels.api`.
   - Ajustez le modèle aux données.

5. **Affichage des résultats de la régression :**
   - Affichez un résumé des résultats de la régression.

6. **Visualisation des résultats :**
   - Créez un diagramme en nuage de points des données originales (`SqFt` vs `Price`).
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

# Questions pour approfondir l'exercice :

1. **Analyse des résultats de la régression :**
   - Quelle est la valeur du coefficient de détermination \( R^2 \) ? Que signifie-t-elle dans le contexte de ce modèle ?
