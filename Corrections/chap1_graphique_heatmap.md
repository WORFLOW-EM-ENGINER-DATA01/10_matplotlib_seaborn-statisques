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

# Créer un heatmap avec Seaborn
plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix, annot=True, cmap='coolwarm', linewidths=.5, square=True,
            xticklabels=corr_matrix.columns, yticklabels=corr_matrix.columns)
plt.title('Heatmap de Corrélation des Températures Mensuelles')
plt.show()
```

### Questions pour l'Exercice :

1. **Interprétation du Heatmap :**
   - Quelle ville montre la corrélation la plus forte avec New York en termes de températures mensuelles ?
   - Y a-t-il des mois où les températures de Tokyo et Sydney montrent une corrélation négative ?

2. **Modification des Données :**
   - Ajoutez une nouvelle ville (par exemple, Londres) avec des données de température fictives pour tous les mois.
   - Recalculez la matrice de corrélation et observez comment cela affecte le heatmap.


## 1. Interprétation du Heatmap :

## Quelle ville montre la corrélation la plus forte avec New York en termes de températures mensuelles ?

Pour déterminer la ville qui présente la corrélation la plus forte avec New York en termes de températures mensuelles, nous devons examiner la ligne ou la colonne correspondant à New York dans la matrice de corrélation.

```python
# Calculer la matrice de corrélation
corr_matrix = df[['New York', 'Paris', 'Tokyo', 'Sydney']].corr()

# Identifier la corrélation de New York avec les autres villes
correlation_with_ny = corr_matrix['New York'].drop('New York')  # Exclure New York lui-même

# Trouver la ville avec la corrélation maximale
max_corr_city = correlation_with_ny.idxmax()
max_corr_value = correlation_with_ny[max_corr_city]

print(f"La ville avec la corrélation la plus forte avec New York est {max_corr_city} avec une corrélation de {max_corr_value:.2f}")
```

**Réponse :** La ville avec la corrélation la plus forte avec New York est Tokyo avec une corrélation de 0.92 (par exemple).

## Y a-t-il des mois où les températures de Tokyo et Sydney montrent une corrélation négative ?

Pour déterminer s'il y a des mois où les températures de Tokyo et Sydney montrent une corrélation négative, nous devons examiner les valeurs dans la matrice de corrélation entre Tokyo et Sydney.

```python
# Vérifier la corrélation entre Tokyo et Sydney dans la matrice de corrélation
corr_ts = corr_matrix.loc['Tokyo', 'Sydney']

if corr_ts < 0:
    print(f"Il y a des mois où les températures de Tokyo et Sydney montrent une corrélation négative.")
else:
    print(f"Il n'y a pas de mois où les températures de Tokyo et Sydney montrent une corrélation négative.")
```

**Réponse :** Cela dépend du résultat spécifique de la matrice de corrélation. Si `corr_ts` est inférieur à zéro, alors il y a des mois où les températures de Tokyo et Sydney montrent une corrélation négative.

## 2. Modification des Données :

## Ajoutez une nouvelle ville (par exemple, Londres) avec des données de température fictives pour tous les mois.

Pour cette étape, nous allons ajouter une nouvelle ville (Londres) avec des données de température fictives pour tous les mois, puis recalculer la matrice de corrélation pour observer comment cela affecte le heatmap.

```python
# Ajouter Londres avec des données fictives
df['Londres'] = [8, 7, 10, 12, 15, 18, 20, 19, 17, 14, 10, 8]

# Recalculer la matrice de corrélation
corr_matrix_updated = df[['New York', 'Paris', 'Tokyo', 'Sydney', 'Londres']].corr()

# Afficher le nouveau heatmap de corrélation
plt.figure(figsize=(10, 8))
sns.heatmap(corr_matrix_updated, annot=True, cmap='coolwarm', linewidths=.5, square=True,
            xticklabels=corr_matrix_updated.columns, yticklabels=corr_matrix_updated.columns)
plt.title('Heatmap de Corrélation des Températures Mensuelles avec Londres')
plt.show()
```

En ajoutant Londres et en recalculant la matrice de corrélation, nous observons comment cela modifie les relations de corrélation entre toutes les villes, y compris la nouvelle ville ajoutée.
