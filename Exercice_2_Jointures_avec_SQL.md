### **Exercice : Jointure avec SQL** ###

Cet exercice est extrait de ce site : https://sqlzoo.net/wiki/The_JOIN_operation. 

<div align="center">
  <img src="https://github.com/user-attachments/assets/f54466de-466f-473d-acbc-d535eb7e7ee4" alt="Description de l'image" width="700"/>
</div>

**Les 3 tables avec les noms de leurs colonnes :**
> game : id, mdate, stadium, team1, team2\
> goal : matchid, teamid, player, gtime\
> eteam : id, teamname, coach\

**1.	Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for : teamid = 'GER'**

SELECT g.id, go.player\
FROM game g\
INNER JOIN goal go ON g.id = go.matchid\
WHERE go.teamid = 'GER'

**2. From the previous query you can see that Lars Bender's scored a goal in game 1012. Now we want to know what teams were playing in that match.**

**Notice in the that the column matchid in the goal table corresponds to the id column in the game table. We can look up information about game 1012 by finding that row in the game table. Show id, stadium, team1, team2 for just game 1012.**

SELECT id, stadium, team1, team2\
FROM game\
WHERE id = 1012


**3. The code below shows the player (from the goal) and stadium name (from the game table) for every goal scored.
Modify it to show the player, teamid, stadium and mdate for every German goal.**\
**Modifiez-le pour afficher le joueur, l'identifiant de l'équipe, le stade et la date de chaque but allemand.**

SELECT go.player, et.id, g.stadium, g.mdate\
FROM game g\
JOIN goal go ON g.id = go.matchid\
JOIN eteam et ON go.teamid = et.id\
WHERE go.teamid = 'GER'\


**4.	Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'\
Afficher l'équipe 1, l'équipe 2 et le joueur pour chaque but marqué par un joueur appelé Mario Player LIKE 'Mario%'**

SELECT g.team1, g.team2, go.player\
FROM game g INNER JOIN goal go ON g.id = go.matchid\
WHERE go.player LIKE 'Mario%'


**5.	The table eteam gives details of every national team including the coach. You can JOIN goal to eteam using the phrase goal JOIN eteam on teamid=id\
Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10. Afficher le joueur, l'identifiant de l'équipe, l'entraîneur et le temps g pour tous les buts marqués au cours des 10 premières minutes gtime <= 10**

SELECT go.player, go.teamid, et.coach, go.gtime\
FROM goal go INNER JOIN eteam et ON go.teamid = et.id\
WHERE go.gtime<=10


**6. To JOIN game with eteam you could use either game JOIN eteam ON (team1=eteam.id) or game JOIN eteam ON (team2=eteam.id)\
Notice that because id is a column name in both game and eteam you must specify eteam.id instead of just id
List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach\
Indiquez les dates des matchs et le nom de l'équipe dans laquelle « Fernando Santos » était l'entraîneur de l'équipe 1.**

SELECT DISTINCT g.mdate, et.teamname\
FROM game g INNER JOIN goal go ON g.id = go.matchid\
INNER JOIN eteam et ON g.team1 = et.id\
WHERE et.coach = 'Fernando Santos'

**7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'\
Indiquez le joueur pour chaque but marqué dans un match où le stade était le « Stade National de Varsovie »**

SELECT go.player\
FROM goal go JOIN game g ON go.matchid = g.id\
WHERE g.stadium = 'National Stadium, Warsaw'


**8. The example query shows all goals scored in the Germany-Greece quarterfinal.\
Instead show the name of all players who scored a goal against Germany.\
Affichez plutôt le nom de tous les joueurs qui ont marqué un but contre l'Allemagne. « teamid » vient de la table 'goal'**

**Version 1**

SELECT DISTINCT go.player\
FROM goal go JOIN game g ON go.matchid = g.id\
WHERE (g.team1='GER' AND go.teamid !='GER') OR\
               (g.team2='GER' AND go.teamid !='GER')\
               
**Version 2**
**Affichez plutôt le nom de tous les joueurs qui ont marqué un but contre l'Allemagne.**\

SELECT DISTINCT go.player\
FROM goal go JOIN game g ON go.matchid = g.id\
WHERE (g.team1='GER' OR g.team2='GER') AND go.teamid != 'GER'

**9.  Show teamname and the total number of goals scored.\
Afficher le nom de l'équipe et le nombre total de buts marqués**\

SELECT et.teamname, COUNT(go.teamid)\
FROM eteam et\
JOIN goal go ON et.id = go.teamid\
GROUP BY et.id\
ORDER BY teamname

**10. Show the stadium and the number of goals scored in each stadium.\
Affichez le stade et le nombre de buts marqués dans chaque stade.**

SELECT DISTINCT g.stadium, COUNT(go.teamid)\
FROM game g\
JOIN goal go ON g.id = go.matchid\
GROUP BY g.stadium

**11. For every match involving 'POL', show the matchid, date and the number of goals scored.
Pour chaque match impliquant « POL », indiquez l'identifiant du match, la date et le nombre de buts marqués**

SELECT go.matchid, g.mdate, count(go.teamid)\
FROM game g\
JOIN goal go ON g.id = go.matchid\
WHERE (g.team1 = 'POL' OR g.team2 = 'POL')\
GROUP BY go.matchid


**12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'\
Pour chaque match où « GER » a marqué, affichez l'identifiant du match, la date du match et le nombre de buts marqués par « GER »**

SELECT go.matchid, g.mdate, COUNT(go.teamid)\
FROM goal go\
JOIN game g ON go.matchid = g.id\
WHERE go.teamid = 'GER'\
GROUP BY go.matchid

**version**

SELECT g.mdate, g.team1, SUM(CASE WHEN g.team1 = go.teamid THEN 1 ELSE 0 END) AS score1, g.team2,\
  SUM(CASE WHEN g.team2 = go.teamid THEN 1 ELSE 0 END) AS score2\
FROM game g\
LEFT JOIN goal go ON g.id = go.matchid\
GROUP BY g.mdate, g.id, g.team1, g.team2\
ORDER BY g.mdate, g.id, g.team1, g.team2;




























