
20. Performance par genre

```python
# Total des ventes par genre
gender_sales = df.groupby('Gender')['Total'].sum()

print("Performance par genre :\n", gender_sales)
```

21. Performance par type de client

```python
# Total des ventes par type de client
customer_type_sales = df.groupby('Customer Type')['Total'].sum()

print("Performance par type de client :\n", customer_type_sales)
```

22. Ventes par genre

```python
# Ventes détaillées par genre
gender_sales_detail = df.groupby(['Gender', 'Product Line'])['Total'].sum()

print("Ventes par genre :\n", gender_sales_detail)
```

23. Ventes par type de client

```python
# Ventes détaillées par type de client
customer_type_sales_detail = df.groupby(['Customer Type', 'Product Line'])['Total'].sum()

print("Ventes par type de client :\n", customer_type_sales_detail)
```

24. Analyse de la saisonnalité

Pour analyser la saisonalité des ventes au fil du temps :

```python
from statsmodels.tsa.seasonal import seasonal_decompose

# Agrégation des ventes semaine
monthly_sales = df.resample('W', on='Date')['Total'].sum()

# Décomposition saisonnière
decomposition = seasonal_decompose(monthly_sales, model='additive', extrapolate_trend='freq')

# Visualisation de la décomposition saisonnière
decomposition.plot()
plt.show()
```

25. Visualiser les ventes par jour de la semaine

```python
# Assurez-vous que la colonne 'Date' est bien de type datetime
df['Date'] = pd.to_datetime(df['Date'])

# Ajouter une colonne pour le jour de la semaine (lundi=0, dimanche=6)
df['Day of Week'] = df['Date'].dt.dayofweek

# Total des ventes par jour de la semaine
sales_by_day = df.groupby('Day of Week')['Total'].sum()

# Renommer les jours de la semaine pour l'affichage
days_of_week = ['Lundi', 'Mardi', 'Mercredi', 'Jeudi', 'Vendredi', 'Samedi', 'Dimanche']
sales_by_day.index = days_of_week

# Visualisation
plt.figure(figsize=(10, 6))
sales_by_day.plot(kind='bar', color='skyblue')
plt.title('Ventes par jour de la semaine')
plt.xlabel('Jour de la semaine')
plt.ylabel('Total des ventes')
plt.xticks(rotation=45)
plt.show()
```

26. Quel est le genre qui dépense le plus ? Le genre qui dépense le moins ?

```python
# Total des ventes par genre
gender_sales = df.groupby('Gender')['Total'].sum()

# Genre qui dépense le plus et le moins
highest_spender_gender = gender_sales.idxmax()
lowest_spender_gender = gender_sales.idxmin()

print("Genre qui dépense le plus :", highest_spender_gender)
print("Genre qui dépense le moins :", lowest_spender_gender)
```

27. Quel type de client dépense le plus ? Quels sont les types de clients ?

```python
# Total des ventes par type de client
customer_type_sales = df.groupby('Customer Type')['Total'].sum()

# Type de client qui dépense le plus
highest_spending_customer_type = customer_type_sales.idxmax()

print("Type de client qui dépense le plus :", highest_spending_customer_type)
print("\nDétails des ventes par type de client :\n", customer_type_sales)
```

28. Y a-t-il une saisonnalité dans les ventes en fonction des jours de la semaine ?

```python
# Total des ventes par jour de la semaine
sales_by_day = df.groupby('Day of Week')['Total'].sum()


# Exemple de visualisation pour détecter la saisonnalité des ventes par jour de la semaine
plt.figure(figsize=(10, 6))
sales_by_day.plot(kind='line', marker='o', linestyle='-', color='b')
plt.title('Saisonnalité des ventes par jour de la semaine')
plt.xlabel('Jour de la semaine')
plt.ylabel('Total des ventes')
plt.grid(True)
plt.xticks(range(7), days_of_week)  # Rééchelonner les étiquettes de l'axe x avec les jours de la semaine
plt.show()
```