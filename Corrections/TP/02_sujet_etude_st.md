# Sujet de TP : Décomposition des Séries Temporelles en Tendance et Saisonnalité

## Objectifs du TP :
Ce TP a pour but de comprendre et de mettre en pratique la décomposition des séries temporelles en leurs composantes fondamentales : tendance, saisonnalité et résidus. Cette approche permet de mieux comprendre la structure des séries temporelles et d'améliorer les modèles de prévision.

## Introduction :
La décomposition des séries temporelles consiste à considérer une série comme une combinaison de plusieurs composantes : le niveau, la tendance, la saisonnalité et le bruit. Cela offre un modèle abstrait utile pour analyser et prévoir les séries temporelles.

Dans ce TP, nous apprendrons à identifier et à extraire ces différentes composantes en utilisant Python. Il est toujours utile de décomposer une série temporelle en ses composantes avant d'appliquer des modèles de prévision.

Les composantes de la série temporelle peuvent être classées en deux catégories :
1. **Composantes Systématiques** : Elles peuvent être modélisées car elles suivent un système ou une récurrence.
2. **Composantes Non Systématiques** : Elles ne peuvent pas être modélisées car elles sont aléatoires.

Nous allons explorer ces composantes et apprendre à les modéliser.

## Étapes du TP :

1. **Importation des Bibliothèques** :
    - Importez les bibliothèques nécessaires pour l'analyse et la visualisation des données.
    - **Question** : Quelles bibliothèques sont nécessaires pour ce TP et pourquoi les utilise-t-on ?

    ```python
    import numpy as np  # Pour l'algèbre linéaire
    import pandas as pd  # Pour le traitement des données et la manipulation des fichiers CSV
    import matplotlib.pyplot as plt  # Pour la visualisation des données
    from statsmodels.tsa.seasonal import seasonal_decompose  # Pour la décomposition des séries temporelles
    ```

2. **Chargement des Données** :
    - Chargez le fichier de données des prix des actions de Yahoo.
    - **Question** : Comment charger un fichier CSV en utilisant Pandas ? Quelle est l'importance de la colonne de date dans une série temporelle ?

    ```python
    # Charger le fichier CSV
    df = pd.read_csv('/chemin/vers/votre_fichier/yahoo_stock.csv', parse_dates=['Date'], index_col='Date')

    # La colonne de date est essentielle car elle permet de gérer et d'analyser les données dans le contexte temporel
    ```

3. **Exploration des Données** :
    - Affichez les premières lignes du dataframe et décrivez les colonnes fournies.
    - **Questions** :
        - Quelles sont les colonnes présentes dans le dataset et que représentent-elles ?
        - Quelle est la période couverte par ce dataset ?

    ```python
    # Afficher les premières lignes
    print(df.head())

    # Afficher les informations descriptives
    print(df.describe())

    # Colonnes et leurs significations :
    # - High : Prix le plus élevé de l'action pour cette date.
    # - Low : Prix le plus bas de l'action pour cette date.
    # - Open : Prix d'ouverture de l'action.
    # - Close : Prix de clôture de l'action.
    # - Volume : Montant total de l'activité de trading.
    # - AdjClose : Valeurs ajustées prenant en compte les actions d'entreprise (dividendes, divisions d'actions, émissions de nouvelles actions).

    # Période couverte : 
    print(df.index.min())
    print(df.index.max())
    # 2015-11-23 à 2020-11-20
    ```

4. **Visualisation des Données** :
    - Visualisez les colonnes High-Low et Open-Close pour comprendre les variations des prix.
    - **Questions** :
        - Comment visualiser les données d'une série temporelle en utilisant Matplotlib ?
        - Quels patterns ou tendances pouvez-vous observer dans les prix High-Low et Open-Close ?

    ```python
    # Visualiser High et Low
    df[['High', 'Low']].plot(figsize=(15, 5), alpha=0.5)
    plt.show()

    # Visualiser Open et Close
    df[['Open', 'Close']].plot(figsize=(15, 5), alpha=0.5)
    plt.show()

    # Observation :
    # - Les prix d'ouverture et de clôture montrent des variations limitées.
    # - Les prix les plus élevés et les plus bas montrent également des variations limitées.
    ```

5. **Décomposition des Séries Temporelles** :
    - Décomposez la série temporelle en utilisant la méthode `seasonal_decompose` de la bibliothèque `statsmodels`.
    - **Questions** :
        - Qu'est-ce que la décomposition additive et multiplicative ?
        - Pourquoi est-il important de décomposer une série temporelle avant d'appliquer des modèles de prévision ?

    ```python
    def decompose(df, column_name):
        """
        Fonction pour décomposer une série temporelle en utilisant les modèles additif et multiplicatif.
        """
        result_mul = seasonal_decompose(df[column_name], model='multiplicative', extrapolate_trend='freq')
        result_add = seasonal_decompose(df[column_name], model='additive', extrapolate_trend='freq')

        plt.rcParams.update({'figure.figsize': (20, 10)})
        result_mul.plot().suptitle('Décomposition Multiplicative', fontsize=30)
        result_add.plot().suptitle('Décomposition Additive', fontsize=30)
        plt.show()

        return result_mul, result_add

    result_mul, result_add = decompose(df, 'Open')

    # Décomposition additive : Les composants sont additionnés (linéaire).
    # Décomposition multiplicative : Les composants sont multipliés (non linéaire).
    # Importance : Permet d'identifier et de modéliser les différentes composantes (tendance, saisonnalité, résidus) séparément pour une meilleure prévision.
    ```

6. **Analyse des Résultats** :
    - Analysez les composants décomposés (tendance, saisonnalité, résidus) pour différentes colonnes (Open, Close, High, Low).
    - **Questions** :
        - Comment interpréter les résultats de la décomposition ?
        - Quels sont les composants observés et comment influencent-ils la série temporelle ?

    ```python
    result_mul_open, result_add_open = decompose(df, 'Open')
    result_mul_close, result_add_close = decompose(df, 'Close')
    result_mul_high, result_add_high = decompose(df, 'High')
    result_mul_low, result_add_low = decompose(df, 'Low')

    # Interprétation :
    # - Tendance : Montre l'évolution à long terme.
    # - Saisonnalité : Montre les cycles répétitifs à court terme.
    # - Résidus : Montre les variations aléatoires.
    # Ces composants aident à comprendre et à modéliser la série temporelle.
    ```

7. **Validation des Résultats** :
    - Vérifiez que la somme des composants décomposés (tendance + saisonnalité + résidus) correspond aux valeurs réelles.
    - **Questions** :
        - Pourquoi est-il important de vérifier la somme des composants ?
        - Comment pouvez-vous utiliser les composants décomposés pour améliorer les modèles de prévision ?

    ```python
    df_reconstructed = pd.concat([result_add_open.seasonal, result_add_open.trend, result_add_open.resid, result_add_open.observed], axis=1)
    df_reconstructed.columns = ['Saisonnalité', 'Tendance', 'Résidu', 'Valeurs Réelles']

    # Vérification de la somme des composants
    df_reconstructed['Reconstructed'] = df_reconstructed['Saisonnalité'] + df_reconstructed['Tendance'] + df_reconstructed['Résidu']
    print(df_reconstructed.head())

    # Importance : 
    # Vérifier la somme garantit que la décomposition est correcte et que les composants peuvent être utilisés pour la modélisation.
    # Utilisation : Les composants décomposés peuvent être utilisés comme caractéristiques dans les modèles de prévision pour améliorer la précision.
    ```

## Conclusion :
Ce TP vous permettra de comprendre comment décomposer des séries temporelles en leurs composants principaux. Cela facilitera l'analyse et l'application de modèles de prévision en tenant compte des tendances et des cycles saisonniers présents dans les données.

## Remarque :
N'oubliez pas de sauvegarder votre travail et de partager vos résultats avec vos collègues pour une discussion approfondie. Profitez de cette opportunité pour explorer davantage les séries temporelles et leurs applications pratiques dans le domaine de l'analyse de données et de la finance.