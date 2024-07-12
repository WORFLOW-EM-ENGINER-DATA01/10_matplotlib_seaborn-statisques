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

```python
# Effectuer l'ANOVA à un facteur sur les pourboires selon le jour
resultats_anova = f_oneway(
    tips['tip'][tips['day'] == 'Thur'],
    tips['tip'][tips['day'] == 'Fri'],
    tips['tip'][tips['day'] == 'Sat'],
    tips['tip'][tips['day'] == 'Sun']
)

# Afficher les résultats de l'ANOVA
print("Statistique F :", resultats_anova.statistic)
print("p-value :", resultats_anova.pvalue)
```

##  Interprétation des Résultats

```python
alpha = 0.05
if resultats_anova.pvalue < alpha:
    print("Il y a des preuves suffisantes pour rejeter l'hypothèse nulle.")
else:
    print("Il n'y a pas suffisamment de preuves pour rejeter l'hypothèse nulle.")
```

### Interprétation des Résultats :

Si la p-value est inférieure à notre seuil alpha (par exemple, 0.05), cela suggère qu'il existe des différences significatives dans les montants des pourboires laissés selon le jour de la semaine. En d'autres termes, il y a des raisons de croire que le jour de la semaine influence les montants des pourboires laissés au restaurant.
