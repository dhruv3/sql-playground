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
## Lesson 3: SELECT from NAME tutorial
### ORDER BY clause
Default ORDER BY is `asc`
```sql
select winner, yr, subject
from nobel
where winner like 'Sir%'
order by yr desc, winner
```
**Note:** The expression `subject IN ('Chemistry','Physics')` can be used as a value - it will be `0` or `1`.
### ORDER BY CASE clause
```sql
SELECT * FROM Country
ORDER BY CASE WHEN cname='other' THEN 1 ELSE 0 END
```
Applying ORDER BY clause with CASE tweaks the "Other" option and places it at the bottom.
## Lesson 4: SELECT within SELECT Tutorial
### CONCAT
```sql
select name, CONCAT(ROUND(population*100/(select population from world where name = 'Germany'),0), '%')
from world
where continent = 'Europe'
```
There can be more than 2 args for `CONCAT` function.
### ALL Clause
```sql
SELECT name
  FROM world
 WHERE population >= ALL(SELECT population
                           FROM world
                          WHERE population>0)
```
The word `ALL` to allow >= or > or < or <= to act over a **list**.
### Correlated Subqueries
A correlated subquery works like a nested loop: the subquery only has access to rows related to a single record at a time in the outer query. The technique relies on table aliases to identify two different uses of the same table, one in the outer query and the other in the subquery.

One way to interpret the line in the WHERE clause that references the two table is “… where the correlated values are the same”.

In the example provided, you would say “select the country details from world where the population is greater than or equal to the population of all countries where the continent is the same”.
```sql
SELECT continent, name, population FROM world x
  WHERE population >= ALL
    (SELECT population FROM world y
        WHERE y.continent=x.continent
          AND population>0)
```
## Lesson 5: SUM and COUNT
The functions `SUM`, `COUNT`, `MAX` and `AVG` are "aggregates", each may be applied to a **numeric attribute** resulting in a single row being returned by the query. (These functions are even more useful when used with the `GROUP BY` clause.)

By including a `GROUP BY` clause, functions such as `SUM` and `COUNT` are applied to groups of items sharing values. When you specify `GROUP BY` continent the result is that you get only one row for each different value of continent. All the other columns must be **"aggregated"** by one of SUM, COUNT ...

The `WHERE` filter takes place before the aggregating function.

The `HAVING` clause is tested after the `GROUP BY`. The `HAVING` clause allows us to filter the groups which are displayed. The `WHERE` clause filters rows before the aggregation, the `HAVING` clause filters after the aggregation.
```sql
SELECT continent, SUM(population)
  FROM world
 GROUP BY continent
HAVING SUM(population)>500000000
```

**Problem:** Show the number of different winners for each subject.
```sql
select subject, count(distinct winner)
from nobel
group by subject
```
## Lesson 6: JOIN
```sql
SELECT *
  FROM game JOIN goal ON (id=matchid)
```
The **FROM** clause says to merge data from the goal table with that from the game table. The **ON** says how to figure out which rows in **game** go with which rows in **goal** - the **matchid** from **goal** must match **id** from **game**.

**Problem:** For every match involving 'POL', show the matchid, date and the number of goals scored.
```sql
SELECT matchid,mdate, count(team1)
FROM game JOIN goal ON matchid = id 
WHERE (team1 = 'POL' OR team2 = 'POL')
group by mdate,matchid
```
