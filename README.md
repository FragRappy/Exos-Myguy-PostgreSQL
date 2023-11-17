# Pratique du SQL

Nous allons continuer à découvrir le SQL, en passant par l'interface web DB-Fiddle afin de nous concentrer sur l'essentiel.

## :zero: Interface DB-Fiddle (rappel)

Avant d'utiliser cette interface, assurez-vous d'avoir sélectionné en haut à gauche la bonne version de SGBD (DBMS) : **PostgreSQL v15**

![sélection du DBMS](./screenshots/select-dbms.png)

## :one: Extraire des données à la demande

Rendez-vous sur cette interface avec un schema déjà pré-rempli : [players-scores](https://www.db-fiddle.com/f/9xfK1brxfTuxFihVXWWR56/8)

1. extraire les informations d'un joueur à partir de son prénom ou de son nom

```sql
-- code SQL ici
```

2. compter le nombre de parties gagnées par un joueur

```sql
-- code SQL ici
```

3. compter le nombre de parties jouées par un joueur

```sql
-- code SQL ici
```

4. extraire la liste de toutes les parties perdues par un joueur

```sql
-- code SQL ici
```

5. extraire la liste de tous les joueurs majeurs

```sql
-- code SQL ici
```

6. extraire la liste de tous les joueurs qui ont rejoint le club avant 2022

```sql
-- code SQL ici
```

7. extraire la liste de tous les joueurs et les trier par
   - ordre alphabétique
   - par age
   - par date d'entrée dans le club

```sql
-- code SQL ici
```

8. calculer le pourcentage de victoires pour chaque joueur du club

```sql
-- code SQL ici
```

> Ecrire une requête qui récupère tous les films réalisés par les Etats Unis et qui ont une note supérieure ou égale à 4

```sql
-- code SQL ici
```

## :lollipop: Bonus

Seulement si vous avez le temps, et que vous avez encore envie de coder :

- faire en sorte que les résultats des demandes précédentes affichent les dates au format **JJ/MM/AAAA**
- Quand on extrait les données des scores, faire en sorte que le nom et le prénom du joueur s'affichent en toute lettre sur la même ligne dans le tableau de résultats.


>! Correction Spoiler
>. extraire les informations d'un joueur à partir de son prénom ou de son nom
>
>```sql
>SELECT *
>FROM players
>WHERE "firstname" = 'Kelly';
>```
>
>2. compter le nombre de parties gagnées par joueur
>
>```sql
>SELECT "firstname", "lastname", COUNT(*) AS "matchs gagnés"
>FROM "players"
>JOIN "scores"
>ON "players"."id" = "scores"."winner"
> -- WHERE "players"."xxxx" = 'xxx" // Peut permettre de filtrer par un nom de colonne ou de remplir une condition
>GROUP BY "firstname", "lastname";
>```
>
>3. compter le nombre de parties jouées par joueur
>
>```sql
>SELECT "firstname", "lastname", COUNT(*) AS "matchs joués"
>FROM "players"
>JOIN "scores"
>ON "players"."id" = "scores"."looser"
>OR "players"."id" = "scores"."winner"
> -- WHERE "players"."xxxx" = 'xxx" // Peut permettre de filtrer par un nom de colonne ou de remplir une condition
>GROUP BY "firstname", "lastname"
>```
>
>4. extraire la liste de toutes les parties perdues par joueur
>
>```sql
>SELECT "firstname", "lastname", COUNT(*) AS "matchs perdu"
>FROM "players"
>JOIN "scores"
>ON "players"."id" = "scores"."looser"
> -- WHERE "players"."xxxx" = 'xxx" // Peut permettre de filtrer par un nom de colonne ou de remplir une condition
>GROUP BY "firstname", "lastname";
>```
>
>5. extraire la liste de tous les joueurs majeurs avec leur age actuel
>
>```sql
>SELECT "firstname", "lastname", ((now()::date - birth::date) / 365) AS "age"
>FROM "players"
>WHERE birth::date <= (CURRENT_DATE - INTERVAL '18 year')::date
>GROUP BY "firstname", "lastname", "birth";
>```
>
>6. extraire la liste de tous les joueurs qui ont rejoint le club avant 2022
>
>```sql
>SELECT "firstname", "lastname"
>FROM "players"
>WHERE "createdAt" < '2022-01-01';
>```
>
>7. extraire la liste de tous les joueurs et les trier par
>   - ordre alphabétique
>   - par age
>   - par date d'entrée dans le club
>
>```sql
>SELECT *
>FROM "players"
>ORDER BY "firstname", "birth", "createdAt";  -- // Priorité de filtrage firstname -> birth -> createAt en ASC (changer l'ordre suivant le besoin ainsi que la méthode de filtrage ASC ou DESC)
>```
>
>8. calculer le pourcentage de victoires pour chaque joueur du club
>
>```sql
>--SELECT "firstname", "lastname", (COUNT("winner") / COUNT(*)) * 100 //Ne marche pas
>--FROM "players"
>--JOIN "scores"
>--ON "players"."id" = "scores"."looser"
>--OR "players"."id" = "scores"."winner"
>--GROUP BY "firstname", "lastname";
>```
>
>## :lollipop: Bonus
>
>Seulement si vous avez le temps, et que vous avez encore envie de coder :
>
>- faire en sorte que les résultats des demandes précédentes affichent les dates au format **JJ/MM/AAAA**
>- Quand on extrait les données des scores, faire en sorte que le nom et le prénom du joueur s'affichent en toute lettre sur la même ligne dans le tableau de résultats.