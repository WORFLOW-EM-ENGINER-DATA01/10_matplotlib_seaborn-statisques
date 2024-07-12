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
# Code ici
```

2. **Chargement des Données** :
    - Chargez le fichier de données des prix des actions de Yahoo.
    - Les données se trouvent [ici](../Work/Notebook/Data/yahoo_stock.csv)

```python
# Code ici
```

3. **Exploration des Données** :
    - Affichez les premières lignes du dataframe et décrivez les colonnes fournies.
    - **Questions** :
        - Quelles sont les colonnes présentes dans le dataset et que représentent-elles ?
        - Quelle est la période couverte par ce dataset ?

```python
# Code ici
```

4. **Visualisation des Données** :
    - Visualisez les colonnes High-Low et Open-Close pour comprendre les variations des prix.
    - **Questions** :
        - Comment visualiser les données d'une série temporelle en utilisant Matplotlib ?
        - Quels patterns ou tendances pouvez-vous observer dans les prix High-Low et Open-Close ?

```python
# Code ici
```

5. **Décomposition des Séries Temporelles** :
    - Décomposez la série temporelle en utilisant la méthode `seasonal_decompose` de la bibliothèque `statsmodels`.
    - **Questions** :
        - Qu'est-ce que la décomposition additive et multiplicative ?
        - Pourquoi est-il important de décomposer une série temporelle avant d'appliquer des modèles de prévision ?

```python
# Code ici
```

6. **Analyse des Résultats** :
    - Analysez les composants décomposés (tendance, saisonnalité, résidus) pour différentes colonnes (Open, Close, High, Low).
    - **Questions** :
        - Comment interpréter les résultats de la décomposition ?
        - Quels sont les composants observés et comment influencent-ils la série temporelle ?

```python
# Code ici
```

7. **Validation des Résultats** :
    - Vérifiez que la somme des composants décomposés (tendance + saisonnalité + résidus) correspond aux valeurs réelles.
    - **Questions** :
        - Pourquoi est-il important de vérifier la somme des composants ?
        - Comment pouvez-vous utiliser les composants décomposés pour améliorer les modèles de prévision ?

```python
# Code ici
```
