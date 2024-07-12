# Régression linéaire avec `statsmodels`

La régression linéaire est une méthode statistique qui modélise la relation entre une variable dépendante (réponse) et une ou plusieurs variables indépendantes (prédicteurs). 

Elle est largement utilisée pour comprendre et prédire le comportement des variables dépendantes en fonction des variables indépendantes.

## Exemple de données

Pour illustrer la régression linéaire avec `statsmodels`, considérons un exemple où nous voulons prédire les ventes en fonction des dépenses publicitaires. Nous allons utiliser le module `statsmodels` pour ajuster un modèle de régression linéaire à nos données et interpréter les résultats.

- Variable indépendante : Dépenses_publicitaires

C'est la variable que nous utilisons pour prédire ou expliquer la variation dans la variable dépendante (Ventes).

- Variable dépendante : Ventes

C'est la variable que nous cherchons à prédire ou à expliquer en fonction des variations observées dans la variable indépendante (Dépenses_publicitaires).

### Préparation des données

Supposons que nous avons des données sur les dépenses publicitaires et les ventes pour une période donnée :

```python
import numpy as np
import pandas as pd
import statsmodels.api as sm
import matplotlib.pyplot as plt

# Génération des données
np.random.seed(42)  # Pour la reproductibilité
n_points = 100
x = np.linspace(0, 100, n_points)  # Dépenses publicitaires
y = 50 + 2 * x + 10 * np.sin(x / 5) + np.random.normal(0, 10, n_points)  # Ventes avec variation sinus

# Création du DataFrame
df = pd.DataFrame({'Dépenses_publicitaires': x, 'Ventes': y})
```

### Ajustement du modèle de régression linéaire

Nous allons maintenant ajuster un modèle de régression linéaire en utilisant `statsmodels`.

```python
import statsmodels.api as sm

# Variables dépendante (Y) et indépendante (X)
X = df['Dépenses_publicitaires']  # Variable indépendante
y = df['Ventes']                   # Variable dépendante

# Ajout d'une constante à X pour le terme d'interception
X = sm.add_constant(X)

# Création du modèle de régression linéaire
model = sm.OLS(y, X)

# Ajustement du modèle aux données
results = model.fit()

# Afficher les résultats de la régression
print(results.summary())

plt.scatter(df['Dépenses_publicitaires'], df['Ventes'], label='Données observées')
plt.plot(df['Dépenses_publicitaires'], results.fittedvalues, color='red', label='Ligne de régression')
plt.xlabel('Dépenses publicitaires')
plt.ylabel('Ventes')
plt.title('Régression linéaire des ventes en fonction des dépenses publicitaires')
plt.legend()
plt.show()
```

### Interprétation des résultats

- Paramètres de l'équation de régression

```python
# Obtenir les paramètres de la régression
intercept = results.params['const']
slope = results.params['Dépenses_publicitaires']

print(f"Interception (constante): {intercept}")
print(f"Coefficient de la variable indépendante (slope): {slope}")

# Construire l'équation de la droite
equation = f"Y = {slope:.2f}X + {intercept:.2f}"
print(f"Équation de la droite de régression: {equation}")
```

Les résultats de la régression linéaire obtenus à partir de `statsmodels` incluent plusieurs statistiques importantes :

- **R-squared (R²)** : Cette mesure indique la proportion de la variance de la variable dépendante expliquée par le modèle. Plus R² est proche de 1, meilleure est l'ajustement du modèle.
  
- **Coefficient (coef)** : C'est le coefficient estimé pour chaque variable indépendante. Il indique la relation linéaire entre la variable dépendante et la variable indépendante.

- **P-value (P>|t|)** : Il s'agit de la probabilité que le coefficient soit nul. Une faible valeur de p-value (généralement < 0.05) indique que le coefficient est statistiquement significatif.

Dans le contexte de la p-value, cette valeur extrêmement petite indique que l'hypothèse nulle (qui stipule qu'il n'y a pas de relation entre les dépenses publicitaires et les ventes) peut être rejetée avec une très grande certitude. En d'autres termes, il y a une relation statistiquement significative entre les dépenses publicitaires et les ventes.

En général, si la **p-value** est inférieure à un seuil communément utilisé (comme 0.05 ou 0.01), on considère que le résultat est statistiquement significatif. 

Ici, la **p-value** est bien inférieure à ces seuils, ce qui signifie que la relation entre les variables est hautement significative.

```python
p_values = results.pvalues
print("P-values des coefficients :")
print(p_values)
# 5.839428e-71 très faible

# Extraire les intervalles de confiance pour chaque coefficient
ci_intercept = confidence_intervals.loc['const']
ci_slope = confidence_intervals.loc['Dépenses_publicitaires']

print(f"Intervalle de confiance pour l'interception (constante): [{ci_intercept[0]:.2f}, {ci_intercept[1]:.2f}]")
print(f"Intervalle de confiance pour le coefficient de la variable indépendante (slope): [{ci_slope[0]:.2f}, {ci_slope[1]:.2f}]")
```

- **Intervalles de confiance (Conf. Int.)** : Ce sont les plages de valeurs dans lesquelles nous sommes 95% confiants que les vraies valeurs des coefficients se situent.

### Hypothèse nulle avec la p-value

Dans le contexte spécifique de votre régression linéaire entre les dépenses publicitaires (`Dépenses_publicitaires`) et les ventes (`Ventes`), l'hypothèse nulle peut être formulée de la manière suivante :

### Hypothèse nulle 

$$ ( H_0 ) $$

Il n'y a pas de relation linéaire entre les dépenses publicitaires et les ventes. Autrement dit, le coefficient des dépenses publicitaires est égal à zéro.

Formellement :

$$ H_0: \beta_1 = 0 $$

où 
$$ \beta_1 $$  

Est le coefficient de la variable indépendante (dépenses publicitaires).

### Hypothèse alternative 

$$ H_a $$

Il existe une relation linéaire entre les dépenses publicitaires et les ventes. Autrement dit, le coefficient des dépenses publicitaires est différent de zéro.

Formellement :

$$ H_a: \beta_1 \neq 0 $$

### Interprétation dans votre analyse :
- **Hypothèse nulle** 
 
$$ ( H_0 ) $$ 

Les dépenses publicitaires n'ont pas d'effet significatif sur les ventes.
- **Hypothèse alternative**  

$$ ( H_a ) $$ 

Les dépenses publicitaires ont un effet significatif sur les ventes.

Étant donné que votre p-value pour le coefficient des dépenses publicitaires est extrêmement petite (5.839428e-71), cela signifie que vous pouvez rejeter l'hypothèse nulle avec une grande certitude. En d'autres termes, il y a une relation statistiquement significative entre les dépenses publicitaires et les ventes dans votre modèle.

Cela implique que les dépenses publicitaires influencent significativement les ventes, et que l'augmentation des dépenses publicitaires est associée à une augmentation des ventes.