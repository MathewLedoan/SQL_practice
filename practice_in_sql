-- # 1. Show all details of the presidential winners:
Theodore Roosevelt
Woodrow Wilson
Jimmy Carter
Barack Obama
SELECT * FROM nobel
 WHERE winner IN ('Theodore Roosevelt',
                  'Woodrow Wilson',
                  'Jimmy Carter',
'Barack Obama')

-- # 2. Show the winners with first name John
SELECT winner
FROM nobel
WHERE winner LIKE 'John%'

-- # 3. Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984.
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'Physics' AND yr = 1980)
OR (subject = 'Chemistry' AND yr = 1984);

-- # 4. Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine
SELECT *
FROM nobel
WHERE yr = 1980
AND subject != 'Chemistry' AND subject != 'Medicine';

-- # 5. Find all details of the prize won by EUGENE O'NEILL

SELECT *
FROM nobel
WHERE winner = 'eugene o'’neill'

-- # 6. List the winners, year and subject where the winner starts with Sir. Show the most recent first, then by name order.
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'sir%'
ORDER BY yr DESC, winner

-- # 7. The expression subject IN ('Chemistry','Physics') can be used as a value - it will be 0 or 1.
Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY  subject IN ('Chemistry','Physics'),subject,winner


-- # 8. Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get the population in millions.

SELECT name, population/1000000 AS 'Million'
FROM world
WHERE continent = 'South America';

-- # 9. Show the countries which have a name that includes the word 'United'
SELECT name
FROM world
WHERE name LIKE '%United%';

-- # 10. Exclusive OR (XOR). Show the countries that are big by area or big by population but not both. Show name, population, and area.
-- # Australia has a big area but a small population, it should be included.
-- #  Indonesia has a big population but a small area, it should be included.
-- # China has a big population and big area, it should be excluded.
-- # The United Kingdom has a small population and a small area, it should be excluded.
SELECT name, population, area
FROM world
WHERE area > 3000000 XOR population > 250000000;

-- # 11. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
-- # For South America show the population in millions and GDP in billions both to 2 decimal places.
-- # Millions and billions

SELECT name, ROUND(population/1000000, 2), ROUND(GDP/1000000000, 2)
FROM world
WHERE continent = 'South America';

-- # 12. Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.
-- # Show per-capita GDP for the trillion dollar countries to the nearest $1000.
SELECT name, ROUND(GDP/population, -3)
FROM world
WHERE GDP >= 1000000000000;

-- # 13. Greece has capital Athens.
-- # Each of the strings 'Greece', and 'Athens' has 6 characters.
-- # Show the name and capital where the name and the capital have the same number of characters.
-- # You can use the LENGTH function to find the number of characters in a string

SELECT name, capital
  FROM world
 WHERE LENGTH(name) = LENGTH(capital)

-- # 12. The capital of Sweden is Stockholm. Both words start with the letter 'S'.
-- # Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.
-- # You can use the function LEFT to isolate the first character.
-- # You can use <> as the NOT EQUALS operator.
SELECT name, capital
FROM world
WHERE LEFT(name,1) = LEFT(capital, 1)
AND
name <> capital;

-- # 13. Equatorial Guinea and the Dominican Republic have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name.
-- # Find the country that has all the vowels and no spaces in its name.
-- # You can use the phrase name NOT LIKE '%a%' to exclude characters from your results.
-- # The query shown misses countries like Bahamas and Belarus because they contain at least one 'a'
SELECT name
FROM world
WHERE name LIKE '%a%' AND name LIKE '%e%' AND name LIKE '%i%' AND name LIKE '%o%' AND name LIKE '%u%' AND 
name NOT LIKE '% %';

-- # 14. Pick the code that shows the amount of years where no Medicine awards were given

SELECT COUNT(DISTINCT yr) FROM nobel
 WHERE yr NOT IN (SELECT DISTINCT yr FROM nobel WHERE subject = 'Medicine')

-- # 15. Select the code that shows how many Chemistry awards were given between 1950 and 1960
SELECT COUNT(subject) FROM nobel
 WHERE subject = 'Chemistry'
   AND yr BETWEEN (1950, 1960)
   
-- #16. Pick the code that shows the amount of years where no Medicine awards were given
SELECT COUNT(DISTINCT yr) FROM nobel
 WHERE yr NOT IN (SELECT DISTINCT yr FROM nobel WHERE subject = 'Medicine')

-- # 17. Select the code which would show the year when neither a Physics or Chemistry award was given
SELECT yr FROM nobel
 WHERE yr NOT IN(SELECT yr 
                   FROM nobel
                 WHERE subject IN ('Chemistry','Physics'))

-- # 18. Select the code which shows the years when a Medicine award was given but no Peace or Literature award was


SELECT DISTINCT yr
  FROM nobel
 WHERE subject='Medicine' 
   AND yr NOT IN(SELECT yr FROM nobel 
                  WHERE subject='Literature')
   AND yr NOT IN (SELECT yr FROM nobel
                   WHERE subject='Peace')
-- # 19. List each country name where the population is larger than that of 'Russia'.

SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')

-- # 20. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.
-- # Per Capita GDP
-- # The per capita GDP is the gdp/population
SELECT name FROM world
WHERE GDP/population > (SELECT GDP/population FROM world WHERE name = 'United Kingdom')
AND continent = 'Europe'

-- # 21. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.
SELECT name, continent
FROM world
WHERE continent IN (SELECT continent FROM world WHERE name IN ('Argentina', 'Australia'))
ORDER by name

-- # 22. Which country has a population that is more than Canada but less than Poland? Show the name and the population.
SELECT a.name country, a.population
FROM world a
WHERE a.population >
(SELECT b.population
FROM world b
WHERE b.name = 'Canada')
AND a.population <
(SELECT c.population
FROM world c
WHERE c.name = 'Poland')

-- # 23. Germany (population 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany.
-- # Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.
-- # Decimal places
-- # You can use the function ROUND to remove the decimal places.
-- # Percent symbol %
-- # You can use the function CONCAT to add the percentage symbol.
SELECT name,
   CONCAT(ROUND(100*population/(SELECT population FROM world WHERE name='Germany')),'%')
FROM world
WHERE continent='Europe'

-- # We can use the word ALL to allow >= or > or < or <=to act over a list. For example, you can find the largest country in the world, by population with this query:
SELECT name
  FROM world
 WHERE population >= ALL(SELECT population
                           FROM world
                          WHERE population>0)

-- # 24. Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)
SELECT name
FROM world
WHERE gdp >= ALL(SELECT gdp FROM world WHERE continent = 'Europe' and gdp > 0) AND
continent != 'Europe'

-- # 25. Find the largest country (by area) in each continent, show the continent, the name and the area:
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent
          AND area>0)

-- # 25. List each continent and the name of the country that comes first alphabetically.
SELECT continent,name FROM world x
  WHERE x.name <= ALL (
    SELECT name FROM world y
     WHERE x.continent=y.continent)

-- # 26. Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.
SELECT x.name, x.continent
FROM world AS x
WHERE x.population/3 > ALL (
  SELECT y.population
  FROM world AS y
  WHERE x.continent = y.continent
  AND x.name != y.name);

-- # 27. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent, and population.
SELECT x.name, x.continent, x.population
FROM world AS x
WHERE 25000000 > ALL (
  SELECT y.population
  FROM world AS y
  WHERE x.continent = y.continent)

-- # 28. For each continent show the continent and number of countries.
SELECT continent, COUNT(name)
FROM world
GROUP BY continent

-- # 29. For each continent show the continent and the number of countries with populations of at least 10 million.
SELECT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent

-- # 30. List the continents that have a total population of at least 100 million.
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000;

-- # 31. List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.
-- # Notice in the query given every goal is listed. If it was a team1 goal then a 1 appears in score1, otherwise there is a 0. You could SUM this column to get a count of the goals scored by team1. Sort your result by mdate, matchid, team1 and team2.
SELECT mdate, 
	   team1, 
	   SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) AS score1, 
	   team2, 
	   SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score2 FROM
	game LEFT JOIN goal ON (id = matchid)
	GROUP BY mdate, matchid, team1, team2

-- # 32. The example query shows all goals scored in the Germany-Greece quarterfinal.
-- # Instead show the name of all players who scored a goal against Germany.
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id 
    WHERE (team1='GER' OR team2='GER')
AND teamid <>'GER'

-- # 33. For every match involving 'POL', show the matchid, date and the number of goals scored.
SELECT id, mdate, COUNT(*)
FROM game
JOIN goal
ON id = matchid
WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY id, mdate

-- # 34. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'
SELECT id, mdate, COUNT(*)
FROM game
JOIN goal
ON id = matchid
WHERE (teamid ='GER')
GROUP BY id, mdate


