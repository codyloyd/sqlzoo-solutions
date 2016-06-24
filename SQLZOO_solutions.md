# SQLZOO Solutions
I've compiled the solutions to all of all 10 levels on the [SQLZOO Tutoral](http://sqlzoo.net/wiki/SQL_Tutorial).  

## SELECT basics
Some simple queries to get you started

1.
```
  SELECT population FROM world
    WHERE name = 'Germany'
```
2.
```
  SELECT name, gdp/population FROM world
    WHERE area > 5000000
```
3.
```
  SELECT name, population FROM world
    WHERE name IN ('Ireland','Iceland','Denmark');
```
4.
```
  SELECT name, area FROM world
    WHERE area BETWEEN 200000 AND 250000
```
## SELECT from WORLD Tutorial
1.
```
SELECT name, continent, population FROM world
```
2.
```
SELECT name FROM world
WHERE population>200000000
```
3.
```
SELECT name, gdp/population FROM world
  WHERE population > 200000000
```
4.
```
SELECT name, population/1000000 FROM world
  WHERE continent = 'South America'
```
5.
```
SELECT name,population FROM world
  WHERE name IN ('France','Germany','Italy')
```
6.
```
SELECT name FROM world
  WHERE name LIKE '%United%'
```
7.
```
select name, population, area from world
  where population > 250000000 or area > 3000000
```
8.
```
select name, population, area from world
  where population > 250000000 xor area > 3000000
```
9.
```
select name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2) from world
  where continent = 'South America'
```
10.
```
select name, ROUND(gdp/population,-3) from world
  where gdp > 1000000000000
```
### Harder Questions:
11.
```
SELECT name,
       CASE WHEN continent='Oceania' THEN 'Australasia'
            ELSE continent END
  FROM world
 WHERE name LIKE 'N%'
```
12.
```
SELECT name,
       CASE WHEN continent='Europe' or continent='Asia' THEN 'Eurasia'
            WHEN continent in ('North America','South America','Caribbean') THEN 'America'   
            ELSE continent END
  FROM world
 WHERE name LIKE 'A%' or name LIKE 'B%'
```
13.(this one was a doozy)

```
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
```
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```
2.
```
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature'
```
3.
```
SELECT yr, subject
  FROM nobel
WHERE winner = 'Albert Einstein'
```
4.
```
SELECT winner
FROM nobel
WHERE subject = 'Peace' AND yr >= 2000
```
5.
```
SELECT yr, subject, winner
  FROM nobel
WHERE subject = 'Literature' AND yr BETWEEN 1980 AND 1989
(in MySQL BETWEEN is inclusive.. this is not always the case)
```
6.
```
SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter')
```
7.
```
SELECT winner FROM nobel
  WHERE winner LIKE 'JOHN %'
```
8.
```
SELECT * FROM nobel
  WHERE yr = 1980 AND subject = 'Physics'
     OR yr = 1984 AND subject = 'Chemistry'
```
9.
```
SELECT * FROM nobel
  WHERE yr = 1980
    AND subject NOT IN ('Chemistry','Medicine')
```
10.
```
SELECT * FROM nobel
  WHERE yr < 1910 AND subject = 'Medicine'
     OR yr >= 2004 AND subject = 'Literature'
```
### Harder Questions
11.
```
SELECT * FROM nobel
  WHERE winner = 'Peter Grünberg'
```
12.
```
SELECT * FROM nobel
  WHERE winner = 'Eugene O''Neill'
```
13.
```

```
14.
```

```
