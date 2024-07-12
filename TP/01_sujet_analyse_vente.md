# TP : Analyse des Données des Ventes d’un Supermarché

## Contrainte 

Faites ce TP par équipe de 2, puis présentez vos résultats à la classe.

## Contexte

Vous êtes analyste de données pour un supermarché qui souhaite mieux comprendre ses ventes. Vous allez utiliser un ensemble de données contenant des informations sur les ventes de différents produits sur plusieurs mois. L'objectif est d'analyser les ventes pour identifier des tendances, des anomalies, et des opportunités d'amélioration.

## Dataset

Le fichier de données est disponible dans le dossier Data dans le cours (`Work/Data`). Le dataset est nommé `supermarket_sales.csv` et contient les colonnes suivantes :

- **Invoice ID** : Identifiant de la facture
- **Branch** : Branche du supermarché (A, B, C)
- **City** : Ville (Istanbul, Ankara, İzmir)
- **Customer Type** : Type de client (Member, Normal)
- **Gender** : Genre du client (Male, Female)
- **Product Line** : Catégorie de produit (Food and Beverages, Health and Beauty, Electronic, Home and Living, Sports and Travel, Fashion and Accessories)
- **Unit Price** : Prix unitaire du produit
- **Quantity** : Quantité vendue
- **Total** : Montant total de la facture (Unit Price * Quantity)
- **Date** : Date de la vente
- **Time** : Heure de la vente

### Questions

1. Chargez les données dans un Notebook.
2. Nettoyez les données.
3. Convertir les colonnes Date et Time en type datetime.
4. Supprimez les incohérences, si elles existent.

5. Quels sont les types de données des colonnes `Date` et `Time` après la conversion ?
6. Combien de valeurs manquantes y a-t-il dans chaque colonne ? Comment gérez-vous les valeurs manquantes ?
7. Vérifiez si le DataFrame contient des doublons et expliquez pourquoi il est important de les supprimer.

8.  Analyse de la distribution des ventes par branche

9. Analyse de la distribution des ventes par ville

10. Catégorie de produit la plus vendue

11. Produits les moins vendus
    
12. Visualiser les ventes

13. Quelle branche génère le plus de ventes ? Quelle ville est la plus lucrative ?
       
14. Décrivez la tendance des ventes par semaine. Y a-t-il des pics ou des baisses notables ?

15. Quels sont les résultats des ventes par branche et par ville ?
    
16. Quelle part des ventes est attribuée à chaque ville ? Comment cela se compare-t-il à la répartition des ventes par branche ?
    
17. Quelle est la catégorie de produit qui rapporte le plus de revenus ?

18. Performance par genre

19. Performance par type de client
    
## Partie 2 - autres questions

20. Performance par genre Ventes par genre

21. Ventes par type de client

22. Analyse de la saisonnalité

23. Visualiser les ventes par jour de la semaine

24. Quel est le genre qui dépense le plus ? Le genre qui dépense le moins ?
   
25. Quel type de client dépense le plus ? Quels sont les types de clients ?
   

26. (recherche) Y a-t-il une saisonnalité dans les ventes en fonction des jours de la semaine ?
