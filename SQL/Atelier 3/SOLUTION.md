## ous devez créer une base données, et imiter les requêtes dans le fichier sql shema.
 
 ## 3.1 Sélectionner tous les entrepôts
 ```sql
 SELECT * FROM Warehouses
 ```
| Code | Location      | Capacity |
|:----:|:------------- |:--------:|
|    1 | chicage       |        3 |
|    2 | chicago       |        4 |
|    3 | New York      |        7 |
|    4 | Los Angeles   |        2 |
|    5 | San Francisco |        8 |

## 3.2 Sélectionnez toutes les cases dont la valeur est supérieure à 150 $.

```sql
SELECT * FROM boxes WHERE value > 150;
```
| Code | Contents | Value | Warehouse |
|:-----|:---------|:-----:|:----------|
| 0MN7 | Rocks    |   180 |         3 |
| 4H8P | Rocks    |   250 |         1 |
| 4RT3 | Scissors |   190 |         4 |
| 7G3H | Rocks    |   200 |         1 |
| 9J6F | Papers   |   175 |         2 |

## 3.3 Sélectionner tous les contenus distincts dans toutes les cases.
```sql
SELECT DISTINCT Contents FROM boxes;
```
| Contents |
|:---------|
| Rocks    |
| Scissors |
| Papers   |

## 3.4 Sélectionner la valeur moyenne de toutes les boîtes
```sql
SELECT AVG(value) FROM boxes;
```
| AVG(value)         |
|:------------------:|
| 147.72727272727272 |

## 3.5 Sélectionner le code de l'entrepôt et la valeur moyenne des boîtes dans chaque entrepôt
```sql
    SELECT Warehouse, AVG(Value) FROM Boxes GROUP By Warehouse;
```
## 3.6 Identique à l'exercice précédent, mais ne sélectionner que les entrepôts où la valeur moyenne des boîtes est supérieure à 150.

```sql
  SELECT Warehouse, AVG(Value) FROM Boxes GROUP BY Warehouse HAVING AVG(Value) > 150;
```

## 3.7 Sélectionnez le code de chaque boîte, ainsi que le nom de la ville dans laquelle la boîte est située.

```sql
 SELECT Boxes.code, Location FROM Warehouses INNER JOIN Boxes ON Warehouses.Code = Boxes.Warehouse;
```
## 3.8 Sélectionnez les codes des entrepôts, ainsi que le nombre de boîtes dans chaque entrepôt. 

```sql
SELECT Warehouse, COUNT(*) FROM boxes GROUP BY Warehouse;
```
## 3.9 Sélectionnez les codes de tous les entrepôts qui sont saturés (un entrepôt est saturé si le nombre de boîtes qu'il contient est supérieur à la capacité de l'entrepôt).

```sql
SELECT Code  FROM Warehouses WHERE Capacity < ( SELECT COUNT(*) FROM Boxes WHERE Warehouse = Warehouses.Code);
```
## 3.10 Sélectionnez les codes de toutes les boîtes situées à Chicago.

```sql
SELECT Code 
   FROM Boxes 
   WHERE Warehouse IN 
   ( 
     SELECT Code 
       FROM Warehouses 
       WHERE Location = 'Chicago' 
   );   
```
## 3.11 Créer un nouvel entrepôt à New York avec une capacité de 3 boîtes.

```sql
INSERT INTO Warehouses (Location, Capacity) VALUES ('New York',3);
```
## 3.12 Créer une nouvelle boîte, avec le code "H5RT", contenant des "Papers" d'une valeur de 200 $, et située dans l'entrepôt 2.

```sql
INSERT INTO Boxes VALUES('H5RT','Papers',200,2); 
```
## 3.13 Réduire la valeur de toutes les boîtes de 15 %.

```sql
UPDATE Boxes SET Value = Value * 0.85;
```
## 3.14 Retirer toutes les boîtes d'une valeur inférieure à 100
```sql
DELETE FROM Boxes WHERE Value < 100
```
## 15 Retirer toutes les boîtes des entrepôts saturés

```sql
CREATE INDEX INDEX_WAREHOUSE ON Boxes (warehouse); 
```
## 3.17 Imprimer tous les index existants.

```sql
SHOW INDEX FROM Boxes;
```
##

```sql

```
