## 4.1 Sélectionnez le titre de tous les films.

```sql
SELECT title FROM movies;
```
## 4.2 Afficher toutes les classifications distinctes dans la base de données.

```sql
SELECT DISTINCT Rating FROM Movies;
```
## -- 4.3 Afficher tous les films non classés

```sql
SELECT * FROM movies WHERE rating is null;
```
## 4.4 Sélectionner tous les cinémas qui ne diffusent pas de film actuellement.

```sql
SELECT * FROM movietheaters WHERE Movie IS NULL;
```
##  4.5 Sélectionner toutes les données de tous les cinémas 

```sql
SELECT * FROM Movietheaters LEFT JOIN Movies ON Movietheaters.Movie = Movies.code;
```
## 4.6 Sélectionnez toutes les données de tous les films et, si ce film est diffusé dans une salle de cinéma, affichez les données de la salle de cinéma.


```sql
 SELECT * FROM MovieTheaters RIGHT JOIN Movies  ON MovieTheaters.Movie = Movies.Code;
```
## 4.7 Afficher les titres des films qui ne sont actuellement diffusés dans aucun cinéma.

```sql
 SELECT Title FROM Movies 
   WHERE Code NOT IN 
   ( 
     SELECT Movie FROM MovieTheaters 
     WHERE Movie IS NOT NULL 
   ); 
```
##  Ajouter le film non coté "One, Two, three".

```sql
 INSERT INTO Movies(Title,Rating) VALUES('One, Two, Three',NULL); 
```
## 4.9 Fixer la classification de tous les films non classés à "G".

```sql
UPDATE Movies SET Rating='G' WHERE Rating IS NULL;
```
## 4.10 Supprimer les salles de cinéma qui projettent des films classés "NC-17".

```sql
 DELETE FROM MovieTheaters WHERE Movie IN 
   (SELECT Code FROM Movies WHERE Rating = 'NC-17'); 
```
