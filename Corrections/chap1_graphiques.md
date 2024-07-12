### Correction détaillée des exercices sur les graphes statistiques

#### Exercice 1 : Diagramme en barres (barplot) - variables discrètes

1. **Charger le jeu de données `tips` à l'aide de Seaborn.**
2. **Utiliser la fonction `sns.barplot` pour créer le diagramme en barres.**
3. **Définir `x` comme étant la variable `smoker` et `y` comme étant la variable `tip`.**
4. **Afficher le graphique.**

**Correction :**

1. Charger le jeu de données `tips` à l'aide de Seaborn :
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt

    # Charger les données "tips"
    tips = sns.load_dataset("tips")
    ```

2. Utiliser la fonction `sns.barplot` pour créer le diagramme en barres :
    ```python
    sum_tips = tips.groupby('smoker', observed=False)['tip'].sum().reset_index()
    sns.barplot(x="smoker", y="tip", data=sum_tips)
    ```

3. Définir `x` comme étant la variable `smoker` et `y` comme étant la variable `tip` :
    - `x="smoker"` indique que l'axe des abscisses (x) représente les fumeurs et non-fumeurs.
    - `y="tip"` indique que l'axe des ordonnées (y) représente le montant des pourboires.

4. Afficher le graphique :
    ```python
    plt.title("Total des pourboires par fumeur et non-fumeur")
    plt.xlabel("Fumeur")
    plt.ylabel("Total des pourboires")
    plt.show()
    ```

**Code complet :**
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Charger les données "tips"
tips = sns.load_dataset("tips")

# Créer le diagramme en barres
sum_tips = tips.groupby('smoker', observed=False)['tip'].sum().reset_index()
sns.barplot(x="smoker", y="tip", data=sum_tips)
plt.title("Total des pourboires par fumeur et non-fumeur")
plt.xlabel("Fumeur")
plt.ylabel("Total des pourboires")
plt.show()
```

5. À partir de l'ensemble de données tips qui contient des informations sur les pourboires, souhaitez-vous créer un diagramme en barres pour comparer le nombre de fumeurs et de non-fumeurs par sexe ?

```python
count_data = tips.groupby(['smoker', 'sex'], observed=False)['tip'].sum().reset_index()

plt.figure(figsize=(8, 6))
sns.barplot( count_data, x='sex', y='tip', hue='smoker')
```

Remarque: sur une méthode utiliser dans la correction

La méthode **reset_index()** en pandas est utilisée pour réinitialiser l'index d'un DataFrame. Lorsque vous manipulez des données dans pandas, il est courant que les opérations effectuées (comme le filtrage, le regroupement, etc.) modifient l'index du DataFrame résultant. reset_index() permet de rétablir cet index à sa forme initiale ou de créer un nouvel index numérique, en fonction des paramètres spécifiés.

 l'intérêt de reset_index() est d'assurer la cohérence et la facilité d'utilisation des données après des manipulations complexes, en rétablissant un index numérique régulier et en permettant de supprimer l'ancien index si nécessaire. Cela améliore la lisibilité des données, simplifie les opérations d'accès aux données et prépare les données pour des analyses ultérieures.

#### Exercice 2 : Diagramme en ligne (lineplot) - variables continues

1. **Charger le jeu de données `tips`.**
2. **Utiliser la fonction `sns.lineplot` pour créer le diagramme en ligne.**
3. **Définir `x` comme étant la variable `total_bill`, `y` comme étant la variable `tip`, et `hue` comme étant la variable `sex`.**
4. **Afficher le graphique.**

**Correction :**

1. Charger le jeu de données `tips` :
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt

    # Charger les données "tips"
    tips = sns.load_dataset("tips")
    ```

2. Utiliser la fonction `sns.lineplot` pour créer le diagramme en ligne :
    ```python
    sns.lineplot(x="total_bill", y="tip", hue="sex", data=tips)
    ```

3. Définir `x` comme étant la variable `total_bill`, `y` comme étant la variable `tip`, et `hue` comme étant la variable `sex` :
    - `x="total_bill"` indique que l'axe des abscisses (x) représente le montant total de la note.
    - `y="tip"` indique que l'axe des ordonnées (y) représente le montant des pourboires.
    - `hue="sex"` colore les lignes en fonction du sexe du serveur.

4. Afficher le graphique :
    ```python
    plt.title("Relation entre le montant total de la note et le pourboire en fonction du sexe")
    plt.xlabel("Montant total de la note")
    plt.ylabel("Pourboire")
    plt.show()
    ```
5. Etudiez maintenant cette même relation en fonction du lunch ou dinner.
    ```python
    tips['time'].unique()
    tipsDinner = tips[ tips[ 'time' ] == 'Dinner' ]
    tipsLunch = tips[ tips[ 'time' ] == 'Lunch' ]

    plt.figure(figsize=(8, 6))
    sns.lineplot(x="total_bill", y="tip", hue="sex", data=tipsDinner)
    plt.title("Relation entre le montant total de la note et le pourboire pour le dîner en fonction du sexe")
    plt.xlabel("Montant total de la note")
    plt.ylabel("Pourboire")
    plt.show();
    ```

#### Exercice 3 : Diagramme à points (scatterplot) - variables continues

1. **Charger le jeu de données `tips`.**
2. **Utiliser la fonction `sns.scatterplot` pour créer le diagramme à points.**
3. **Définir `x` comme étant la variable `total_bill`, `y` comme étant la variable `tip`, et `hue` comme étant la variable `time`.**
4. **Afficher le graphique.**
5. **Etudiez cela maintenant par sex**


1. Charger le jeu de données `tips` :
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt

    # Charger les données "tips"
    tips = sns.load_dataset("tips")
    ```

2. Utiliser la fonction `sns.scatterplot` pour créer le diagramme à points :
    ```python
    sns.scatterplot(x="total_bill", y="tip", hue="time", data=tips)
    ```

3. Définir `x` comme étant la variable `total_bill`, `y` comme étant la variable `tip`, et `hue` comme étant la variable `time` :
    - `x="total_bill"` indique que l'axe des abscisses (x) représente le montant total de la note.
    - `y="tip"` indique que l'axe des ordonnées (y) représente le montant des pourboires.
    - `hue="time"` colore les points en fonction du moment de la journée (déjeuner ou dîner).

4. Afficher le graphique :
    ```python
    plt.title("Relation entre le montant total de la note et le pourboire en fonction du moment de la journée")
    plt.xlabel("Montant total de la note")
    plt.ylabel("Pourboire")
    plt.show()
    ```
5. Par sex
   
```python
# Par sex
tipsMale = tips[tips['sex'] == 'Male']
sns.scatterplot(x="total_bill", y="tip", hue="time", data=tipsMale);

tipsFemale = tips[tips['sex'] == 'Female']
sns.scatterplot(x="total_bill", y="tip", hue="time", data=tipsFemale);
```

**Code complet :**
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Charger les données "tips"
tips = sns.load_dataset("tips")

# Créer le diagramme à points
sns.scatterplot(x="total_bill", y="tip", hue="time", data=tips)
plt.title("Relation entre le montant total de la note et le pourboire en fonction du moment de la journée")
plt.xlabel("Montant total de la note")
plt.ylabel("Pourboire")
plt.show()
```

#### Exercice 4 : Diagramme en boîtes (boxplot) - variables continues

1. **Charger le jeu de données `tips`.**
2. **Utiliser la fonction `sns.boxplot` pour créer le diagramme en boîtes.**
3. **Définir `x` comme étant la variable `day` et `y` comme étant la variable `total_bill`.**
4. **Afficher le graphique.**

**Correction :**

1. Charger le jeu de données `tips` :
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt

    # Charger les données "tips"
    tips = sns.load_dataset("tips")
    ```

2. Utiliser la fonction `sns.boxplot` pour créer le diagramme en boîtes :
    ```python
    sns.boxplot(x="day", y="total_bill", data=tips)
    ```

3. Définir `x` comme étant la variable `day` et `y` comme étant la variable `total_bill` :
    - `x="day"` indique que l'axe des abscisses (x) représente les différents jours de la semaine.
    - `y="total_bill"` indique que l'axe des ordonnées (y) représente le montant total de la note.

4. Afficher le graphique :
    ```python
    tips['day'].unique() # nombre de jours 4 
    plt.title("Distribution des montants totaux de la note par jour de la semaine")
    plt.xlabel("Jour de la semaine")
    plt.ylabel("Montant total de la note")
    plt.show();
    ```

**Code complet :**
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Charger les données "tips"
tips = sns.load_dataset("tips")

# Créer le diagramme en boîtes
sns.boxplot(x="day", y="total_bill", data=tips)
plt.title("Distribution des montants totaux de la note par jour de la semaine")
plt.xlabel("Jour de la semaine")
plt.ylabel("Montant total de la note")
plt.show()
```

#### Exercice 5 : Diagramme en violon (violinplot) - variables continues

1. **Charger le jeu de données `tips`.**
2. **Utiliser la fonction `sns.violinplot` pour créer le diagramme en violon.**
3. **Définir `x` comme étant la variable `day` et `y` comme étant la variable `tip`.**
4. **Afficher le graphique.**

**Correction :**

1. Charger le jeu de données `tips` :
    ```python
    import seaborn as sns
    import matplotlib.pyplot as plt

    # Charger les données "tips"
    tips = sns.load_dataset("tips")
    ```

2. Utiliser la fonction `sns.violinplot` pour créer le diagramme en violon :
    ```python
    sns.violinplot(x="day", y="tip", data

=tips)
    ```

3. Définir `x` comme étant la variable `day` et `y` comme étant la variable `tip` :
    - `x="day"` indique que l'axe des abscisses (x) représente les différents jours de la semaine.
    - `y="tip"` indique que l'axe des ordonnées (y) représente le montant des pourboires.

4. Afficher le graphique :
    ```python
    plt.title("Distribution des pourboires par jour de la semaine")
    plt.xlabel("Jour de la semaine")
    plt.ylabel("Pourboire")
    plt.show()
    ```

**Code complet :**
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Charger les données "tips"
tips = sns.load_dataset("tips")

# Créer le diagramme en violon
sns.violinplot(x="day", y="tip", data=tips)
plt.title("Distribution des pourboires par jour de la semaine")
plt.xlabel("Jour de la semaine")
plt.ylabel("Pourboire")
plt.show()
```

## Avec le Titanic

1. **Distribution des âges par catégorie `who` :**
   Utilisez un diagramme en violon pour comparer la distribution des âges entre les hommes, femmes et enfants (`who` variable dans le dataset Titanic).

   ```python
   sns.violinplot(x='who', y='age', data=titanic)
   ```

2. **Survie des enfants par classe et sexe :**
   Analysez la survie des enfants en fonction de leur classe de voyage et de leur sexe pour voir s'il y a des différences marquées.

   ```python
   sns.catplot(x='class', hue='sex', col='survived', data=titanic[titanic['who']=='child'], kind='count')
   ```

3. **Mortalité des enfants par classe :**
   Utilisez un diagramme en barres pour comparer le nombre d'enfants décédés dans chaque classe.

   ```python
   sns.barplot(x='class', y='survived', hue='who', data=titanic[titanic['who']=='child'], estimator=lambda x: len(x) - sum(x))
   ```

La répartition des âges chez les enfants survivants pourrait refléter une politique de priorisation basée sur l'âge lors du sauvetage, où les plus jeunes ont eu la priorité.
La concentration des enfants non survivants parmi les nourrissons pourrait refléter la vulnérabilité accrue des très jeunes enfants lors du naufrage.