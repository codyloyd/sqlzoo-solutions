# SQLZOO Solutions
I've compiled the solutions to all of all 10 levels on the [SQLZOO Tutoral](http://sqlzoo.net/wiki/SQL_Tutorial).  

## Sections:
1. [SELECT basics](#select-basics)
2. [SELECT from WORLD](#select-from-world)
3. [SELECT from NOBEL](#select-from-nobel)
4. [SELECT in SELECT](#select-in-select)
5. [SUM and COUNT](#sum-and-count)
6. [JOIN](#join)
7. [More JOIN](#more-join)
8. [Using NULL](#using-null)
9. [Self JOIN](#self-join)

## SELECT basics
Some simple queries to get you started

1.
```sql
  SELECT population FROM world
    WHERE name = 'Germany'
```
2.
```sql
  SELECT name, gdp/population FROM world
    WHERE area > 5000000
```
3.
```sql
  SELECT name, population FROM world
    WHERE name IN ('Ireland','Iceland','Denmark');
```
4.
```sql
  SELECT name, area FROM world
    WHERE area BETWEEN 200000 AND 250000
```
## SELECT from WORLD
1.
```sql
SELECT name, continent, population FROM world
```
2.
```sql
SELECT name FROM world
WHERE population>200000000
```
3.
```sql
SELECT name, gdp/population FROM world
  WHERE population > 200000000
```
4.
```sql
SELECT name, population/1000000 FROM world
  WHERE continent = 'South America'
```
5.
```sql
SELECT name,population FROM world
  WHERE name IN ('France','Germany','Italy')
```
6.
```sql
SELECT name FROM world
  WHERE name LIKE '%United%'
```
7.
```sql
select name, population, area from world
  where population > 250000000 or area > 3000000
```
8.
```sql
select name, population, area from world
  where population > 250000000 xor area > 3000000
```
9.
```sql
select name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2) from world
  where continent = 'South America'
```
10.
```sql
select name, ROUND(gdp/population,-3) from world
  where gdp > 1000000000000
```
### Harder Questions:
11.
```sql
SELECT name,
       CASE WHEN continent='Oceania' THEN 'Australasia'
            ELSE continent END
  FROM world
 WHERE name LIKE 'N%'
```
12.
```sql
SELECT name,
       CASE WHEN continent='Europe' or continent='Asia' THEN 'Eurasia'
            WHEN continent in ('North America','South America','Caribbean') THEN 'America'   
            ELSE continent END
  FROM world
 WHERE name LIKE 'A%' or name LIKE 'B%'
```
13.(this one was a doozy)

```sql
SELECT name, continent, CASE
                     WHEN continent = 'Oceania' THEN 'Australasia'
                     WHEN continent = 'Eurasia' THEN 'Europe/Asia'
                     WHEN name = 'Turkey' THEN 'Europe/Asia'
    WHEN continent = 'Caribbean' AND name LIKE 'B%' then 'North America'
    WHEN continent = 'Caribbean' THEN 'South America'    
                 ELSE continent END
FROM world ORDER BY name
```

## SELECT from NOBEL
1.
```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```
2.
```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```
3.
```sql
SELECT yr, subject
  FROM nobel
WHERE winner = 'Albert Einstein'
```
4.
```sql
SELECT winner
FROM nobel
WHERE subject = 'Peace' AND yr >= 2000
```
5.
```sql
SELECT yr, subject, winner
  FROM nobel
WHERE subject = 'Literature' AND yr BETWEEN 1980 AND 1989
(in MySQL BETWEEN is inclusive.. this is not always the case)
```
6.
```sql
SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter')
```
7.
```sql
SELECT winner FROM nobel
  WHERE winner LIKE 'JOHN %'
```
8.
```sql
SELECT * FROM nobel
  WHERE yr = 1980 AND subject = 'Physics'
     OR yr = 1984 AND subject = 'Chemistry'
```
9.
```sql
SELECT * FROM nobel
  WHERE yr = 1980
    AND subject NOT IN ('Chemistry','Medicine')
```
10.
```sql
SELECT * FROM nobel
  WHERE yr < 1910 AND subject = 'Medicine'
     OR yr >= 2004 AND subject = 'Literature'
```
### Harder Questions
11.
```sql
SELECT * FROM nobel
  WHERE winner = 'Peter Grünberg'
```
12.
```sql
SELECT * FROM nobel
  WHERE winner = 'Eugene O''Neill'
```
13.
```sql
SELECT winner, yr, subject FROM nobel
  WHERE winner LIKE 'Sir %'
  ORDER BY yr DESC, winner
```
14.
```sql
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject in ('Chemistry','Physics'), subject, winner
```
## SELECT in SELECT
1.
```sql

```
2.
```sql

```
3.
```sql

```
4.
```sql

```
5.
```sql

```
6.
```sql

```
7.
```sql

```
8.
```sql

```
### Difficult Questions that use techniques not covered in previous sections...
9.
```sql

```
10.
```sql

```
## SUM and COUNT
1.
```sql

```
2.
```sql

```
3.
```sql

```
4.
```sql

```
5.
```sql

```
6.
```sql

```
7.
```sql

```
8.
```sql

```
9.
```sql

```
10.
```sql

```
## JOIN
1.
```sql

```
2.
```sql

```
3.
```sql

```
4.
```sql

```
5.
```sql

```
6.
```sql

```
7.
```sql

```
8.
```sql

```
9.
```sql

```
10.
```sql

```
## More JOIN
1.
```sql

```
2.
```sql

```
3.
```sql

```
4.
```sql

```
5.
```sql

```
6.
```sql

```
7.
```sql

```
8.
```sql

```
9.
```sql

```
10.
```sql

```
## Using NULL
1.
```sql

```
2.
```sql

```
3.
```sql

```
4.
```sql

```
5.
```sql

```
6.
```sql

```
7.
```sql

```
8.
```sql

```
9.
```sql

```
10.
```sql

```
## Self JOIN
1.
```sql

```
2.
```sql

```
3.
```sql

```
4.
```sql

```
5.
```sql

```
6.
```sql

```
7.
```sql

```
8.
```sql

```
9.
```sql

```
10.
```sql

```
