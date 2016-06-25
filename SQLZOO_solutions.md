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
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```
2.
```sql
SELECT name FROM world
  WHERE continent = 'Europe'
    AND gdp/population > (SELECT gdp/population
                            FROM world
                           WHERE name = 'United Kingdom')
```
3.
```sql
SELECT name, continent FROM world
  WHERE continent IN (SELECT continent FROM world
                        WHERE name IN ('Argentina','Australia'))
  ORDER BY name
```
4.
```sql
SELECT name, population FROM world
  WHERE population > (SELECT population FROM world
                        WHERE name = 'Canada')
    AND population < (SELECT population FROM world
                        WHERE name = 'Poland')
```
5.
```sql
SELECT name, CONCAT(ROUND(population/(SELECT population FROM world
                          WHERE name = 'Germany')*100,0),'%')
             FROM world WHERE continent = 'Europe'
```
6.
```sql
SELECT name FROM world
  WHERE gdp > ALL(SELECT gdp FROM world
                   WHERE gdp > 0 AND continent = 'Europe')
```
7.
```sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)
```
8.
```sql
SELECT continent, name FROM world x
  WHERE name <= ALL
    (SELECT name FROM world y
        WHERE y.continent=x.continent)
--Got this one to work.. but I'm still not quite sure what the variables are doing.
```
### Difficult Questions that use techniques not covered in previous sections...
9.
```sql
SELECT name, continent, population FROM world x
  WHERE 25000000 >= ALL(SELECT population
	                FROM world y
		        WHERE x.continent = y.continent
                        AND y.population>0);
```
10.
```sql
SELECT name, continent FROM world x
  WHERE population >= ALL(SELECT population*3
                         FROM world y
                         WHERE x.continent = y.continent
                         and y.name != x.name)
```
## SUM and COUNT
1.
```sql
SELECT SUM(population)
FROM world
```
2.
```sql
SELECT DISTINCT continent FROM world
```
3.
```sql
SELECT SUM(gdp) FROM world
  WHERE continent = 'Africa'
```
4.
```sql
SELECT COUNT(name) FROM world
  WHERE area >= 1000000
```
5.
```sql
SELECT SUM(population) FROM world
  WHERE name IN ('France','Germany','Spain')
```
6.
```sql
SELECT continent, COUNT(name) FROM world
GROUP BY continent
```
7.
```sql
SELECT continent, COUNT(name) FROM world
  WHERE population > 10000000
  GROUP BY continent
```
8.
```sql
SELECT continent FROM world
  GROUP BY continent
  HAVING SUM(population) > 100000000
```
## JOIN
1.
```sql
SELECT matchid, player FROM goal
  WHERE teamid = 'GER'
```
2.
```sql
SELECT id,stadium,team1,team2
  FROM game
  WHERE id = 1012
```
3.
```sql
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid)
  WHERE teamid = 'GER'
```
4.
```sql
SELECT team1, team2, player FROM game
  JOIN goal ON (id=matchid)
  WHERE player LIKE 'Mario%'
```
5.
```sql
SELECT player, teamid, coach, gtime
  FROM goal
  JOIN eteam on (teamid=id)
 WHERE gtime<=10
```
6.
```sql
SELECT mdate,teamname FROM game
  JOIN eteam ON (team1 = eteam.id)
  WHERE coach = 'Fernando Santos'
```
7.
```sql
SELECT player FROM goal
  JOIN game ON (matchid = id)
  WHERE stadium = 'National Stadium, Warsaw'
```
### More Difficult Questions....
8.
```sql
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id
    WHERE (team1= 'GER' OR team2='GER')
    AND teamid != 'GER'
```
9.
```sql
SELECT teamname, COUNT(*)
  FROM eteam JOIN goal ON id=teamid
 GROUP BY teamname
```
10.
```sql
SELECT stadium, COUNT(*) FROM goal
  JOIN game ON (matchid = id)
  GROUP BY stadium
```
11.
```sql
SELECT matchid, mdate, COUNT(*)
  FROM game JOIN goal ON matchid = id
  WHERE (team1 = 'POL' OR team2 = 'POL')
  GROUP BY mdate,matchid
```
12.
```sql
SELECT matchid, mdate, COUNT(*) FROM goal
  JOIN game ON (matchid=id)
  WHERE teamid = 'GER'
  GROUP BY matchid, mdate
```
13.
```sql
SELECT DISTINCT mdate, team1,
	SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
    team2,
    SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
FROM game
LEFT JOIN goal ON game.id = goal.matchid
GROUP BY id, mdate, team1, team2
ORDER BY mdate, matchid, team1, team2
```
## More JOIN
1.
```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```
2.
```sql
SELECT yr
  FROM movie
  WHERE title = 'Citizen Kane'
```
3.
```sql
SELECT id, title, yr FROM movie
  WHERE title LIKE '%Star Trek%'
  ORDER BY yr
```
4.
```sql
SELECT title FROM movie
  WHERE id IN (11768, 11955, 21191)
```
5.
```sql
SELECT id FROM actor
  WHERE name = 'Glenn Close'
```
6.
```sql
SELECT id FROM movie
  WHERE title = 'Casablanca'
```
7.
```sql
SELECT name FROM casting JOIN actor ON (id=actorid)
  WHERE movieid=11768
```
8.
```sql
SELECT name FROM casting
  JOIN actor ON (actor.id=actorid)
  JOIN movie ON (movie.id=movieid)
  WHERE title = 'Alien'
```
9.
```sql
SELECT title FROM casting
  JOIN movie ON (movie.id = movieid)
  JOIN actor ON (actor.id = actorid)
  WHERE name = 'Harrison Ford'
```
10.
```sql
SELECT title FROM casting
  JOIN movie ON (movie.id = movieid)
  JOIN actor ON (actor.id = actorid)
  WHERE name = 'Harrison Ford'  AND ord > 1
```
11.
```sql
SELECT title, name FROM casting
  JOIN movie ON (movie.id = movieid)
  JOIN actor ON (actor.id = actorid)
  WHERE yr = 1962 and ord = 1
```
### Harder Questions
12.
```sql
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
         JOIN actor   ON actorid=actor.id
WHERE name='John Travolta'
GROUP BY yr
HAVING COUNT(title)=(SELECT MAX(c) FROM
(SELECT yr,COUNT(title) AS c FROM
   movie JOIN casting ON movie.id=movieid
         JOIN actor   ON actorid=actor.id
 WHERE name='John Travolta'
 GROUP BY yr) AS t
)
```
13.
```sql
SELECT title, name FROM casting
  JOIN movie ON movie.id = movieid
  JOIN actor ON actor.id = actorid
WHERE ord = 1
	AND movie.id IN
	(SELECT movie.id FROM movie
	   JOIN casting ON movie.id = movieid
	   JOIN actor ON actor.id = actorid
           WHERE actor.name = 'Julie Andrews')
```
14.
```sql
SELECT DISTINCT name FROM casting
  JOIN movie ON movie.id = movieid
  JOIN actor ON actor.id = actorid
  WHERE actorid IN (
	SELECT actorid FROM casting
	  WHERE ord = 1
	  GROUP BY actorid
	  HAVING COUNT(actorid) >= 30)
ORDER BY name
```
15.
```sql
SELECT title, COUNT(actorid) FROM casting
  JOIN movie ON movieid = movie.id
  WHERE yr = 1978
  GROUP BY movieid, title
  ORDER BY COUNT(actorid) DESC
```
16.
```sql
SELECT DISTINCT name FROM casting
  JOIN actor ON actorid = actor.id
  WHERE name != 'Art Garfunkel'
	AND movieid IN (
		SELECT movieid
		FROM movie
		JOIN casting ON movieid = movie.id
		JOIN actor ON actorid = actor.id
		WHERE actor.name = 'Art Garfunkel'
)
```
## Using NULL
1.
```sql
SELECT name FROM teacher
  WHERE dept IS NULL
```
2.
```sql
SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)
```
3.
```sql
SELECT teacher.name, dept.name
 FROM teacher LEFT JOIN dept
           ON (teacher.dept=dept.id)
```
4.
```sql
SELECT teacher.name, dept.name
 FROM teacher RIGHT JOIN dept
           ON (teacher.dept=dept.id)
```
5.
```sql
SELECT teacher.name, COALESCE(teacher.mobile,'07986 444 2266')  FROM teacher
```
6.
```sql
SELECT teacher.name, COALESCE(dept.name,'None') FROM teacher
  LEFT JOIN dept ON teacher.dept = dept.id
```
7.
```sql
SELECT COUNT(name), COUNT(mobile) FROM teacher
```
8.
```sql
SELECT dept.name, COUNT(teacher.dept) FROM teacher
  RIGHT JOIN dept ON dept.id = teacher.dept
  GROUP BY dept.name
```
9.
```sql
SELECT name, CASE WHEN dept IN (1,2) THEN 'Sci'
                  ELSE 'Art'
                  END
                  FROM teacher
```
10.
```sql
SELECT name, CASE WHEN dept IN (1,2) THEN 'Sci'
                  WHEN dept = 3 THEN 'Art'
                  ELSE 'None'
                  END
                  FROM teacher
```
## Self JOIN
1.
```sql
SELECT DISTINCT COUNT(*) FROM stops
```
2.
```sql
SELECT id FROM stops
  WHERE name = 'Craiglockhart'
```
3.
```sql
SELECT id, name FROM stops JOIN route ON (stops.id = route.stop)
  WHERE num = 4
```
4.
```sql
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) = 2
```
5.
```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop = (SELECT id FROM stops WHERE name = 'London Road')
```
6.
```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' and stopb.name = 'London Road'
```
7.
```sql
SELECT a.company, a.num  
FROM route a, route b
WHERE a.num = b.num AND (a.stop = 115 AND b.stop = 137)
GROUP BY num;
```
8.
```sql
SELECT a.company, a.num
FROM route a
JOIN route b ON (a.company = b.company AND a.num = b.num)
JOIN stops stopa ON a.stop = stopa.id
JOIN stops stopb ON b.stop = stopb.id
WHERE stopa.name = 'Craiglockhart'
AND stopb.name = 'Tollcross';
```
9.
```sql
SELECT DISTINCT name, a.company, a.num
FROM route a
JOIN route b ON (a.company = b.company AND a.num = b.num)
JOIN stops ON a.stop = stops.id
WHERE b.stop = 53;
```
10.
```sql
SELECT a.num, a.company, stopb.name, c.num, c.company
FROM route a
JOIN route b ON (a.company = b.company AND a.num = b.num)
JOIN (route c JOIN route d ON (c.company = d.company AND c.num = d.num))
JOIN stops stopa ON a.stop = stopa.id
JOIN stops stopb ON b.stop = stopb.id
JOIN stops stopc ON c.stop = stopc.id
JOIN stops stopd ON d.stop = stopd.id
WHERE stopa.name = 'Craiglockhart'
	AND stopd.name = 'Sighthill'
	AND stopb.name = stopc.name
ORDER BY LENGTH(a.num), b.num, stopb.name, LENGTH(c.num), d.num;
```
