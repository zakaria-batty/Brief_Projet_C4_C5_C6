## vous devez créer une base données, et imiter les requêtes dans le fichier sql shema
 * Department 
 
| Code | Name            | Budget |
|:----:|:----------------|:------:|
|   14 | IT              |  65000 |
|   37 | Accounting      |  15000 |
|   59 | Human Resources | 240000 |
|   77 | Research        |  55000 |

* Employees

| SSN       | Name      | LastName  | Department |
|:---------:|:----------|:----------|:----------:|
| 123234877 | Michael   | Rogers    |         14 |
| 152934485 | Anand     | Manikutty |         14 |
| 222364883 | Carol     | Smith     |         37 |
| 326587417 | Joe       | Stevens   |         37 |
| 332154719 | Mary-Anne | Foster    |         14 |
| 332569843 | George    | ODonnell  |         77 |
| 546523478 | John      | Doe       |         59 |
| 631231482 | David     | Smith     |         77 |
| 654873219 | Zacary    | Efron     |         59 |
| 745685214 | Eric      | Goldsmith |         59 |
| 845657245 | Elizabeth | Doe       |         14 |
| 845657246 | Kumar     | Swamy     |         14 |

## 2.1 Sélectionnez le nom de famille de tous les employés.
```sql
SELECT  LastName from employees;
```
## 2.2 Sélectionnez le nom de famille de tous les employés, sans doublons.
```sql
SELECT distinct LastName FROM employees;
```
## 2.3 Sélectionnez toutes les données des employés dont le nom de famille est "Smith".
```sql
 SELECT * FROM employees WHERE LastName = 'Smith';
```
| SSN       | Name  | LastName | Department |
|:---------:|:------|:---------|:----------:|
| 222364883 | Carol | Smith    |         37 |
| 631231482 | David | Smith    |         77 |

## 2.4 Sélectionnez toutes les données des employés dont le nom de famille est "Smith" ou "Doe".

```sql
SELECT * FROM employees WHERE LastName IN ('Smith','Doe');
```
| SSN       | Name      | LastName | Department |
|:---------:|:----------|:---------|:----------:|
| 222364883 | Carol     | Smith    |         37 |
| 546523478 | John      | Doe      |         59 |
| 631231482 | David     | Smith    |         77 |
| 845657245 | Elizabeth | Doe      |         14 |

## 2.5 Sélectionnez toutes les données des employés qui travaillent dans le département 14.
```sql
SELECT * FROM employees WHERE Department = 14
```
## 2.6 Sélectionner toutes les données des employés qui travaillent dans le département 37 ou le département 77.
```sql
SELECT * FROM employees WHERE Department IN ('37', '77');
```
## 2.7 Sélectionner toutes les données des employés dont le nom de famille commence par un "S".
```sql
SELECT * FROM employees WHERE LastName LIKE('S%');
```
## 2.8 Sélectionner la somme des budgets de tous les départements.
```sql
SELECT SUM(Budget) FROM departments;
```
## 2.9 Sélectionnez le nombre d'employés dans chaque département (vous devez seulement indiquer le code du département et le nombre d'employés).

```sql
SELECT count(*), department FROM employees group by department;
```
## 2.10 Sélectionnez toutes les données des employés, y compris les données du département de chaque employé.

```sql
SELECT * FROM employees e inner join departments d  on e.Department = d.Code;
```
## 2.11 Sélectionnez le nom et le prénom de chaque employé, ainsi que le nom et le budget du département de l'employé.

```sql
SELECT e.name, e.LastName, d.Name, d.Budget FROM employees e join departments d on e.Department = d.Code;
```
## 2.12 Sélectionnez le nom et le nom de famille des employés travaillant pour des ministères dont le budget est supérieur à 60 000 $
```sql
SELECT name, LastName FROM employees WHERE Department IN (SELECT Code FROM departments WHERE Budget > 60000);

```
## 2.13 Sélectionnez les départements dont le budget est supérieur au budget moyen de l'ensemble des départements.

```sql
SELECT * FROM departments WHERE budget > (SELECT AVG(Budget) FROM departments);
```
## 2.14 Sélectionnez les noms des départements ayant plus de deux employés.

```sql
SELECT name FROM departments WHERE Code IN (SELECT department FROM employees group by department having count(*) > 2);

```
## 2.15 Très important - Sélectionnez le nom et le nom de famille des employés travaillant pour les ministères dont le budget est le deuxième plus bas.
```sql
SELECT e.Name, e.LastName FROM Employees e WHERE e.Department = (SELECT sub.Code FROM (SELECT * FROM Departments d ORDER BY d.budget LIMIT 2) sub ORDER BY budget DESC LIMIT 1);
```


## 2.16 Ajoutez un nouveau service appelé "Quality assurance", avec un budget de 40 000 $ et le code de service 11. Et ajoutez un employé appelé "Mary Moore" dans ce département, avec le code SSN 847-21-9811.
```sql
INSERT INTO departments values(11, 'Quality Assurance', 40000);
 INSERT INTO employees values(847219811, 'Mary', 'Moore', 11);
```
## 2.17 Réduire le budget de tous les départements de 10 %.
```sql
update departments set budget = 0.9 * budget;
```
## 2.18 Réaffecter tous les employés du département de la recherche (code 77) au département informatique (code 14).

```sql
 update employees set department = 14 WHERE department = 77;
```
## 2.19 Supprimer du tableau tous les employés du département informatique (code 14).

```sql
 DELETE FROM employees WHERE department = 14;
```
## 2.20 Supprimer du tableau tous les employés qui travaillent dans des départements dont le budget est supérieur ou égal à 60 000 $.

```sql
DELETE FROM employees WHERE 'departement' in (SELECT Code FROM departments WHERE Budget >= 60000 );
```
## 2.21 Supprimer du tableau tous les employés.
```sql
 delete from employees;
```



