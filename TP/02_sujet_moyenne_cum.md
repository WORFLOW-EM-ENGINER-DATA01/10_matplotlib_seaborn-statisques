# TP : Analyse des Ventes Quotidiennes - Moyenne Cumulative et Moyenne Lissée

## Étapes du TP

# Partie 1 : Génération des Données Fictives

1. **Importation des Bibliothèques**
   ```python
   import pandas as pd
   import numpy as np
   import matplotlib.pyplot as plt
   ```

2. **Génération des Données**
   - Configurez les paramètres pour la génération des données :
     ```python
     np.random.seed(42)  # Pour des résultats reproductibles
     num_days = 365
     mean_sales = 50  # Ventes moyennes quotidiennes
     std_dev = 10  # Écart type pour simuler les fluctuations quotidiennes
     ```
   - Génération des dates pour une année entière :
     ```python
     dates = pd.date_range(start='2023-01-01', periods=num_days, freq='D')
     ```
   - Génération des ventes quotidiennes avec une fluctuation autour de la moyenne :
     ```python
     sales = np.random.normal(loc=mean_sales, scale=std_dev, size=num_days)
     ```
   - Création du DataFrame :
     ```python
     data = pd.DataFrame({'Date': dates, 'Ventes': sales})
     ```

3. **Affichage des Données Générées**

# Partie 2 : Calcul de la Moyenne Cumulative

1. **Calcul de la Moyenne Cumulative**

2. **Affichage des Données avec Moyenne Cumulative**

# Partie 3 : Calcul de la Moyenne Lissée

1. **Calcul de la Moyenne Lissée** `rolling` 
 

2. **Affichage des Données avec Moyenne Lissée**


# Partie 4 : Visualisation des Résultats

1. **Création des Graphiques**
   
2. **Interprétation des Résultats**
   - Analysez les graphiques obtenus et décrivez les tendances observées. Répondez aux questions suivantes :
     - La moyenne cumulative se stabilise-t-elle au fil du temps ?
     - Quelle tendance observez-vous dans les ventes quotidiennes après avoir appliqué la moyenne lissée ?

# Questions de Réflexion

1. **Moyenne Cumulative**
   - Pourquoi la moyenne cumulative est-elle utile pour analyser les ventes ?
   - Que signifie une stabilisation de la moyenne cumulative ?

2. **Moyenne Lissée**
   - Pourquoi utilise-t-on une moyenne lissée (moyenne mobile) ?
   - Comment la moyenne lissée aide-t-elle à comprendre les tendances des ventes quotidiennes ?

