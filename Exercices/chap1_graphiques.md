### Exercices sur les graphes statistiques

#### Exercice 1 : Diagramme en barres (barplot) - variables discrètes

Utilisez le jeu de données `tips` pour créer un diagramme en barres qui compare le nombre total de pourboires donnés (variable `tip`) par fumeur et non-fumeur (variable `smoker`).

1. Chargez le jeu de données `tips` à l'aide de Seaborn.
2. Utilisez la fonction `sns.barplot` pour créer le diagramme en barres.
3. Définissez `x` comme étant la variable `smoker` et `y` comme étant la variable `tip`.
4. Affichez le graphique.
5. À partir de l'ensemble de données tips qui contient des informations sur les pourboires, souhaitez-vous créer un diagramme en barres pour comparer le nombre de fumeurs et de non-fumeurs par sexe ?

#### Exercice 2 : Diagramme en ligne (lineplot) - variables continues

Utilisez le jeu de données `tips` pour créer un diagramme en ligne qui montre la relation entre le montant total de la note (variable `total_bill`) et le pourboire (variable `tip`) en fonction du sexe du serveur (variable `sex`).

1. Chargez le jeu de données `tips`.
2. Utilisez la fonction `sns.lineplot` pour créer le diagramme en ligne.
3. Définissez `x` comme étant la variable `total_bill`, `y` comme étant la variable `tip`, et `hue` comme étant la variable `sex`.
4. Affichez le graphique.
5. Etudiez maintenant cette même relation en fonction du lunch ou dinner.

#### Exercice 3 : Diagramme à points (scatterplot) - variables continues

Utilisez le jeu de données `tips` pour créer un diagramme à points qui montre la relation entre le montant total de la note (variable `total_bill`) et le pourboire (variable `tip`) en fonction du moment de la journée (variable `time`).

1. Chargez le jeu de données `tips`.
2. Utilisez la fonction `sns.scatterplot` pour créer le diagramme à points.
3. Définissez `x` comme étant la variable `total_bill`, `y` comme étant la variable `tip`, et `hue` comme étant la variable `time`.
4. Affichez le graphique.
5. Etudiez la répartition des tips par sex.

#### Exercice 4 : Diagramme en boîtes (boxplot) - variables continues

Utilisez le jeu de données `tips` pour créer un diagramme en boîtes qui compare la distribution des montants totaux de la note (variable `total_bill`) entre les différents jours de la semaine (variable `day`).

1. Chargez le jeu de données `tips`.
2. Utilisez la fonction `sns.boxplot` pour créer le diagramme en boîtes.
3. Définissez `x` comme étant la variable `day` et `y` comme étant la variable `total_bill`.
4. Affichez le graphique.

#### Exercice 5 : Diagramme en violon (violinplot) - variables continues

Utilisez le jeu de données `tips` pour créer un diagramme en violon qui compare la distribution des pourboires (variable `tip`) entre les différents jours de la semaine (variable `day`).

1. Chargez le jeu de données `tips`.
2. Utilisez la fonction `sns.violinplot` pour créer le diagramme en violon.
3. Définissez `x` comme étant la variable `day` et `y` comme étant la variable `tip`.
4. Affichez le graphique.

Dans le contexte du Titanic, bien que la variable `age` ne soit pas directement liée à la mortalité des enfants à bord, elle peut être explorée pour comprendre la répartition des passagers par âge dans différentes classes, ce qui peut indirectement fournir des insights sur la démographie des passagers, y compris les enfants.

Pour examiner spécifiquement la mortalité des enfants à bord du Titanic, il serait pertinent de se concentrer sur d'autres variables telles que `age` (âge), `who` (qui), et `survived` (survécu), et éventuellement les croiser avec d'autres comme `pclass` (classe), `sex` (sexe), et `alone` (seul).
