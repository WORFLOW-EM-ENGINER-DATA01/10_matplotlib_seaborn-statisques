# Prévision des séries temporelles

Pour les séries temporelles, les modèles de prévision tels que ARIMA et Prophet sont largement utilisés en raison de leur efficacité à capturer des schémas complexes dans les données. 

Voici une introduction à l'utilisation de ces modèles avec des exemples pratiques.

## Utilisation de ARIMA

ARIMA (AutoRegressive Integrated Moving Average) est un modèle statistique utilisé pour analyser et prévoir des séries temporelles. Voici comment l'utiliser avec Python :

### Installation des bibliothèques nécessaires

Assurez-vous d'avoir les bibliothèques `pandas` et `statsmodels` installées. Vous pouvez les installer en utilisant pip :

```bash
pip install pandas statsmodels
```

### Exemple pratique avec ARIMA

1. **Création d'une série temporelle fictive** :

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.arima.model import ARIMA

# Initialiser la seed pour la reproductibilité
np.random.seed(42)

# Création d'une série temporelle fictive
date_rng = pd.date_range(start='1/1/2020', end='31/12/2022', freq='M')
sales = np.random.randint(20, 35, size=(len(date_rng))) + 10 * np.sin(np.linspace(0, 3 * np.pi, len(date_rng)))

"""
len(date_rng))) + 10 * np.sin(np.linspace(0, 3 * np.pi, len(date_rng))
Le but global de cette ligne est de créer une séquence de données qui suit une tendance sinusoidale oscillante, décalée vers le haut par la longueur de la séquence de dates. Cela est utile pour générer des données d'exemple avec une tendance temporelle et une composante saisonnière ou périodique.
"""

ts = pd.Series(sales, index=date_rng)
```

2. **Ajustement du modèle ARIMA** :

```python
# Ajustement du modèle ARIMA (p=1, d=1, q=1)
model = ARIMA(ts, order=(1, 1, 1))
model_fit = model.fit()

# Résumé du modèle
print(model_fit.summary())
```

3. **Prévision avec ARIMA** :

```python
# Prévision des 12 prochains mois
forecast = model_fit.forecast(steps=12)
print(forecast)

# Visualisation
plt.figure(figsize=(10, 6))
plt.plot(ts, label='Original')
plt.plot(forecast, label='Forecast', color='red')
plt.legend(loc='upper left')
plt.show()
```

## Utilisation de Prophet

Prophet est un modèle de prévision développé par Facebook, particulièrement efficace pour les données comportant des tendances saisonnières et des points de changement. Voici comment l'utiliser avec Python :

### Installation des bibliothèques nécessaires

Installez Prophet en utilisant pip :

```bash
pip install prophet
```

### Exemple pratique avec Prophet

1. **Préparation des données** :

```python
from prophet import Prophet

# Préparation des données pour Prophet
df = ts.reset_index()
df.columns = ['ds', 'y']
```

2. **Ajustement du modèle Prophet** :

```python
# Initialisation et ajustement du modèle
model = Prophet()
model.fit(df)
```

3. **Prévision avec Prophet** :

```python
# Création d'un dataframe pour les dates futures
future = model.make_future_dataframe(periods=12, freq='M')

# Prévision
forecast = model.predict(future)

# Visualisation
fig = model.plot(forecast)
plt.show()
```

## Comparaison des modèles ARIMA et Prophet

- **ARIMA** :
  - Meilleur pour les séries temporelles stationnaires.
  - Requiert l'ajustement des paramètres `p`, `d`, `q`.
  - Peut capturer les relations auto-régressives et les moyennes mobiles.

- **Prophet** :
  - Conçu pour gérer les séries temporelles non stationnaires avec des tendances et des effets saisonniers.
  - Facile à utiliser avec moins de prétraitement requis.
  - Bon pour les données avec des points de changement et des jours fériés.

## Conclusion

Les modèles ARIMA et Prophet sont deux outils puissants pour la prévision des séries temporelles. ARIMA est plus traditionnel et statistique, tandis que Prophet est plus moderne et intuitif. Le choix entre les deux dépend de la nature de vos données et de vos besoins spécifiques en matière de prévision.