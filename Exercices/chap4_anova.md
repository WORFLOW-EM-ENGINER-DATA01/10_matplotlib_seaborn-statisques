# Analyse de Variance (ANOVA) avec le dataset "tips"

Nous allons tester si les montants des pourboires (tips) varient significativement en fonction du jour de la semaine où ils ont été laissés.

## Chargement et Exploration des Données

Nous allons d'abord charger le dataset "tips" de Seaborn et examiner ses caractéristiques.

```python
import seaborn as sns
import pandas as pd
from scipy.stats import f_oneway

# Charger le dataset "tips"
tips = sns.load_dataset('tips')

# Afficher les premières lignes du dataset
print(tips.head())
```

## Formulation de l'Hypothèse

- **Hypothèse nulle (H0) :** Les moyennes des pourboires laissés ne varient pas significativement selon le jour de la semaine.
- **Hypothèse alternative (H1) :** Il existe au moins une paire de jours de la semaine où les moyennes des pourboires diffèrent significativement.

## Effectuer l'ANOVA

Nous allons utiliser l'ANOVA pour comparer les moyennes des pourboires entre les différents jours de la semaine.

