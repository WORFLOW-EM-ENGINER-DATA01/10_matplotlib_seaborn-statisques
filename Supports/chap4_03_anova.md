# Analyse de Variance (ANOVA)

Supposons que nous ayons un jeu de données sur les performances de trois groupes de participants à un test de mathématiques, et nous voulons déterminer s'il y a des différences significatives dans les scores moyens entre ces groupes.

## Jeu de données fictif :

| Groupe   | Score  |
|----------|--------|
| Groupe A | 85     |
| Groupe A | 79     |
| Groupe A | 92     |
| Groupe A | 88     |
| Groupe A | 78     |
| Groupe B | 75     |
| Groupe B | 82     |
| Groupe B | 70     |
| Groupe B | 68     |
| Groupe B | 74     |
| Groupe C | 90     |
| Groupe C | 85     |
| Groupe C | 88     |
| Groupe C | 82     |
| Groupe C | 87     |

## Étapes pour effectuer l'ANOVA en Python :

1. **Charger et préparer les données :**
   - Charger les données dans une structure adaptée (par exemple, un dataframe pandas).

```python
import pandas as pd

# Créer un dataframe à partir des données
data = pd.DataFrame({
    'Groupe': ['A', 'A', 'A', 'A', 'A', 'B', 'B', 'B', 'B', 'B', 'C', 'C', 'C', 'C', 'C'],
    'Score': [85, 79, 92, 88, 78, 75, 82, 70, 68, 74, 90, 85, 88, 82, 87]
})
```

2. **Effectuer l'ANOVA avec `scipy.stats` :**
   - Utiliser la fonction `f_oneway` pour calculer l'ANOVA à un facteur.

```python
from scipy.stats import f_oneway

# Séparer les scores par groupe
groupe_a = data[data['Groupe'] == 'A']['Score']
groupe_b = data[data['Groupe'] == 'B']['Score']
groupe_c = data[data['Groupe'] == 'C']['Score']

# Effectuer l'ANOVA à un facteur
resultats_anova = f_oneway(groupe_a, groupe_b, groupe_c)

# Afficher les résultats
print("Statistique F :", resultats_anova.statistic)
print("p-value :", resultats_anova.pvalue)
```

3. **Interpréter les résultats :**
   - Analyser la statistique F et la p-value pour décider si les moyennes des groupes sont significativement différentes.

```python
# Interpréter la p-value
alpha = 0.05
if resultats_anova.pvalue < alpha:
    print("Il y a des preuves suffisantes pour rejeter l'hypothèse nulle.")
else:
    print("Il n'y a pas suffisamment de preuves pour rejeter l'hypothèse nulle.")
```

### Interprétation des résultats :

Dans cet exemple :

- La statistique F mesure la variation entre les moyennes des groupes par rapport à la variation à l'intérieur des groupes.
- La p-value nous indique la probabilité d'obtenir une statistique F aussi extrême (ou plus) si les moyennes des groupes étaient en réalité égales.
- Si la p-value est inférieure à notre seuil alpha (0.05 dans cet exemple), nous concluons qu'il y a des différences significatives entre au moins deux des groupes.

En suivant ces étapes, vous pouvez facilement effectuer une Analyse de Variance (ANOVA) à un facteur en utilisant Python pour analyser et interpréter des données réelles ou simulées, et ainsi déterminer les différences significatives entre les moyennes de plusieurs groupes.