# Exercices 

## Partie 1 : Création et Indexation d'une Série Temporelle - introduction

### Exercice 1

Créer une série temporelle à partir de données fictives et effectuer des opérations d'indexation.

1. **Instructions :**
   - Créez une série temporelle quotidienne pour une semaine (du lundi au dimanche).
   - Utilisez des données fictives comme les températures quotidiennes.
   - Indexez la série temporelle par les dates.

2. **Correction :**
   ```python
   import pandas as pd
   import numpy as np

   # Création d'une série temporelle
   dates = pd.date_range(start='2024-07-01', periods=7, freq='D')
   temperatures = [25.6, 26.3, 27.1, 26.8, 27.5, 28.2, 28.9]
   ts = pd.Series(temperatures, index=dates)

   # Affichage de la série temporelle
   print("Série temporelle créée :")
   print(ts)
   ```

   **Explication :** 
   - `pd.date_range` est utilisé pour créer une séquence de dates.
   - Une liste `temperatures` est créée pour les valeurs quotidiennes.
   - `pd.Series` est utilisé pour créer la série temporelle en utilisant `dates` comme index.

### Exercice 2

Manipuler une série temporelle en effectuant des opérations de sélection et de calcul.

1. **Instructions :**
   - À partir de la série temporelle créée précédemment, sélectionnez les températures pour les jours mardi à vendredi.
   - Calculez la température moyenne sur cette période.

2. **Correction :**
   ```python
   # Sélection des températures pour mardi à vendredi
   temp_weekdays = ts['2024-07-02':'2024-07-05']

   # Calcul de la température moyenne
   mean_temperature = temp_weekdays.mean()

   print("Températures du mardi au vendredi :")
   print(temp_weekdays)
   print("\nTempérature moyenne sur cette période :", mean_temperature)
   ```

   **Explication :**
   - `ts['2024-07-02':'2024-07-05']` sélectionne les données pour les jours mardi à vendredi.
   - `.mean()` calcule la moyenne des températures sélectionnées.


### Partie 2 : Chargement des données

1. **Objectif** : Charger les données depuis un fichier CSV et afficher les premières lignes pour vérifier le contenu.

```python
import pandas as pd

# Charger les données depuis le fichier CSV
file_path = '../Data/temperature_series_2024.csv'
ts = pd.read_csv(file_path, parse_dates=['Date'], index_col='Date')

# Afficher les premières lignes du DataFrame
print(ts.head())
```

### Partie 3 : Calcul de la moyenne mobile sur 7 jours

1. **Objectif** : Calculer la moyenne mobile sur une période de 7 jours et ajouter cette information au DataFrame.

```python
# Calculer la moyenne mobile sur 7 jours
ts['7-day'] = ts['Temperature'].rolling(window=7).mean()

# Afficher les premières lignes pour vérifier le calcul
print(ts.head(10))
```

### Partie 4 : Gestion des valeurs NaN

1. **Objectif** : Remplacer les valeurs NaN dans la colonne de la moyenne mobile par la moyenne cumulée jusqu'à cette date.

```python
# Remplacer les NaN par la moyenne cumulée
ts['7-day'] = ts['7-day'].fillna(ts['Temperature'].expanding().mean())

# Afficher les premières lignes pour vérifier le remplissage des NaN
print(ts.head(10))
```

### Partie 5 : Création du graphique

1. **Objectif** : Créer un graphique montrant à la fois les données brutes et la moyenne mobile de 7 jours.

```python
import matplotlib.pyplot as plt

# Créer une nouvelle figure
plt.figure(figsize=(10, 6))

# Tracer les données brutes
plt.plot(ts.index, ts['Temperature'], label='Température brute', color='lightblue')

# Tracer la moyenne mobile de 7 jours
plt.plot(ts.index, ts['7-day'], label='Moyenne mobile 7 jours', color='red')

# Ajouter des titres et légendes
plt.title('Température maximale avec moyenne mobile de 7 jours')
plt.xlabel('Date')
plt.ylabel('Température (°C)')
plt.legend()

# Afficher le graphique
plt.tight_layout()
plt.show()
```

## Le code complet

```python
import pandas as pd
import matplotlib.pyplot as plt

# Charger les données depuis le fichier CSV
file_path = '../Data/temperature_series_2024.csv'
ts = pd.read_csv(file_path, parse_dates=['Date'], index_col='Date')

# Afficher les premières lignes du DataFrame
print("Premières lignes des données :")
print(ts.head())

# Calculer la moyenne mobile sur 7 jours
ts['7-day'] = ts['Temperature'].rolling(window=7).mean()

# Afficher les premières lignes pour vérifier le calcul
print("Données avec la moyenne mobile (7 jours) :")
print(ts.head(10))

# Remplacer les NaN par la moyenne cumulée
ts['7-day'] = ts['7-day'].fillna(ts['Temperature'].expanding().mean())

# Afficher les premières lignes pour vérifier le remplissage des NaN
print("Données après remplissage des NaN :")
print(ts.head(10))

# Créer une nouvelle figure
plt.figure(figsize=(10, 6))

# Tracer les données brutes
plt.plot(ts.index, ts['Temperature'], label='Température brute', color='lightblue')

# Tracer la moyenne mobile de 7 jours
plt.plot(ts.index, ts['7-day'], label='Moyenne mobile 7 jours', color='red')

# Ajouter des titres et légendes
plt.title('Température maximale avec moyenne mobile de 7 jours')
plt.xlabel('Date')
plt.ylabel('Température (°C)')
plt.legend()

# Afficher le graphique
plt.tight_layout()
plt.show()
```

- **Chargement des données** : Les données sont chargées depuis un fichier CSV et indexées par la colonne `Date` pour une manipulation plus facile des séries temporelles.
  
- **Calcul de la moyenne mobile** : Utilisation de la méthode `rolling()` de Pandas pour calculer la moyenne mobile sur une période de 7 jours.
  
- **Gestion des NaN** : Remplacement des valeurs NaN dans la colonne de la moyenne mobile par la moyenne cumulée des températures.

