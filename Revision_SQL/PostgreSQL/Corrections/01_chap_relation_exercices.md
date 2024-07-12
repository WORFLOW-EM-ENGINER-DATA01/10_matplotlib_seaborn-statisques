# Exercices

1. **Liste des clients avec leurs commandes et détails de commande :**
```sql
SELECT c.name AS customer_name, o.id AS order_id, oi.quantity, p.title AS photo_title
FROM customers c
JOIN orders o ON c.id = o.customer_id
JOIN order_items oi ON o.id = oi.order_id
JOIN photos p ON oi.photo_id = p.id;
```

2. **Liste des photos avec leurs tags associés :**
```sql
SELECT p.title AS photo_title, t.name AS tag_name
FROM photos p
JOIN photo_tags pt ON p.id = pt.photo_id
JOIN tags t ON pt.tag_id = t.id;
```

3. **Total des ventes par client :**
```sql
SELECT c.name AS customer_name, SUM(oi.quantity * oi.price) AS total_sales
FROM customers c
JOIN orders o ON c.id = o.customer_id
JOIN order_items oi ON o.id = oi.order_id
GROUP BY c.id;
```

4. **Liste des produits avec leurs descriptions complètes :**
```sql
SELECT p.data->>'name' AS product_name, p.data->>'description' AS product_description
FROM products p;
```

5. **Détails des commandes pour une photo spécifique :**
```sql
SELECT o.id AS order_id, c.name AS customer_name, oi.quantity, oi.price
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
JOIN customers c ON o.customer_id = c.id
WHERE oi.photo_id = (SELECT id FROM photos WHERE title = 'Sunset at Beach');
```

6. **Liste des tags avec le nombre de photos associées :**
```sql
SELECT t.name AS tag_name, COUNT(pt.photo_id) AS photo_count
FROM tags t
LEFT JOIN photo_tags pt ON t.id = pt.tag_id
GROUP BY t.name;
```

7. **Commandes passées par un client spécifique avec les détails des photos commandées :**
```sql
SELECT o.id AS order_id, p.title AS photo_title, oi.quantity, oi.price
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
JOIN photos p ON oi.photo_id = p.id
WHERE o.customer_id = (SELECT id FROM customers WHERE name = 'Bob Smith');
```

8. **Liste des photos sans tag :**
```sql
SELECT p.title AS photo_title
FROM photos p
LEFT JOIN photo_tags pt ON p.id = pt.photo_id
WHERE pt.photo_id IS NULL;
```

9. **Total des ventes par mois et année :**
```sql
SELECT DATE_TRUNC('month', o.order_date) AS month_year, SUM(oi.quantity * oi.price) AS total_sales
FROM orders o
JOIN order_items oi ON o.id = oi.order_id
GROUP BY DATE_TRUNC('month', o.order_date)
ORDER BY month_year;
```

10. **Liste des clients ayant passé au moins une commande avec des photos de montagnes :**
```sql
SELECT DISTINCT c.name AS customer_name
FROM customers c
JOIN orders o ON c.id = o.customer_id
JOIN order_items oi ON o.id = oi.order_id
JOIN photos p ON oi.photo_id = p.id
JOIN photo_tags pt ON p.id = pt.photo_id
JOIN tags t ON pt.tag_id = t.id
WHERE t.name = 'mountain';
```