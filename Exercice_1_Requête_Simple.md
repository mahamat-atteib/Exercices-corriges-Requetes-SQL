### **Exercice 1 : requête simple** ###

Ces requêtes simples utilisent également les fonctions SUM et COUNT.\
Cet exercice est extrait de ce site : https://sqlzoo.net/wiki/SUM_and_COUNT.\
Ci-dessous un aperçu de la table "world"

<div align="center">
  <img src="https://github.com/user-attachments/assets/41d7e3bd-6b7c-4336-8c93-9fd2eaffb730" alt="Description de l'image" width="400"/>
</div>

**1.	Show the total population of the world.**\
SELECT SUM(population)\
FROM world

**2.	List all the continents - just once each.**\
SELECT DISTINCT continent\
FROM world

**3.	Give the total GDP of Africa**\
SELECT SUM(gdp)\
FROM world\
WHERE continent = 'Africa'

**4.	How many countries have an area of at least 1000000**\
SELECT count(name)\
FROM world\
WHERE area > 1000000

**5. What is the total population of ('Estonia', 'Latvia', 'Lithuania')**\
SELECT SUM(population) as population_de_trois_pays\
FROM world\
WHERE name in ('Estonia', 'Latvia', 'Lithuania')

**6. For each continent show the continent and number of countries.**\
SELECT continent, count(name)\
FROM world\
GROUP BY continent

**7.	For each continent show the continent and number of countries with populations of at least 10 million.**\
SELECT continent, count(name)\
FROM world\
WHERE population >= 10000000\
GROUP BY continent

**8.	List the continents that have a total population of at least 100 million.**\
SELECT continent FROM world\
GROUP BY continent\
HAVING SUM(population) > 100000000

















