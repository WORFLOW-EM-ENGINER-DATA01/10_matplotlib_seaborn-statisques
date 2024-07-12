
```python
import pandas as pd
import matplotlib.pyplot as plt

# Exemple de données de température
data = {
    'Date': pd.date_range(start='2024-01-01', periods=10, freq='D'),
    'Temperature': [20, 22, 19, 23, 21, 18, 24, 20, 25, 19]
}

# Création du DataFrame
ts = pd.DataFrame(data)
ts.set_index('Date', inplace=True)

# Calcul de la moyenne cumulative
ts['Cumulative MA'] = ts['Temperature'].expanding().mean()

# Afficher les résultats
print(ts)

# Création du graphique
plt.figure(figsize=(10, 6))

# Tracer les données brutes
plt.plot(ts.index, ts['Temperature'], label='Température brute', color='lightblue')

# Tracer la moyenne cumulative
plt.plot(ts.index, ts['Cumulative MA'], label='Moyenne cumulative', color='red')

# Ajouter des titres et légendes
plt.title('Température maximale avec moyenne cumulative')
plt.xlabel('Date')
plt.ylabel('Température (°C)')
plt.legend()

# Afficher le graphique
plt.tight_layout()
plt.show();

```