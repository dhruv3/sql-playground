# SQLZOO Notes and Problem Solution

## SELECT basics
### where clause
```sql
SELECT population FROM world
  WHERE name = 'Germany'
```

### IN clause
IN allows us to check if an item is in a list.
```sql
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

### BETWEEN clause
```sql
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```
### LIKE clause and wildcard
Select the code which shows the countries that end in A or L
```sql
SELECT name FROM world
 WHERE name LIKE '%a' OR name LIKE '%l'
```
### length operation
```sql
SELECT name,length(name)
FROM world
WHERE length(name)=5 and region='Europe'
```
### multiplication operation
```sql
SELECT name, area*2 FROM world WHERE population = 64000
```
### division operation
```sql
SELECT name, population/area
  FROM world
 WHERE name IN ('China', 'Nigeria', 'France', 'Australia')
 ```
