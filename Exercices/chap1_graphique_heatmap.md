# Exercice sur Heatmaps : Corrélation des Températures Mensuelles

## Étape 1 : Préparation des Données

Nous allons créer un jeu de données fictif contenant les températures mensuelles moyennes de quatre villes différentes (New York, Paris, Tokyo, Sydney) sur une année.

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# Créer un DataFrame avec des données de température mensuelle
data = {
    'Month': ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
    'New York': [32, 35, 45, 55, 65, 75, 80, 75, 70, 60, 50, 40],
    'Paris': [5, 6, 10, 15, 20, 25, 30, 28, 23, 15, 10, 6],
    'Tokyo': [10, 12, 15, 20, 25, 28, 30, 31, 27, 22, 18, 14],
    'Sydney': [25, 26, 24, 20, 17, 15, 14, 16, 18, 20, 22, 24]
}

df = pd.DataFrame(data)

# Afficher les premières lignes du DataFrame pour vérifier
print(df.head())
```

## Étape 2 : Création du Heatmap

Maintenant, nous allons créer un heatmap pour visualiser la corrélation entre les températures mensuelles des différentes villes.

```python
# Calculer la matrice de corrélation
corr_matrix = df[['New York', 'Paris', 'Tokyo', 'Sydney']].corr()
```

1. **Interprétation du Heatmap :**
   - Quelle ville montre la corrélation la plus forte avec New York en termes de températures mensuelles ? 
   - Y a-t-il des mois où les températures de Tokyo et Sydney montrent une corrélation négative ?

2. **Modification des Données :**
   - Ajoutez une nouvelle ville (par exemple, Londres) avec des données de température fictives pour tous les mois.
   - Recalculez la matrice de corrélation et observez comment cela affecte le heatmap.
