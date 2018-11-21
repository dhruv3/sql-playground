# SQLZOO Notes and Problem Solution

## Lesson 1: SELECT basics
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
## Lesson 2: SELECT from WORLD Tutorial
### round operation
```sql
select name, ROUND(population/1000000, 2), ROUND(gdp/1000000000, 2)
from world
where continent = 'South America'
 ```
Syntax:

`ROUND ( numeric_expression , length [ ,function ] )`

When length is a positive number, numeric_expression is rounded to the number of decimal positions specified by length. When length is a negative number, numeric_expression is rounded on the left side of the decimal point, as specified by length.
```sql
select name, ROUND(gdp/population, -3)
from world
where gdp > 1000000000000
```
### LEFT function
LEFT(s,n) allows you to extract n characters from the start of the string s.
```sql
LEFT('Hello world', 4) -> 'Hell'
```
