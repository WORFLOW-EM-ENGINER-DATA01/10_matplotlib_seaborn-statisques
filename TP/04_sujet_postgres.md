# TP Statistique : Régression Linéaire avec PostgreSQL et Pandas

## Objectifs

1. Charger et explorer un dataset dans PostgreSQL.
2. Effectuer des analyses statistiques basiques.
3. Exécuter une régression linéaire simple directement dans PostgreSQL.
4. Récupérer et visualiser les résultats dans un Jupyter Notebook avec Pandas et Matplotlib.

## Prérequis

- PostgreSQL doit être installé et accessible.
- Pandas, SQLAlchemy, Psycopg2 et Matplotlib doivent être installés dans votre environnement Jupyter Notebook.

## 1. Préparation des données

Pour ce TP, nous allons utiliser le dataset classique "Housing Prices" qui contient des informations sur les maisons, y compris leur prix, la taille, le nombre de chambres, etc. Voici un exemple de dataset en CSV :

```csv
house_id,price,area,bedrooms,bathrooms
1,450000,2000,3,2
2,550000,2500,4,3
3,300000,1500,2,1
4,650000,3000,5,4
5,400000,1800,3,2
```

- Génération de valeurs

```python
import pandas as pd
import numpy as np

# Définir le nombre de lignes à générer
num_rows = 1000

# Générer des identifiants uniques pour chaque maison
house_id = np.arange(1, num_rows + 1)

# Générer des valeurs pour area et price avec une relation logarithmique
np.random.seed(0)
area = np.random.randint(500, 5000, size=num_rows)
price = 50000 + 20000 * np.log(area) + np.random.normal(0, 10000, num_rows)  # Prix suit une loi log(area) + bruit

# Générer des valeurs aléatoires pour les autres colonnes
bedrooms = np.random.randint(1, 6, size=num_rows)
bathrooms = np.random.randint(1, 5, size=num_rows)

# Créer le DataFrame
df = pd.DataFrame({
    'house_id': house_id,
    'price': price.astype(int),
    'area': area,
    'bedrooms': bedrooms,
    'bathrooms': bathrooms
})

# Afficher les premières lignes du DataFrame
print(df.head())

# Sauvegarder le DataFrame en fichier CSV
df.to_csv('housing_prices_generated.csv', index=False)
```

Créez ce fichier CSV dans votre répertoire de travail, par exemple sous le nom `housing_prices.csv`.

## 2. Insertion des données dans PostgreSQL

Créez une table dans PostgreSQL et insérez-y les données.

```sql
-- Créer la table housing
CREATE TABLE housing (
    house_id SERIAL PRIMARY KEY,
    price INT,
    area INT,
    bedrooms INT,
    bathrooms INT
);

-- Insérer les données dans la table housing
COPY housing(price, area, bedrooms, bathrooms)
FROM '/path/to/your/housing_prices.csv'
DELIMITER ','
CSV HEADER;
```

Note : Remplacez `/path/to/your/housing_prices.csv` par le chemin absolu du fichier CSV dans le container PostgreSQL.

## 3. Analyse exploratoire des données avec Pandas

Dans votre Jupyter Notebook, chargez les données depuis PostgreSQL et explorez-les.

```python
import pandas as pd
from sqlalchemy import create_engine

# Créer l'URL de connexion
hostname = 'docker_postgres'
database = 'db'
username = 'admin'
password = 'admin'
port = 5432
connection_string = f"postgresql+psycopg2://{username}:{password}@{hostname}:{port}/{database}"

# Créer le moteur de connexion
engine = create_engine(connection_string)

# Charger les données depuis PostgreSQL
df = pd.read_sql_query("SELECT * FROM housing", engine)

# Afficher les premières lignes du dataset
print(df.head())

# Statistiques descriptives
print(df.describe())
```

## 4. Régression linéaire avec PostgreSQL

Effectuons une régression linéaire simple pour prédire `price` en fonction de `area`.

```sql
-- Installer l'extension nécessaire
CREATE EXTENSION IF NOT EXISTS tablefunc;

-- Exécuter la régression linéaire
SELECT
    regr_slope(price, area) AS slope,
    regr_intercept(price, area) AS intercept,
    regr_r2(price, area) AS r_squared
FROM
    housing;
```

## 5. Récupération et visualisation des résultats

Récupérez les résultats de la régression linéaire dans votre Jupyter Notebook et visualisez-les avec Matplotlib.

```python
# Récupérer les résultats de la régression linéaire
regression_query = """
SELECT
    regr_slope(price, area) AS slope,
    regr_intercept(price, area) AS intercept,
    regr_r2(price, area) AS r_squared
FROM
    housing;
"""
regression_result = pd.read_sql_query(regression_query, engine)

slope = regression_result['slope'][0]
intercept = regression_result['intercept'][0]
r_squared = regression_result['r_squared'][0]

print(f"Slope: {slope}, Intercept: {intercept}, R-squared: {r_squared}")

# Visualisation des résultats
import matplotlib.pyplot as plt

# Scatter plot des données
plt.scatter(df['area'], df['price'], label='Data points')

# Ligne de régression
plt.plot(df['area'], slope * df['area'] + intercept, color='red', label='Regression line')

# Labels et titre
plt.xlabel('Area (sq ft)')
plt.ylabel('Price ($)')
plt.title('Regression Line - Price vs Area')
plt.legend()

# Afficher le plot
plt.show()
```

En suivant ces étapes, vous aurez appris à :

- Charger des données dans PostgreSQL.
- Explorer et analyser ces données avec Pandas.
- Effectuer une régression linéaire directement dans PostgreSQL.
- Récupérer et visualiser les résultats dans un Jupyter Notebook.