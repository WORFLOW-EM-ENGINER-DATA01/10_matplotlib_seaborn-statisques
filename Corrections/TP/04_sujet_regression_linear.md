# TP sur les Iris

##  Régression Linéaire sur le Jeu de Données des Iris

Utilisez sklearn dans ce TP

```python
from sklearn.linear_model import LinearRegression
# Création du modèle de régression linéaire
model = LinearRegression()

# Entraînement du modèle
model.fit(X, y) # X et Y sont à déterminées en fonction de vos données

# Coefficient (pente)
coefficient = model.coef_[0]

# Interception
interception = model.intercept_

print(f"Coefficient : {coefficient}")
print(f"Interception : {interception}")

# Prédictions du modèle == la droite de régression
y_pred = model.predict(X)

# Evaluation du modèle
r_squared = model.score(X, y)
print(f"Coefficient de détermination R² : {r_squared}")
```

- **Coefficient** : Le **coefficient** indique l'effet de la longueur des sépales sur la longueur des pétales. Si le coefficient est positif, cela signifie que la longueur des pétales augmente avec la longueur des sépales. Coefficient directeur de la droite dans votre modèle.
- **Interception** : L'**interception** est la valeur prédite de la longueur des pétales lorsque la longueur des sépales est zéro (l'ordonnée à l'origine).
- **Coefficient de détermination r_squared** : Cette valeur varie entre 0 et 1 et indique la proportion de la variance de la variable cible expliquée (dépendante y) par le modèle. Plus la valeur de r_squared est proche de 1, meilleur est le modèle ! 

###  Préparation du Jeu de Données

1. **Chargement et exploration des données**
   
```python
import pandas as pd
from sklearn.datasets import load_iris

# Chargement du jeu de données des iris
iris = load_iris()
iris_df = pd.DataFrame(data=iris.data, columns=iris.feature_names)
iris_df['target'] = iris.target

# Affichage des premières lignes du DataFrame
print(iris_df.head())
```

2. **Sélection des variables explicatives et cible**
    - Sélectionnez la longueur des sépales comme variable explicative (X).
    - Sélectionnez la longueur des pétales comme variable cible (y).

## Correction 

```python
# Sélection des variables explicative (X) et cible (y)
X = iris_df[['sepal length (cm)']].values  # Longueur des sépales comme variable explicative (indépendante)
y = iris_df['petal length (cm)'].values    # Longueur des pétales comme variable cible (dépendante)
```

### Modélisation - regression linéaire 

1. **Création et entraînement du modèle de régression linéaire**
    - Importez la classe `LinearRegression` de `sklearn.linear_model`.
    - Créez une instance de `LinearRegression` et entraînez le modèle sur les données.

## Correction

```python
from sklearn.linear_model import LinearRegression

# Création et entraînement du modèle de régression linéaire
model = LinearRegression()
model.fit(X, y)
```

2. **Affichage des coefficients appris par le modèle**
    - Affichez le coefficient et l'interception du modèle.

## Correction

```python
# Affichage des coefficients appris par le modèle
print(f"Coefficient : {model.coef_[0]}")
print(f"Interception : {model.intercept_}")
```

3. **Analyse des coefficients et interprétation**
    - Expliquez ce que représentent le coefficient et l'interception dans le contexte du jeu de données des iris.

#### Correction

- Le **coefficient** (ou pente) dans le contexte du jeu de données des iris représente le changement attendu dans la longueur des pétales (variable dépendante) pour chaque unité de changement dans la longueur des sépales (variable indépendante). Autrement dit, il indique la relation linéaire entre ces deux mesures.

- L'**interception** est la valeur de la longueur des pétales lorsque la longueur des sépales est égale à zéro. C'est un point théorique, car dans le contexte des iris, la longueur des sépales ne peut pas être zéro.

4. Interprétez les résultats obtenus en termes de relation entre la longueur des sépales et la longueur des pétales.

#### Correction

Si le coefficient est positif => à mesure que la longueur des sépales augmente, la longueur des pétales tend à augmenter également.
Si le coefficient est élevé, => un impact significatif sur la longueur des pétales. Un coefficient faible indiquerait une relation plus faible.

L'interception => est une partie théorique (ordonnée à l'origine de la droite) de l'équation de la droite de régression.

5. Que représente le coefficient dans une régression linéaire ?

#### Correction

Si le coefficient est positif, cela signifie qu'il y a une relation positive entre la longueur des sépales et la longueur des pétales : à mesure que la longueur des sépales augmente, la longueur des pétales tend à augmenter également.

6. En utilisant les coefficients obtenus, écrivez l'équation de la droite de régression.

y= 1.8584329782548412⋅x - 7.101443369602455

```python
print(f"Coefficient : {model.coef_[0]}") #  1.8584329782548412
print(f"Interception : {model.intercept_}") # - 7.101443369602455
```

#### Correction

Le coefficient dans une régression linéaire représente la pente de la droite de régression. Il indique combien la variable dépendante (y) change pour une unité de changement dans la variable indépendante (x). En d'autres termes, c'est le taux de changement de y par rapport à x.

7. **Visualisation**
    - Tracez un graphique de la longueur des sépales en fonction de la longueur des pétales.
    - Ajoutez la droite de régression au graphique pour visualiser l'ajustement du modèle.

#### Correction - visualisation

```python
import matplotlib.pyplot as plt

# Prédictions du modèle
y_pred = model.predict(X)

# Création du graphique
plt.scatter(X, Y, color='blue', label='Données réelles')
plt.plot(X, y_pred, color='red', label='Droite de régression')
plt.xlabel('Longueur des sépales (cm)')
plt.ylabel('Longueur des pétales (cm)')
plt.title('Régression linéaire simple sur le jeu de données des iris')
plt.legend()
plt.show()
```

8. **Évaluation du modèle**
    - Calculez le coefficient de détermination R² pour évaluer la performance du modèle.

## Correction

```python
# Évaluation du modèle
r_squared = model.score(X, y)
print(f"Coefficient de détermination R² : {r_squared}")
```