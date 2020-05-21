
## 1/Créer la base donnée sous nom "boutique".
```sql
 CREATE DATABESE boutique
```
| Database           |
| :----------------- | 
| boutique           |
| information_schema |
| mysql              |
| performance_schema |
| phpmyadmin         |
## 2/Création des tables (Manufacturers, Products).
```sql
MariaDB [boutique]> CREATE TABLE Manufacturers(
Code INT auto_increment,
    Name varchar(100),
    primary key(Code)
);
MariaDB [boutique]> CREATE TABLE Products(
Code INT auto_increment,
Name VARCHAR(100),
Price float,
Manufacturer_code INT,
primary key(Code),
foreign key(Manufacturer_code) references manufacturers(Code)
);
```
## 3/Insérer dans le tableau Manufacturers les valeurs :
```sql
MariaDB [boutique]> INSERT INTO manufacturers (Name) VALUES ('Sony'), ('Creative Labs'), ('Hewlett-Packard'), ('Iomega'), ('Fujitsu'), ('Winchester');
```
```sql
SELECT * FROM `manufacturers`;
```
| Code | Name            |
| :---:| :-------------- | 
|    1 | Sony            |
|    2 | Creative Labs   |
|    3 | Hewlett-Packard |
|    4 | Iomega          |
|    5 | Fujitsu         |
|    6 | Winchester      |


## 4/ Insérer dans le tableau Products :
```sql
MariaDB [boutique]> INSERT INTO products (Name, Price, Manufacturer_code) VALUES 
('Hard drive', 240.00, 5),
('Memory', 120.00, 6),
('ZIP drive', 150.00, 4),
('Floppy disk', 5.00, 6),
('Monitor', 240.00, 1),
('DVD drive', 180.00, 2),
('CD drive', 90.00, 2),
('Printer', 270.00, 3),
('Toner cartridge', 66.00, 3),
('DVD burner', 180.00, 2) ;
```
MariaDB [boutique]> SELECT*FROM `products`;

| Code | Name            | Price | Manufacturer_code |
| :--: | :---------------| :---: | :---------------: | 
|    1 | Hard drive      |   240 |                 5 |
|    2 | Memory          |   120 |                 6 |
|    3 | ZIP drive       |   150 |                 4 |
|    4 | Floppy disk     |     5 |                 6 |
|    5 | Monitor         |   240 |                 1 |
|    6 | DVD drive       |   180 |                 2 |
|    7 | CD drive        |    90 |                 2 |
|    8 | Printer         |   270 |                 3 |
|    9 | Toner cartridge |    66 |                 3 |
|   10 | DVD burner      |   180 |                 2 |


## 6/ Sélectionner les noms et les prix de tous les produits du magasin.
```sql
MariaDB [boutique]> SELECT Name, Price FROM products;
```
| Name            | Price |
| :-------------- | :---: | 
| Hard drive      |   240 |
| Memory          |   120 |
| ZIP drive       |   150 |
| Floppy disk     |     5 |
| Monitor         |   240 |
| DVD drive       |   180 |
| CD drive        |    90 |
| Printer         |   270 |
| Toner cartridge |    66 |
| DVD burner      |   180 |

## 7/ Sélectionner le nom des produits dont le prix est inférieur ou égal à 200 $.
```sql
MariaDB [boutique]> SELECT Name FROM products WHERE Price <= 200;
```
| Name            |
| :-------------- | 
| Memory          |
| ZIP drive       |
| Floppy disk     |
| DVD drive       |
| CD drive        |
| Toner cartridge |
| DVD burner      |

## 8/ Sélectionnez tous les produits dont le prix est compris entre 60 et 120 dollars.
```sq
MariaDB [boutique]> SELECT * FROM products WHERE Price between 60 and 120;
```
| Code | Name            | Price | Manufacturer_code |
| :--: | :-------------- | :---: | :---------------- | 
|    2 | Memory          |   120 |                 6 |
|    7 | CD drive        |    90 |                 2 |
|    9 | Toner cartridge |    66 |                 3 |

## 9/Sélectionnez le nom et le prix en cents (c'est-à-dire que le prix doit être multiplié par 100).
```sql
MariaDB [boutique]> SELECT Price*100  AS Price_Cents, Name FROM products ;
```

| Price_Cents | Name            |
| :---------: | :-------------- | 
|       24000 | Hard drive      |
|       12000 | Memory          |
|       15000 | ZIP drive       |
|         500 | Floppy disk     |
|       24000 | Monitor         |
|       18000 | DVD drive       |
|        9000 | CD drive        |
|       27000 | Printer         |
|        6600 | Toner cartridge |
|       18000 | DVD burner      |

## 10/Calculer le prix moyen de tous les produits.
```sql
MariaDB [boutique]> SELECT AVG(Price) FROM products ;
```
| AVG(Price) |
| :--------: | 
|      154.1 |

## 11/Calculer le prix moyen de tous les produits dont le code fabricant est égal à 2.
```sql
MariaDB [boutique]> SELECT AVG(Price) FROM products WHERE Manufacturer_code = 2;
```
| AVG(Price) |
| :--------: | 
|        150 |

## 12/ Calculer le nombre de produits dont le prix est supérieur ou égal à 180 dollars.
```sql
MariaDB [boutique]> SELECT count(*) FROM products WHERE price >= 180;
```
| count(*) |
| :------: | 
|        5 |

## 13) Sélectionner le nom et le prix de tous les produits dont le prix est supérieur ou égal à 180 dollars, et trier d'abord par prix (par ordre décroissant), puis par nom (par ordre croissant).
```sql
MariaDB [boutique]> SELECT Name , Price FROM products WHERE price >= 180 order by Price desc,Name Asc;
```
| Name       | Price |
| :--------- | :---: | 
| Printer    |   270 |
| Hard drive |   240 |
| Monitor    |   240 |
| DVD burner |   180 |
| DVD drive  |   180 |

## 14) Sélectionnez toutes les données des produits, y compris toutes les données relatives au fabricant de chaque produit.
```sql
MariaDB [boutique]> SELECT * FROM products INNER JOIN manufacturers on products.Manufacturer_code = manufacturers.Code;
```

| Code | Name            | Price | Manufacturer_code | Code | Name            |
| :--: | :-------------- | :---: | :---------------: | :--: | :-------------- | 
|    1 | Hard drive      |   240 |                 5 |    5 | Fujitsu         |
|    2 | Memory          |   120 |                 6 |    6 | Winchester      |
|    3 | ZIP drive       |   150 |                 4 |    4 | Iomega          |
|    4 | Floppy disk     |     5 |                 6 |    6 | Winchester      |
|    5 | Monitor         |   240 |                 1 |    1 | Sony            |
|    6 | DVD drive       |   180 |                 2 |    2 | Creative Labs   |
|    7 | CD drive        |    90 |                 2 |    2 | Creative Labs   |
|    8 | Printer         |   270 |                 3 |    3 | Hewlett-Packard |
|    9 | Toner cartridge |    66 |                 3 |    3 | Hewlett-Packard |
|   10 | DVD burner      |   180 |                 2 |    2 | Creative Labs   |

## 15) Sélectionnez le nom du produit, le prix et le nom du fabricant de tous les produits.
```sql
MariaDB [boutique]> SELECT products.Name, products.Price, manufacturers.Name FROM products INNER JOIN manufacturers on products.Manufacturer_code = manufacturers.Code;
```

| Name            | Price | Name            |
| :-------------- | :---: | :-------------- | 
| Hard drive      |   240 | Fujitsu         |
| Memory          |   120 | Winchester      |
| ZIP drive       |   150 | Iomega          |
| Floppy disk     |     5 | Winchester      |
| Monitor         |   240 | Sony            |
| DVD drive       |   180 | Creative Labs   |
| CD drive        |    90 | Creative Labs   |
| Printer         |   270 | Hewlett-Packard |
| Toner cartridge |    66 | Hewlett-Packard |
| DVD burner      |   180 | Creative Labs   |

## 16) Sélectionnez le prix moyen des produits de chaque fabricant, en indiquant uniquement le code du fabricant.
```sql
MariaDB [boutique]> SELECT  AVG(Price), Manufacturer_code FROM products group by Manufacturer_code;
```

| AVG(Price) | Manufacturer_code |
| :--------: | :---------------: |  
|        240 |                 1 |
|        150 |                 2 |
|        168 |                 3 |
|        150 |                 4 |
|        240 |                 5 |
|       62.5 |                 6 |

## 17) Sélectionnez le prix moyen des produits de chaque fabricant, en indiquant le nom du fabricant.
```sql
MariaDB [boutique]> SELECT  AVG(Price), manufacturers.Name FROM products INNER JOIN manufacturers on products.Manufacturer_code = manufacturers.Code group by Manufacturer_code;
```

| AVG(Price) | Name            |
| :--------: | :-------------- | 
|        240 | Sony            |
|        150 | Creative Labs   |
|        168 | Hewlett-Packard |
|        150 | Iomega          |
|        240 | Fujitsu         |
|       62.5 | Winchester      |

## 8) Sélectionnez les noms des fabricants dont les produits ont un prix moyen supérieur ou égal à 150 $.
```sql
MariaDB [boutique]> SELECT  AVG(Price), manufacturers.Name FROM products INNER JOIN manufacturers on products.Manufacturer_code = manufacturers.Code group by Manufacturer_code  having AVG(Price) >= 150;
```

| AVG(Price) | Name            |
| :--------: | :-------------- | 
|        240 | Sony            |
|        150 | Creative Labs   |
|        168 | Hewlett-Packard |
|        150 | Iomega          |
|        240 | Fujitsu         |

## 19/Sélectionnez le nom et le prix du produit le moins cher
```sql
MariaDB [boutique]> SELECT Name, Price FROM products WHERE Price = (SELECT min(Price) FROM products);
```

| Name        | Price |
| :---------- | :---: | 
| Floppy disk |     5 |

## 20) Sélectionnez le nom de chaque fabricant ainsi que le nom et le prix de son produit le plus cher.
```sql
MariaDB [boutique]>  SELECT M.name, P.Name, P.Price FROM products P join manufacturers M on P.Manufacturer_code = M.Code group by Manufacturer_code ;
```

| name            | Name       | Price |
| :-------------- | :--------- | :---: | 
| Sony            | Monitor    |   240 |
| Creative Labs   | DVD drive  |   180 |
| Hewlett-Packard | Printer    |   270 |
| Iomega          | ZIP drive  |   150 |
| Fujitsu         | Hard drive |   240 |
| Winchester      | Memory     |   120 |

## 21) Ajouter un nouveau produit : Loudspeakers, 70 $, manufacter 2
```sql
INSERT INTO products (Name, Price, Manufacturer_code) VALUES ('Loudspeakers', 70.00, 2);
```
## 22) Mettre à jour le nom du produit 8 en "laser Print".
```sql
MariaDB [boutique]> UPDATE products SET Name = 'Laser Print' WHERE Code = 8;
```
## 23) Appliquer une remise de 10 % à tous les produits.
```sql
MariaDB [boutique]> UPDATE products SET Price = Price*0.9;
MariaDB [boutique]> UPDATE products SET Price = Price - (Price*0.1);
```
## 24) Appliquer une remise de 10 % à tous les produits dont le prix est supérieur ou égal à 120 $.
```sql
MariaDB [boutique]> UPDATE products SET Price = Price*0.9 WHERE Price >= 120;
```
| Code | Name            | Price  | Manufacturer_code |
| :--: | :-------------- | :----: | :---------------: | 
|    1 | Hard drive      | 174.96 |                 5 |
|    2 | Memory          |   97.2 |                 6 |
|    3 | ZIP drive       | 109.35 |                 4 |
|    4 | Floppy disk     |   4.05 |                 6 |
|    5 | Monitor         | 174.96 |                 1 |
|    6 | DVD drive       | 131.22 |                 2 |
|    7 | CD drive        |   72.9 |                 2 |
|    8 | Laser Print     | 196.83 |                 3 |
|    9 | Toner cartridge |  53.46 |                 3 |
|   10 | DVD burner      | 131.22 |                 2 |
|   11 | Loudspeakers    |   56.7 |                 2 |




