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
   - Affichez les 10 premières lignes du DataFrame :
     ```python
     print(data.head(10))
     ```

# Partie 2 : Calcul de la Moyenne Cumulative

1. **Calcul de la Moyenne Cumulative**
   - Utilisez la méthode `expanding().mean()` pour calculer la moyenne cumulative :
     ```python
     data['Moyenne_Cumulative'] = data['Ventes'].expanding().mean()
     ```

2. **Affichage des Données avec Moyenne Cumulative**
   - Affichez les 10 premières lignes du DataFrame incluant la moyenne cumulative :
     ```python
     print(data.head(10))
     ```

# Partie 3 : Calcul de la Moyenne Lissée

1. **Calcul de la Moyenne Lissée**
   - Utilisez la méthode `rolling(window=7).mean()` pour calculer la moyenne lissée sur 7 jours :
     ```python
     data['Moyenne_Lissée'] = data['Ventes'].rolling(window=7).mean()
     ```

2. **Affichage des Données avec Moyenne Lissée**
   - Affichez les 10 premières lignes du DataFrame incluant la moyenne lissée :
     ```python
     print(data.head(10))
     ```

# Partie 4 : Visualisation des Résultats

1. **Création des Graphiques**
   - Utilisez `matplotlib` pour visualiser les résultats :
     ```python
     plt.figure(figsize=(14, 7))

     # Graphique de la moyenne cumulative
     plt.subplot(2, 1, 1)
     plt.plot(data['Date'], data['Moyenne_Cumulative'], label='Moyenne Cumulative')
     plt.xlabel('Date')
     plt.ylabel('Ventes Moyenne Cumulative')
     plt.title('Moyenne Cumulative des Ventes Quotidiennes')
     plt.legend()

     # Graphique des ventes quotidiennes et de la moyenne lissée
     plt.subplot(2, 1, 2)
     plt.plot(data['Date'], data['Ventes'], label='Ventes Quotidiennes')
     plt.plot(data['Date'], data['Moyenne_Lissée'], label='Moyenne Lissée (7 jours)', color='orange')
     plt.xlabel('Date')
     plt.ylabel('Ventes')
     plt.title('Ventes Quotidiennes et Moyenne Lissée')
     plt.legend()

     plt.tight_layout()
     plt.show()
     ```

2. **Interprétation des Résultats**
   - Analysez les graphiques obtenus et décrivez les tendances observées. Répondez aux questions suivantes :
     - La moyenne cumulative se stabilise-t-elle au fil du temps ?
     - Quelle tendance observez-vous dans les ventes quotidiennes après avoir appliqué la moyenne lissée ?


### Interprétation des Résultats

#### Analyse des Graphiques et Tendances Observées

1. **La moyenne cumulative se stabilise-t-elle au fil du temps ?**
   - Oui, la moyenne cumulative se stabilise. Au début, les nouvelles valeurs ajoutées ont un impact plus important sur la moyenne cumulative. Cependant, à mesure que le nombre de points de données augmente, chaque nouvelle valeur a un impact de plus en plus faible, ce qui conduit à une stabilisation de la moyenne cumulative. Cela indique que les données ajoutées récemment sont représentatives de l'ensemble des données.

2. **Quelle tendance observez-vous dans les ventes quotidiennes après avoir appliqué la moyenne lissée ?**
   - La moyenne lissée (moyenne mobile sur 7 jours) montre une tendance plus régulière et moins volatile que les ventes quotidiennes brutes. Les pics et les creux sont atténués, révélant ainsi les tendances sous-jacentes des ventes quotidiennes. Cela permet d'observer des tendances à court terme, telles que des augmentations ou des diminutions régulières des ventes, sans être distrait par les fluctuations quotidiennes aléatoires.

### Questions de Réflexion

1. **Moyenne Cumulative**

   - **Pourquoi la moyenne cumulative est-elle utile pour analyser les ventes ?**
     - La moyenne cumulative est utile pour analyser les ventes car elle permet de suivre l'évolution de la performance moyenne sur une période prolongée. En calculant la moyenne cumulative, on peut observer les tendances globales et la stabilité des ventes, ce qui est particulièrement utile pour détecter des changements à long terme et évaluer la constance de la performance.

   - **Que signifie une stabilisation de la moyenne cumulative ?**
     - Une stabilisation de la moyenne cumulative signifie que les nouvelles valeurs ajoutées sont proches de la moyenne actuelle, indiquant une régularité dans les données. Cela suggère que les variations quotidiennes des ventes se sont atténuées et que le comportement des ventes est devenu prévisible et constant.

2. **Moyenne Lissée**

   - **Pourquoi utilise-t-on une moyenne lissée (moyenne mobile) ?**
     - On utilise une moyenne lissée pour atténuer les fluctuations quotidiennes ou hebdomadaires et pour mieux visualiser les tendances sous-jacentes. La moyenne mobile permet de filtrer le bruit aléatoire et de mettre en évidence les mouvements réguliers ou les tendances saisonnières, ce qui facilite l'analyse et la prise de décision.

   - **Comment la moyenne lissée aide-t-elle à comprendre les tendances des ventes quotidiennes ?**
     - La moyenne lissée aide à comprendre les tendances des ventes quotidiennes en fournissant une vue plus claire et moins volatile des données. En lissant les données, les pics et les creux aléatoires sont réduits, permettant de voir les tendances plus persistantes et les schémas de variation à court terme. Cela permet de détecter des tendances à moyen terme, telles que des augmentations ou des diminutions constantes des ventes, qui seraient autrement masquées par les fluctuations quotidiennes.

