# TP : Analyse des Données des Ventes d’un Supermarché

## Contexte

Vous êtes analyste de données pour un supermarché qui souhaite mieux comprendre ses ventes. Vous allez utiliser un ensemble de données contenant des informations sur les ventes de différents produits sur plusieurs mois. L'objectif est d'analyser les ventes pour identifier des tendances, des anomalies, et des opportunités d'amélioration.

## Dataset

Le fichier de données est disponible en [téléchargement ici](https://www.kaggle.com/datasets/siddharthm16/supermarket-sales). Le dataset est nommé `supermarket_sales.csv` et contient les colonnes suivantes :

Bien sûr! Voici comment vous pourriez répondre à chaque question en utilisant du code Python avec Pandas :

1. **Chargement des données :**

```python
import pandas as pd

# Chargement des données depuis le fichier CSV
df = pd.read_csv('Work/Data/supermarket_sales.csv')
```

2. **Nettoyage des données :**

```python
# Suppression des lignes avec des valeurs manquantes
df.dropna(inplace=True)
```

3. **Conversion des colonnes Date et Time en type datetime :**

```python
df['Date'] = pd.to_datetime(df['Date'])
df['Time'] = pd.to_datetime(df['Time'], format='%H:%M')
```

4. **Suppression des incohérences :**

   Pour répondre à la question 4 sur la suppression des incohérences dans les données, nous devons d'abord identifier quelles incohérences peuvent exister dans le jeu de données des ventes de supermarché. Voici quelques exemples courants d'incohérences et comment vous pourriez les gérer :

### Exemples d'incohérences et leur gestion :

1. **Valeurs négatives dans les colonnes de quantité ou de prix :**
   - Supprimez les lignes où la quantité est négative ou égale à zéro, car cela pourrait indiquer des retours ou des erreurs de saisie.

   ```python
   df = df[df['Quantity'] > 0]
   ```

2. **Dates incorrectes ou futures :**
   - Vérifiez les dates pour vous assurer qu'elles sont dans une plage valide (par exemple, pas de dates dans le futur si les données s'arrêtent à aujourd'hui).

   ```python
   from datetime import datetime
   
   # Supprimer les dates futures
   today = datetime.now()
   df = df[df['Date'] <= today]
   ```

   1. **Montants totaux négatifs :**
      - Assurez-vous que les montants totaux calculés à partir du prix unitaire et de la quantité sont positifs.

      ```python
      df = df[df['Total'] > 0]
      ```

   2. **Données aberrantes dans les colonnes numériques :**
      - Identifiez et gérez les valeurs aberrantes qui pourraient fausser les analyses.

      ```python
      # Exemple : Supprimer les valeurs aberrantes basées sur la distribution (en utilisant des seuils spécifiques)
      Q1 = df['Unit Price'].quantile(0.25)
      Q3 = df['Unit Price'].quantile(0.75)
      IQR = Q3 - Q1
      lower_bound = Q1 - 1.5 * IQR
      upper_bound = Q3 + 1.5 * IQR
      df = df[(df['Unit Price'] >= lower_bound) & (df['Unit Price'] <= upper_bound)]
      ```

   3. **Doublons basés sur l'identifiant de facture :**
      - Supprimez les doublons qui pourraient résulter d'erreurs de saisie ou de duplication.

      ```python
      df.drop_duplicates(subset='Invoice ID', keep='first', inplace=True)
      ```

   4. **Erreurs de saisie dans les catégories de produits ou les branches :**
      - Vérifiez et corrigez les erreurs typographiques ou les valeurs non valides.

      ```python
      # Exemple : Correction des valeurs incorrectes dans la colonne 'Branch'
      df['Branch'].replace({'A1': 'A', 'B1': 'B', 'C1': 'C'}, inplace=True)
      ```
   5. **Types de données après conversion :**

   ```python
   print(df[['Date', 'Time']].dtypes)
   ```

   6. **Valeurs manquantes et gestion :**

   ```python
   # Nombre de valeurs manquantes par colonne
   missing_values = df.isnull().sum()
   print(missing_values)

   # Gestion des valeurs manquantes (ex. suppression des lignes)
   df.dropna(inplace=True)
   ```

   7. **Détection et suppression des doublons :**

   ```python
   # Vérification des doublons
   duplicate_rows = df[df.duplicated()]
   print("Nombre de doublons :", len(duplicate_rows))

   # Suppression des doublons
   df.drop_duplicates(inplace=True)
   ```

8. **Analyse de la distribution des ventes par branche :**

```python
branch_sales = df.groupby('Branch')['Total'].sum()
print(branch_sales)

import matplotlib.pyplot as plt


# Plot
plt.figure(figsize=(8, 6))
branch_sales.plot(kind='bar', color='skyblue')
plt.title('Ventes par branche')
plt.xlabel('Branche')
plt.ylabel('Total des ventes')
plt.xticks(rotation=0)
plt.grid(axis='y')
plt.show()
```

9. **Analyse de la distribution des ventes par ville :**

```python
city_sales = df.groupby('City')['Total'].sum()
print(city_sales)

# Plot
plt.figure(figsize=(10, 6))
city_sales.plot(kind='bar', color='skyblue')
plt.title('Ventes par ville')
plt.xlabel('Ville')
plt.ylabel('Total des ventes')
plt.xticks(rotation=45)
plt.grid(axis='y')
plt.show()
```

10. **Catégorie de produit la plus vendue :**

```python
most_sold_category = df['Product line'].value_counts().idxmax()
print("Catégorie la plus vendue :", most_sold_category)
```

11. **Produits les moins vendus :**

```python
least_sold_products = df.groupby('Product line')['Quantity'].sum().nsmallest(5)
print("Produits les moins vendus :\n", least_sold_products)
```

12.   **Visualisation des ventes :**

```python
import matplotlib.pyplot as plt

day_sales = df.resample('D', on='Date')['Total'].sum()
smoothed_sales = monthly_sales.rolling(window=3).mean()

plt.figure(figsize=(10, 6))
day_sales.plot(kind='line', linestyle='-', color='black')
smoothed_sales.plot(kind='line', linestyle='-', color='r')

plt.title('Ventes mensuelles')
plt.xlabel('Mois')
plt.ylabel('Total des ventes')
plt.grid(True)
plt.show()
```

13. **Branche et ville les plus rentables :**
   

```python
most_profitable_branch = branch_sales.idxmax()
most_profitable_city = city_sales.idxmax()
print("Branche la plus rentable :", most_profitable_branch)
print("Ville la plus rentable :", most_profitable_city)
```

14.  Décrivez la tendance des ventes par semaine. Y a-t-il des pics ou des baisses notables ?

Pour analyser la tendance des ventes par semaine et identifier les pics ou les baisses :

```python
df['Date'] = pd.to_datetime(df['Date'])

# Agrégation des ventes par semaine
monthly_sales = df.resample('ME', on='Date')['Total'].sum()

# Visualisation
plt.figure(figsize=(12, 6))
monthly_sales.plot(kind='line', marker='o', linestyle='-', color='b')
plt.title('Tendance des ventes par semaine')
plt.xlabel('Mois')
plt.ylabel('Total des ventes')
plt.grid(True)
plt.show()
```

15.  Quels sont les résultats des ventes par branche et par ville ?

```python
# Résultats des ventes par branche
branch_sales = df.groupby('Branch')['Total'].sum()

# Résultats des ventes par ville
city_sales = df.groupby('City')['Total'].sum()

print("Résultats des ventes par branche :\n", branch_sales)
print("\nRésultats des ventes par ville :\n", city_sales)
```

16.  Quelle part des ventes est attribuée à chaque ville ? Comment cela se compare-t-il à la répartition des ventes par branche ?

```python
# Calcul de la part des ventes par ville
city_sales_percentage = (city_sales / city_sales.sum()) * 100

# Comparaison avec la répartition des ventes par branche
branch_sales_percentage = (branch_sales / branch_sales.sum()) * 100

print("Part des ventes par ville :\n", city_sales_percentage)
print("\nRépartition des ventes par branche :\n", branch_sales_percentage)
```

17.  Quelle est la catégorie de produit qui rapporte le plus de revenus ?

```python
# Catégorie de produit qui rapporte le plus de revenus
top_category = df.groupby('Product Line')['Total'].sum().idxmax()
print("Catégorie de produit qui rapporte le plus de revenus :", top_category)
```
