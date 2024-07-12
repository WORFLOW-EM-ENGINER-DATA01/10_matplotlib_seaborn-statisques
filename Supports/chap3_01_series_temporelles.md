# Cours détaillé sur les séries temporelles

## 1. Introduction aux séries temporelles

**Qu'est-ce qu'une série temporelle ?**
- Une série temporelle est une séquence de données mesurées à des intervalles réguliers dans le temps. Chaque observation est associée à un instant spécifique.
- Exemples : données économiques (PIB, taux de chômage), météorologiques (température, précipitations), ventes journalières, etc.

**Exemples d'applications des séries temporelles**
- Prévisions économiques et financières.
- Modélisation climatique et météorologique.
- Surveillance de la performance des entreprises.
- Détection de tendances et saisonnalités.

## 2. Travailler avec des séries temporelles dans Pandas

**Création d'une série temporelle**
```python
import pandas as pd

# Création d'une série temporelle avec des dates
dates = pd.date_range('2023-01-01', periods=365)
ts = pd.Series(range(365), index=dates)
```

**Indexation des séries temporelles**
- Accès aux données temporelles spécifiques :
```python
ts['2023-05-15']
```

**Manipulation des séries temporelles**
- Calcul de moyennes mobiles :
```python
ts.rolling(window=30).mean()
```

## 3. Manipulation des fréquences

**Fréquences des séries temporelles**
- Définition de la fréquence :
```python
ts = ts.asfreq('D')  # D pour quotidien
```

**Changement de la fréquence**
- Rééchantillonnage pour changer la fréquence :
```python
ts.resample('M').mean()  # Rééchantillonnage mensuel avec moyenne
```

**Regroupement des données en intervalles de temps**
- Agrégation par période :
```python
ts.groupby(pd.Grouper(freq='W')).sum()  # Somme hebdomadaire
```

## 4. Analyse des tendances et des saisons

**Tendances et saisons dans les séries temporelles**

Pour décomposer une série temporelle (`ts`) en ses trois composants principaux : tendance (`trend`), saisonnier (`seasonal`) et résiduel (`residual`), on utilise `seasonal_decompose`.

1. **Importation de la fonction `seasonal_decompose`** :
   ```python
   from statsmodels.tsa.seasonal import seasonal_decompose
   ```

   Cette ligne importe la fonction `seasonal_decompose` qui permet de décomposer une série temporelle en ses composants.

2. **Décomposition de la série temporelle** :
   ```python
   decomposition = seasonal_decompose(ts, model='additive')
   ```

   Ici, la série temporelle `ts` est décomposée en utilisant un modèle additif. Le modèle additif suppose que les composants sont ajoutés ensemble, c'est-à-dire :
   \[
   Y(t) = T(t) + S(t) + R(t)
   \]
   où \( Y(t) \) est la valeur observée à temps \( t \), \( T(t) \) est la tendance, \( S(t) \) est le composant saisonnier et \( R(t) \) est le résiduel.

3. **Extraction des composants décomposés** :
   ```python
   trend = decomposition.trend
   seasonal = decomposition.seasonal
   residual = decomposition.resid
   ```

Ces lignes extraient respectivement les composants de tendance, saisonnier et résiduel de l'objet `decomposition`.

### Exemple 

Supposons que nous avons une série temporelle mensuelle des ventes d'un magasin sur 3 ans :

```python
import pandas as pd
import numpy as np

# Création d'une série temporelle fictive
np.random.seed(42) # garanti d'avoir le même jeu de données 
date_rng = pd.date_range(start='1/1/2020', end='31/12/2022', freq='M')
sales = np.random.randint(20, 35, size=(len(date_rng))) + 10*np.sin(np.linspace(0, 3 * np.pi, len(date_rng)))

ts = pd.Series(sales, index=date_rng)
```

Voyons maintenant comment appliquer `seasonal_decompose` à cette série temporelle :

```python
from statsmodels.tsa.seasonal import seasonal_decompose

# Décomposition de la série temporelle
decomposition = seasonal_decompose(ts, model='additive')

# Extraction des composants
trend = decomposition.trend
seasonal = decomposition.seasonal
residual = decomposition.resid

# Affichage des composants
import matplotlib.pyplot as plt

plt.figure(figsize=(12, 8))
plt.subplot(411)
plt.plot(ts, label='Original')
plt.legend(loc='upper left')

plt.subplot(412)
plt.plot(trend, label='Trend')
plt.legend(loc='upper left')

plt.subplot(413)
plt.plot(seasonal, label='Seasonal')
plt.legend(loc='upper left')

plt.subplot(414)
plt.plot(residual, label='Residual')
plt.legend(loc='upper left')

plt.tight_layout()
plt.show()
```

### Interprétation des résultats :

- **Série originale (Original)** : C'est la série temporelle initiale avec toutes ses composantes.
- **Tendance (Trend)** : Cette courbe montre la tendance générale des ventes au fil du temps, en filtrant les fluctuations saisonnières et les résidus.
- **Saisonnier (Seasonal)** : Ce composant capture les variations périodiques qui se répètent à intervalles réguliers, par exemple, les variations saisonnières mensuelles.
- **Résiduel (Residual)** : Ce sont les variations restantes qui ne peuvent pas être expliquées par la tendance ou le composant saisonnier. Il capture les anomalies et le bruit.

En utilisant ce processus, vous pouvez analyser les différents aspects de vos données temporelles pour mieux comprendre les tendances sous-jacentes et les variations saisonnières.
