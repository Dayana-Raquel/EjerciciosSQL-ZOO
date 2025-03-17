# SQL ZOO - Ejercicios Resueltos

## 1. SELECT BASICS

### 1.1. Listado de Países y Poblaciones
Modifica para mostrar la población de Alemania:
```sql
SELECT population FROM world
WHERE name = 'Germany';
```

### 1.2. Escandinavia
Mostrar el nombre y la población para 'Sweden', 'Norway' y 'Denmark':
```sql
SELECT name, population FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

### 1.3. El Tamaño Justo
Modifica para mostrar el país y el área de los países con un área entre 200,000 y 250,000:
```sql
SELECT name, area FROM world
WHERE area BETWEEN 200000 AND 250000;
```

---
## 2. SELECT FROM WORLD

### 2.1. Introducción
Lee las notas sobre esta tabla. Observa el resultado de ejecutar este comando SQL para mostrar el nombre, el continente y la población de todos los países:
```sql
SELECT name, continent, population FROM world;
```

### 2.2. Países Grandes
Cómo usar WHERE para filtrar registros. Muestra el nombre de los países con una población de al menos 200 millones (200000000):
```sql
SELECT name FROM world
WHERE population >= 200000000;
```

### 2.3. PIB Per Cápita
Indique el nombre y el PIB per cápita de los países con una población de al menos 200 millones:
```sql
SELECT name, gdp/population
FROM world
WHERE population >= 200000000;
```

### 2.4. Sudamérica en Millones
Mostrar el nombre y la población en millones para los países del continente 'South America':
```sql
SELECT name, population/1000000
FROM world
WHERE continent = 'South America';
```

### 2.5. Francia, Alemania, Italia
Mostrar el nombre y la población para Francia, Alemania e Italia:
```sql
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

### 2.6. Unidos
Mostrar los países que tengan un nombre que incluya la palabra 'United':
```sql
SELECT name
FROM world
WHERE name LIKE '%United%';
```

### 2.7. Dos Maneras de Ser Grande
Un país es grande si tiene una superficie de más de 3 millones de km² o una población de más de 250 millones:
```sql
SELECT name, population, area
FROM world
WHERE area >= 3000000 OR population >= 250000000;
```

### 2.8. Uno o el Otro (pero no Ambos)
Mostrar los países con mayor superficie (más de 3 millones) o mayor población (más de 250 millones), pero no ambos:
```sql
SELECT name, population, area
FROM world
WHERE (area > 3000000 AND population <= 250000000) 
   OR (population > 250000000 AND area <= 3000000);
```

### 2.9. Redondeo
Mostrar el nombre, la población en millones y el PIB en miles de millones de los países del continente 'South America':
```sql
SELECT name, ROUND(population / 1000000, 2), 
       ROUND(gdp / 1000000000, 2)
FROM world
WHERE continent = 'South America';
```

### 2.10. Economías de Billones de Dólares
Mostrar el PIB per cápita de los países con un PIB de al menos un billón, redondeado al millar más cercano:
```sql
SELECT name, ROUND(gdp / population, -3)
FROM world
WHERE gdp >= 1000000000000;
```

### 2.11. Nombre y Capital con la Misma Longitud
```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

### 2.12. Coincidir Nombre y Capital
Mostrar el nombre y la capital donde coincidan las primeras letras de cada una:
```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1)
AND name <> capital;
```

### 2.13. Todas las Vocales
Encontrar el país que tiene todas las vocales y ningún espacio en el nombre:
```sql
SELECT name
FROM world
WHERE name LIKE '%a%' AND name LIKE '%e%' 
AND name LIKE '%i%' AND name LIKE '%o%' 
AND name LIKE '%u%' AND name NOT LIKE '% %';
```

---
## 3. SELECT FROM NOBEL

### 3.1. Ganadores de 1950
 Cambia la consulta mostrada para que muestre los premios Nobel de 1950
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```

### 3.2. Literatura de 1962
Mostrar quien ganó el premio de literatura en 1962
```sql
SELECT winner
FROM nobel
WHERE yr = 1962 AND subject = 'Literature';
```

### 3.3. Albert Einstein
Mostrar el año y la materia que ganó 'Albert Einstein' su premio
```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

### 3.4. Premios Nobel de la Paz Recientes
Dar el nombre de los ganadores de la "paz" desde el año 2000, incluido el 2000.
```sql
SELECT winner
FROM nobel
WHERE yr >= 2000 AND subject = 'Peace';
```

### 3.5. Literatura en los 80s
Mostrar todos los detalles (año, tema, ganador) de los ganadores del premio literario entre 1980 y 1989 inclusive.      
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr BETWEEN 1980 AND 1989 AND subject = 'Literature';
```

### 3.6. Solo Presidentes
Muestra todos los detalles de los presidentes ganadores:
Theodore Roosevelt, Thomas Woodrow Wilson, Jimmy Carter, Barack Obama
```sql
SELECT *
FROM nobel
WHERE winner IN ('Theodore Roosevelt', 'Thomas Woodrow Wilson', 'Jimmy Carter', 'Barack Obama');
```

### 3.7. Ganadores con el Primer Nombre 'John'
Muestra los ganadores con el primer nombre John
```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John %';
```

### 3.8. Química y Física de Diferentes Años
Mostrar el año, materia y el nombre de los ganadores de física por el 1980 junto con los ganadores de química por el 1984
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'Physics' AND yr = 1980) 
   OR (subject = 'Chemistry' AND yr = 1984);
```

### 3.9. Excluir Químicos y Médicos
Mostrar el año, materia y el nombre de los ganadores de 1980 excluyendo química y medicina
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980 AND subject NOT IN ('Chemistry', 'Medicine');
```

### 3.10. Medicina Temprana, Literatura Tardía
Mostrar el año, materia y nombre de las personas que ganaron un premio de 'Medicina' en un año temprano(antes de 1910, no excluir 1910) junto con los ganadores de un premio de 'Literatura' en un año posterior (después de 2004, incluido 2004)
```sql
SELECT yr, subject, winner
FROM nobel
WHERE (subject = 'Medicine' AND yr < 1910) 
   OR (subject = 'Literature' AND yr >= 2004);
```

### 3.11. Metafonía
Encuentra todos los detalles del premio ganado por PETER GRÜNBERG
```sql
SELECT *
FROM nobel
WHERE winner = 'Peter Grünberg';
```

### 3.12. Apóstrofe
Encuentra todos los detalles del premio ganado por EUGENE O'NEILL
```sql
SELECT *
FROM nobel
WHERE winner = 'Eugene O''Neill';
```

### 3.13. Caballeros del Reino
Listar los ganadores, año y materia cuando el ganador empieza con Sir. Muestra primero el más reciente y luego el orden del nombre
```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir %'
ORDER BY yr DESC, winner ASC;
```

### 3.14. Química y Física al Final
La expresión Subject IN ('química','física') puede usarse como valor; será 0 o 1.
                Mostrar los ganadores y la asignatura de 1984 ordenados por asignatura y nombre del ganador; pero incluir química y física al final.
```sql
SELECT winner, subject 
FROM nobel 
WHERE yr = 1984 
ORDER BY 
  CASE 
    WHEN subject IN ('chemistry', 'physics') THEN 1
    ELSE 0  
  END, subject, winner;
```
------------------------------------------------------------------------

## 4. SELECT IN SELECT

### 4.1. Más grande que Rusia
List each country name where the population is larger than that of 'Russia'.

                world(name, continent, area, population, gdp)

```sql
SELECT name FROM world
WHERE population >
(SELECT population FROM world
WHERE name='Russia')
```

### 4.2. Más rico que el Reino Unido
Muestra los países europeos con un PIB per cápita superior al del Reino Unido.
```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND (gdp / population) > 38555.0739
```

### 4.3. Vecinos de Argentina y Australia
Listar el nombre y el continente de los países que contienen a Argentina o Australia. Ordena por nombre del país.
```sql
SELECT name, continent
FROM world
WHERE continent IN (SELECT continent FROM world WHERE name IN ('Argentina', 'Australia')
)
ORDER BY name;
```

### 4.4. Entre Canadá y Polonia
¿Qué país tiene una población mayor que la del Reino Unido pero menor que la de Alemania? Indica el nombre y la población.
```sql
SELECT name, population
FROM world
WHERE population > (SELECT population FROM world WHERE name = 'United Kingdom')
  AND population < (SELECT population FROM world WHERE name = 'Germany');
```

### 4.5. Porcentajes de Alemania
Alemania (con una población aproximada de 80 millones) es el país más poblado de Europa. Austria (con una población de 8,5 millones) representa el 11 % de la población de Alemania.
Muestre el nombre y la población de cada país europeo. Muestre la población como porcentaje de la población de Alemania.
```sql
SELECT name, 
CONCAT(ROUND((population / (SELECT population FROM world WHERE name = 'Germany')) * 100, 0), '%') AS percentage
FROM world
WHERE continent = 'Europe';
```

### 4.6. Más grande que todos los países de Europa
¿Qué países tienen un PIB mayor que todos los países de Europa? [Indique solo el nombre.] (Algunos países pueden tener valores de PIB nulos).
```sql
SELECT name
FROM world
WHERE gdp > (SELECT MAX(gdp) FROM world WHERE continent = 'Europe' AND gdp IS NOT NULL);
```

### 4.7. El más grande de cada continente
Encuentre el país más grande (por área) de cada continente, muestre el continente, su nombre y su área:
```sql
SELECT continent, name, area
  FROM world x
 WHERE area >= ALL
       (SELECT area
          FROM world y
         WHERE y.continent = x.continent
           AND area > 0);
```

### 4.8. El primero de los países de cada continente alfabéticamente
Enumere cada continente y el nombre del país que aparece primero en orden alfabético.
```sql
SELECT continent, name
FROM world x
WHERE name = (SELECT MIN(name) FROM world y WHERE y.continent = x.continent);
```

### 4.9. Preguntas difíciles que utilizan técnicas no cubiertas en secciones anteriores
Encuentre los continentes donde todos los países tienen una población <= 25000000. Luego, encuentre los nombres de los países asociados a estos continentes. Muestre el nombre, el continente y la población.
```sql
SELECT name, continent, population
FROM world
WHERE continent IN (
SELECT continent
FROM world
GROUP BY continent
HAVING MAX(population) <= 25000000
 );
```

### 4.10. Tres veces más grande
Algunos países tienen poblaciones tres veces mayores que la de sus vecinos (en el mismo continente). Indica los países y continentes.
```sql
SELECT a.name, a.continent
FROM world a
WHERE a.population > 3 * (
SELECT MAX(b.population)
FROM world b
WHERE a.continent = b.continent
AND a.name != b.name
 );
```

## 5. SUM AND COUNT

### 5.1. Población mundial total
Muestra la población mundial total.
```sql
SELECT SUM(population) 
FROM world;
```

### 5.2. Lista de continentes
Enumera todos los continentes, solo una vez cada uno.
```sql
SELECT DISTINCT continent 
FROM world;
```

### 5.3. PIB de África
Indique el PIB total de África.
```sql
SELECT SUM(gdp) 
FROM world 
WHERE continent = 'Africa';
```

### 5.4. Cuente los países grandes.
¿Cuántos países tienen una superficie de al menos 1 millón de habitantes?
```sql
SELECT COUNT(*) 
FROM world 
WHERE area >= 1000000;
```

### 5.5. Población de los países bálticos
¿Cuál es la población total de ('Estonia', 'Letonia', 'Lituania')?
```sql
SELECT SUM(population) 
FROM world 
WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```

### 5.6. Conteo de países en cada continente.
Para cada continente, muestra el continente y el número de países.
```sql
SELECT continent, COUNT(name) AS country_count
FROM world
GROUP BY continent;
```

### 5.7. Contando los países grandes en cada continente
Para cada continente, muestre el continente y el número de países con poblaciones de al menos 10 millones.
```sql
SELECT continent, COUNT(name) AS big_countries
FROM world
WHERE population >= 10000000
GROUP BY continent;
```

### 5.8. Contando continentes grandes
Enumere los continentes que tienen una población total de al menos 100 millones.
```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) >= 100000000;
```

### 6. JOIN

### 6.1. 
Modifíquelo para mostrar el matchid y el nombre del jugador de todos los goles de Alemania. Para identificar a los jugadores alemanes, busque: teamid = 'GER'.
```sql
SELECT matchid, player 
FROM goal 
WHERE teamid = 'GER';
```

### 6.2. 
Mostrar "id", "stadium", "team1", "team2" solo para el partido 1012.
```sql
SELECT id, stadium, team1, team2
FROM game
WHERE id = 1012;
```

### 6.3.
Modifícalo para que muestre el jugador, el teamid, el estadio y la fecha de meta para cada gol alemán.
```sql
SELECT goal.player, goal.teamid, game.stadium, game.mdate
FROM game
JOIN goal ON game.id = goal.matchid
WHERE goal.teamid = 'GER';
```

### 6.4. 
Mostrar el equipo 1, el equipo 2 y el jugador por cada gol marcado por un jugador llamado Mario, como 'Mario%'.
```sql
SELECT game.team1, game.team2, goal.player
FROM game
JOIN goal ON game.id = goal.matchid
WHERE goal.player LIKE 'Mario%';
```

### 6.5. 
Mostrar jugador, teamid, entrenador y tiempo de juego para todos los goles marcados en los primeros 10 minutos (tiempo de juego <=10).
```sql
SELECT goal.player, goal.teamid, eteam.coach, goal.gtime
FROM goal
JOIN eteam ON goal.teamid = eteam.id
WHERE goal.gtime <= 10;
```

### 6.6. 
Indica las fechas de los partidos y el nombre del equipo en el que Fernando Santos fue el entrenador del equipo 1.
```sql
SELECT game.mdate, eteam.teamname AS team_name
FROM game
JOIN eteam ON game.team1 = eteam.id
WHERE eteam.coach = 'Fernando Santos';
```

### 6.7 
Enumere el jugador por cada gol marcado en un partido cuyo estadio fue el 'Estadio Nacional de Varsovia'
```sql
SELECT goal.player
FROM goal
JOIN game ON goal.matchid = game.id
WHERE game.stadium = 'National Stadium, Warsaw';
```

### 6.8. 
Muestre el nombre de todos los jugadores que marcaron un gol contra Alemania.
```sql
SELECT distinct player
FROM game JOIN goal ON matchid=id
WHERE (team1='GER' OR team2='GER') AND teamid <> 'GER';
```

### 6.9. 
Mostrar el nombre del equipo y el número total de goles marcados.
COUNT y GROUP BY
```sql
SELECT eteam.teamname, COUNT(*) AS total_goals
FROM eteam
JOIN goal ON eteam.id = goal.teamid
GROUP BY eteam.teamname
ORDER BY eteam.teamname;
```

### 6.10. 
Muestra el estadio y el número de goles marcados en cada uno.
```sql
SELECT game.stadium, COUNT(*) AS total_goals
FROM game
JOIN goal ON game.id = goal.matchid
GROUP BY game.stadium
ORDER BY game.stadium;
```

### 6.11. 
Para cada partido en el que participe 'POL', muestre el ID del partido, la fecha y el número de goles marcados.
```sql
SELECT matchid, mdate, count(*)
FROM game JOIN goal ON id=matchid
WHERE (team1 = 'POL' OR team2 = 'POL')
group by matchid, mdate
```

### 6.12. 
Para cada partido en el que 'GER' haya marcado, muestra el ID del partido, la fecha del partido y el número de goles marcados por 'GER'.
```sql
SELECT goal.matchid, game.mdate, COUNT(*) AS goles
FROM game
JOIN goal ON game.id = goal.matchid
WHERE goal.teamid = 'GER'
GROUP BY goal.matchid, game.mdate;
```

### 6.13 
Enumere cada partido con los goles marcados por cada equipo, como se muestra. Esto usará el caso "CASE WHEN".
Ordena el resultado por mdate, matchid, equipo 1 y equipo 2.
```sql
SELECT 
    game.mdate,
    game.team1,
    SUM(CASE WHEN goal.teamid = game.team1 THEN 1 ELSE 0 END) AS score1,
    game.team2,
    SUM(CASE WHEN goal.teamid = game.team2 THEN 1 ELSE 0 END) AS score2
FROM 
    game
LEFT JOIN 
    goal ON game.id = goal.matchid
GROUP BY 
    game.mdate, game.id, game.team1, game.team2
ORDER BY 
    game.mdate, game.id, game.team1, game.team2;
```

## 7. MORE JOINS OPERATIONS

### 7.1. Películas de 1962
Listar las películas cuyo año es 1962 [Mostrar ID, título]
```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```

### 7.2. ¿Cuándo se estrenó Ciudadano Kane?
Indica el año de estreno de 'Ciudadano Kane'.
```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane';
```

### 7.3. Películas de Star Trek
Enumera todas las películas de Star Trek, incluyendo la identificación, el título y el año (todas estas películas incluyen la palabra "Star Trek" en el título). Ordena los resultados por año.
```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr;
```

### 7.4. Identificación del actor Glenn Close
¿Qué número de identificación tiene el actor Glenn Close?
```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close';
```

### 7.5. Identificación de Casablanca
¿Cuál es la identificación de la película 'Casablanca'?
```sql
SELECT id
FROM movie
WHERE title = 'Casablanca';
```

### 7.6. Lista de actores de Casablanca
Obtén la lista de actores de 'Casablanca'.
¿Qué es una lista de actores?
Usa movieid=11768 
```sql
SELECT actor.name
FROM actor
JOIN casting ON actor.id = casting.actorid
WHERE casting.movieid = 11768;
```

### 7.7. Lista de actores de Alien
Obtén la lista de actores de la película 'Alien'
```sql
SELECT actor.name
FROM actor
JOIN casting ON actor.id = casting.actorid
WHERE casting.movieid = 10522;
```

### 7.8. Películas de Harrison Ford
Enumere las películas en las que ha aparecido Harrison Ford.
```sql
SELECT movie.title
FROM movie
JOIN casting ON movie.id = casting.movieid
WHERE casting.actorid = 2216;
```

### 7.9. Harrison Ford como actor secundario
Enumere las películas donde Harrison Ford ha aparecido, pero no como protagonista. [Nota: El campo ord del casting indica la posición del actor. Si ord = 1, este actor es protagonista].
```sql
SELECT movie.title
FROM movie
JOIN casting ON movie.id = casting.movieid
WHERE casting.actorid = 2216
  AND casting.ord <> 1;
```

### 7.10. Actores principales en películas de 1962
Enumere las películas junto con el protagonista principal de todas las películas de 1962.
```sql
SELECT movie.title, actor.name
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE movie.yr = 1962
  AND casting.ord = 1;
```

### 7.11. Años de mayor actividad para Rock Hudson
¿Cuáles fueron los años de mayor actividad para Rock Hudson? Indica el año y la cantidad de películas que hizo cada año, en caso de que haya hecho más de dos.
```sql
SELECT movie.yr, COUNT(movie.title) AS num_movies
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE actor.name = 'Rock Hudson'
GROUP BY movie.yr
HAVING COUNT(movie.title) > 2;
```

### 7.12. Actor principal en las películas de Julie Andrews
Enumere el título de la película y el actor principal de todas las películas en las que Julie Andrews actuó.
```sql
SELECT movie.title, actor.name
FROM movie
JOIN casting ON movie.id = casting.movieid
JOIN actor ON casting.actorid = actor.id
WHERE movie.id IN (
  SELECT casting.movieid
  FROM casting
  JOIN actor ON casting.actorid = actor.id
  WHERE actor.name = 'Julie Andrews'
)
AND casting.ord = 1;
```

### 7.13. Actores con 15 papeles protagónicos
Obtén una lista, en orden alfabético, de actores que hayan tenido al menos 15 papeles protagónicos.
```sql
SELECT actor.name
FROM actor
JOIN casting ON actor.id = casting.actorid
WHERE casting.ord = 1
GROUP BY actor.name
HAVING COUNT(casting.movieid) >= 15
ORDER BY actor.name ASC;
```

### 7.14. Estrenadas en el año 1978
Enumere las películas estrenadas en el año 1978 ordenadas por número de actores en el reparto y luego por título.
```sql
SELECT movie.title, COUNT(casting.actorid) AS num_actors
FROM movie
JOIN casting ON movie.id = casting.movieid
WHERE movie.yr = 1978
GROUP BY movie.title
ORDER BY num_actors DESC, movie.title ASC;
```

### 7.15. Con 'Art Garfunkel'
Enumere a todas las personas que han trabajado con 'Art Garfunkel'.
```sql
SELECT DISTINCT actor.name
FROM actor
JOIN casting ON actor.id = casting.actorid
WHERE casting.movieid IN (
  SELECT casting.movieid
  FROM casting
  JOIN actor ON casting.actorid = actor.id
  WHERE actor.name = 'Art Garfunkel'
)
AND actor.name <> 'Art Garfunkel';
```


## 8. USING NULL

### 8.1. 
NULL, INNER JOIN, LEFT JOIN, RIGHT JOIN
Enumere los profesores que tienen NULL en su departamento.
```sql
SELECT name
FROM teacher
WHERE dept IS NULL;
```

### 8.2. 
Tenga en cuenta que la unión interna no incluye a los profesores sin departamento ni a los departamentos sin profesor.
```sql
SELECT teacher.name, dept.name
FROM teacher
INNER JOIN dept ON teacher.dept = dept.id;
```

### 8.3. 
Utilice un JOIN diferente para que aparezcan todos los profesores.
```sql
SELECT teacher.name, dept.name
FROM teacher
LEFT JOIN dept ON teacher.dept = dept.id;
```

### 8.4. 
Utilice una combinación diferente para que aparezcan todos los departamentos.
```sql
SELECT teacher.name, dept.name
FROM teacher
RIGHT JOIN dept ON teacher.dept = dept.id;
```

### 8.5. 
Use COALESCE para imprimir el número de móvil. Si no hay número, use el número "07986 444 2266". Indique el nombre y el número de móvil del profesor o "07986 444 2266".
```sql
SELECT name, COALESCE(mobile, '07986 444 2266') AS mobile
FROM teacher;
```

### 8.6.
Use la función COALESCE y una combinación izquierda para imprimir el nombre del profesor y el nombre del departamento. Use la cadena "Ninguno" si no hay departamento.
```sql
SELECT teacher.name, COALESCE(dept.name, 'None') AS department
FROM teacher
LEFT JOIN dept ON teacher.dept = dept.id;
```

### 8.7.
Utilice COUNT para mostrar el número de profesores y el número de teléfonos móviles.
```sql
SELECT COUNT(id) AS num_teachers, COUNT(mobile) AS num_mobiles
FROM teacher;
```

### 8.8. 
Utilice COUNT y GROUP BY dept.name para mostrar cada departamento y su número de personal. Utilice RIGHT JOIN para asegurarse de que el departamento de Ingeniería aparezca en la lista.
```sql
SELECT dept.name, COUNT(teacher.id) AS num_staff
FROM teacher
RIGHT JOIN dept ON teacher.dept = dept.id
GROUP BY dept.name;
```

### 8.9. 
Use mayúsculas y minúsculas para mostrar el nombre de cada profesor, seguido de "Ciencia" si el profesor pertenece al departamento 1 o 2, y de "Arte" en caso contrario.

```sql
SELECT name,
CASE WHEN dept IN (1, 2) THEN 'Sci'
ELSE 'Art' END AS department_type
FROM teacher;
```

### 8.10. 
Use CASE para mostrar el nombre de cada profesor seguido de "Ciencia" si el profesor está en el departamento 1 o 2, muestre "Arte" si el departamento del profesor es 3 y "Ninguno" en caso contrario.
```sql
SELECT name,
CASE WHEN dept IN (1, 2) THEN 'Sci'
WHEN dept = 3 THEN 'Art'
ELSE 'None'
END AS department_type
FROM teacher;
```

------------------------------------
## 8+. NUMERIC EXAMPLES

### 8.1. Revisa la fila
El ejemplo muestra el número de personas que respondieron a la pregunta 1
en la Universidad Napier de Edimburgo
estudiando (8) Informática
Muestra el porcentaje de quienes están TOTALMENTE DE ACUERDO
```sql
SELECT A_STRONGLY_AGREE
FROM nss
WHERE question = 'Q01' AND institution = 'Edinburgh Napier University'
AND subject = '(8) Computer Science';
```

### 8.2. Calcula cuántos están de acuerdo o muy de acuerdo.
Indica la institución y la asignatura donde la puntuación en la pregunta 15 es al menos 100.
```sql
SELECT institution, subject
FROM nss
WHERE question = 'Q15' AND score >= 100;
```

### 8.3. Estudiantes de informática descontentos
Indique la institución y la puntuación donde la puntuación de '(8) Informática' es inferior a 50 en la pregunta 'Q15'.
```sql
SELECT institution, score
FROM nss
WHERE question = 'Q15'
AND subject = '(8) Computer Science'
AND score < 50;
```

### 8.4. ¿Más estudiantes de informática o creativos?
Indique la asignatura y el número total de estudiantes que respondieron a la pregunta 22 para cada una de las asignaturas «(8) Informática» y «(H) Artes Creativas y Diseño».
```sql
SELECT subject, SUM(response) AS total_responses
FROM nss
WHERE question = 'Q22' AND subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
GROUP BY subject;
```

### 8.5. Números de Totalmente de Acuerdo
Muestre la materia y el número total de estudiantes que ESTÁN TOTALMENTE DE ACUERDO con la pregunta 22 para cada una de las materias "(8) Informática" y "(H) Artes Creativas y Diseño".
```sql
SELECT subject, SUM(response * A_STRONGLY_AGREE / 100.0) AS "SUM(response*A_STRONGLY_AGREE/100)"
FROM nss
WHERE question = 'Q22'
AND subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
GROUP BY subject;
```

### 8.6. Totalmente de acuerdo, porcentaje
Muestra el porcentaje de estudiantes que están TOTALMENTE DE ACUERDO con la pregunta 22 de la asignatura "(8) Informática". Muestra la misma cifra para la asignatura "(H) Artes Creativas y Diseño".
Usa la función ROUND para mostrar el porcentaje sin decimales.
```sql
SELECT subject, ROUND(SUM(response * A_STRONGLY_AGREE) / SUM(response), 0) AS percentage
FROM nss
WHERE question = 'Q22'
AND subject IN ('(8) Computer Science', '(H) Creative Arts and Design')
GROUP BY subject;
```

### 8.7. Puntuaciones de las instituciones en Manchester
Muestre las puntuaciones promedio de la pregunta "P22" para cada institución que incluya "Manchester" en su nombre.
La puntuación de la columna es un porcentaje: debe utilizar el método descrito anteriormente para multiplicar el porcentaje por la respuesta y dividirlo entre el total de respuestas. Redondee su respuesta al número entero más cercano.
```sql
SELECT institution, ROUND(SUM(response * score) / SUM(response), 0) AS average_score
FROM nss
WHERE question = 'Q22'
AND institution LIKE '%Manchester%'
GROUP BY institution;
```

### 8.8. Número de estudiantes de informática en Manchester
Indique la institución, el tamaño total de la muestra y el número de estudiantes de informática de las instituciones en Manchester para la pregunta "Q01".
```sql
SELECT institution,
SUM(sample) AS total_sample_size,
SUM(CASE WHEN subject LIKE '(8)%' THEN sample ELSE 0 END) AS computing_students
FROM nss
WHERE question = 'Q01'
AND institution LIKE '%Manchester%'
GROUP BY institution;
```


## 9-. WINDOW FUNCTION

### 9.1. Preparándose
Mostrar el apellido, el partido y los votos para la circunscripción 'S14000024' en 2017.
```sql
SELECT lastName, party, votes
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY votes DESC;
```

### 9.2. ¿Quién ganó?
Puede usar la función RANK para ver el orden de los candidatos. Si usa (ORDER BY votes DESC), el candidato con más votos ocupa el primer puesto.
Muestre el partido y el RANK para la circunscripción S14000024 en 2017. Enumere los resultados por partido.
```sql
SELECT party, votes, RANK() OVER (ORDER BY votes DESC) AS posn
FROM ge
WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party;
```

### 9.3. PARTITION BY
Las elecciones de 2015 son una PARTICIÓN diferente a las de 2017. Solo nos interesa el orden de los votos de cada año.
Utilice PARTITION para mostrar la posición de cada partido en S14000021 cada año. Incluya año, partido, votos y posición (el partido con más votos es el 1).
```sql
SELECT yr, party, votes, RANK() OVER (PARTITION BY yr ORDER BY votes DESC) AS posn
FROM ge
WHERE constituency = 'S14000021'
ORDER BY party, yr;
```

### 9.4. Circunscripción de Edimburgo
Las circunscripciones de Edimburgo están numeradas del S14000021 al S14000026.
Utilice la función "DIVISIÓN POR circunscripción" para mostrar la posición de cada partido en Edimburgo en 2017. Ordene los resultados de modo que los ganadores aparezcan primero y luego por circunscripción.
```sql
SELECT constituency, party, votes, RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
FROM ge
WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
AND yr = 2017
ORDER BY posn, constituency;
```

### 9.5.Solo ganadores
Puede usar SELECT dentro de SELECT para seleccionar solo a los ganadores de Edimburgo.
Muestra los partidos que ganaron en cada circunscripción de Edimburgo en 2017.
```sql
SELECT constituency,party, votes
FROM ge
WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
AND yr  = 2017
ORDER BY constituency,votes DESC
```

### 9.6. Escaños escoceses
Puede usar COUNT y GROUP BY para ver el desempeño de cada partido en Escocia. Las circunscripciones escocesas empiezan por 'S'.
Muestre cuántos escaños obtuvo cada partido en Escocia en 2017.
```sql
SELECT party, COUNT(*) AS seats
FROM (SELECT constituency, party, RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
FROM ge
WHERE constituency LIKE 'S%'AND yr = 2017) AS sc
WHERE posn = 1
GROUP BY party;
```


## 9+. COVID 19

### 9.1. Presentación de la tabla de COVID
El ejemplo utiliza una cláusula WHERE para mostrar los casos en Italia en marzo de 2020.
Modifique la consulta para mostrar los datos de España.
```sql
SELECT name, DAY(whn) AS day, confirmed, deaths, recovered
FROM covid
WHERE name = 'Spain' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn;
```

### 9.2. Introduciendo la función LAG
La función LAG se utiliza para mostrar los datos de la fila o tabla anterior. Al alinear las filas, los datos se dividen por nombre de país y se ordenan según el tiempo de los datos. Esto significa que solo se consideran los datos de Italia.
Modifique la consulta para mostrar los datos confirmados del día anterior.
```sql
SELECT name, DAY(whn) AS day, confirmed, LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) AS previous_day_confirmed
FROM covid
WHERE name = 'Italy' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn;
```

### 9.3. Número de casos nuevos
El número de casos confirmados es acumulativo, pero podemos usar el LAG para recuperar el número de casos nuevos notificados cada día.
Muestra el número de casos nuevos diarios de Italia para marzo.

```sql
SELECT name, DAY(whn) AS day, confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) AS new_cases
FROM covid
WHERE name = 'Italy' AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn;
```

### 9.4. Cambios semanales
Los datos recopilados son necesariamente estimaciones e inexactos. Sin embargo, al considerar un período más largo, podemos mitigar algunos de los efectos.
Puede filtrar los datos para ver solo las cifras del lunes, donde DÍA(hora) = 0.
Muestra el número de casos nuevos en Italia cada semana de 2020 (solo el lunes).
```sql
SELECT name, DATE_FORMAT(whn, '%Y-%m-%d') AS date, confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) AS new_this_week
FROM covid
WHERE name = 'Italy' AND WEEKDAY(whn) = 0 AND YEAR(whn) = 2020
ORDER BY whn;
```

### 9.5. LAG mediante un JOIN
Puedes unir una tabla mediante la función DATE. Esto generará resultados diferentes si faltan datos.
Muestra el número de casos nuevos en Italia cada semana (solo el lunes).
En la consulta de ejemplo, unimos esta semana tw con la semana pasada lw mediante la función DATE_ADD.
```sql

SELECT tw.name, DATE_FORMAT(tw.whn, '%Y-%m-%d') AS date, tw.confirmed - lw.confirmed AS new_cases
FROM covid AS tw
LEFT JOIN covid AS lw
ON DATE_ADD(lw.whn, INTERVAL 1 WEEK) = tw.whn
AND tw.name = lw.name
WHERE tw.name = 'Italy' AND WEEKDAY(tw.whn) = 0
ORDER BY tw.whn;

```

### 9.6. RANK()
Esta consulta muestra el número de casos confirmados junto con la clasificación mundial de casos para la fecha '20/04/2020'. También se muestra el número de muertes por COVID.
Estados Unidos tiene el mayor número, España ocupa el segundo lugar...
Observe que, si bien España ocupa el segundo lugar en cuanto a casos confirmados, Italia tiene el segundo mayor número de muertes por el virus.
Agregue una columna para mostrar la clasificación del número de muertes por COVID.
```sql
SELECT tw.name, tw.confirmed, RANK() OVER (ORDER BY tw.confirmed DESC) AS case_rank, tw.deaths, 
RANK() OVER (ORDER BY tw.deaths DESC) AS death_rank
FROM covid AS tw
WHERE tw.whn = '2020-04-20'
ORDER BY case_rank;
```

### 9.7. Tasa de infección
Esta consulta incluye una tabla JOIN t the world para acceder a la población total de cada país y calcular las tasas de infección (en casos por 100.000).
Muestra la clasificación de la tasa de infección de cada país. Incluye solo países con una población de al menos 10 millones.
```sql
SELECT world.name, ROUND(100000 * confirmed / population, 2) AS infection_rate, 
RANK() OVER (ORDER BY 100000 * confirmed / population) AS rank
FROM covid
JOIN world ON covid.name = world.name
WHERE whn = '2020-04-20' AND population > 10000000
ORDER BY population DESC;
```

### 9.8. Superando la crisis
Para cada país que haya tenido al menos 1000 casos nuevos en un solo día, indique la fecha del pico de casos nuevos.
```sql
SELECT name,
    DATE_FORMAT(whn, '%Y-%m-%d') AS peak_date, newCases AS peakNewCases
FROM (SELECT name, whn, newCases,
        RANK() OVER (PARTITION BY name ORDER BY newCases DESC) AS rnc
FROM (SELECT name, whn, confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) AS newCases
        FROM covid) AS x) AS y 
WHERE rnc = 1 AND newCases > 1000
ORDER BY whn;
```


## 9. SELF JOIN

### 9.1. 
¿Cuántas paradas hay en la base de datos?
```sql
SELECT COUNT(*) AS num_stops
FROM stops;
```

### 9.2. 
Encuentre el valor de identificación de la parada 'Craiglockhart'
```sql
SELECT id
FROM stops
WHERE name = 'Craiglockhart';
```

### 9.3. 
Indique el ID y el nombre de las paradas del servicio '4' 'LRT'.
```sql
SELECT stops.id, stops.name
FROM stops
JOIN route ON stops.id = route.stop
WHERE route.num = '4' AND route.company = 'LRT'
ORDER BY route.pos;
```

### 9.4. 
La consulta que se muestra indica el número de rutas que pasan por London Road (149) o Craiglockhart (53). Ejecute la consulta y observe que los dos servicios que enlazan estas paradas tienen un recuento de 2. 
Agregue una cláusula HAVING para restringir la salida a estas dos rutas.
```sql
SELECT company, num, COUNT(*)
FROM route
WHERE stop = 149 OR stop = 53
GROUP BY company, num
HAVING COUNT(*) = 2;
```

### 9.5. 
Ejecute la autounión mostrada y observe que b.stop muestra todos los lugares a los que se puede llegar desde Craiglockhart, sin cambiar de ruta. Modifique la consulta para que muestre los servicios de Craiglockhart a London Road.
```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON (a.company = b.company AND a.num = b.num)
WHERE a.stop = 53 AND b.stop = 149;
```

### 9.6. 
Modifique la consulta para que se muestren los servicios entre 'Craiglockhart' y 'London Road'.
```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON (a.company = b.company AND a.num = b.num)
JOIN stops stopa ON (a.stop = stopa.id)
JOIN stops stopb ON (b.stop = stopb.id)
WHERE stopa.name = 'Craiglockhart' AND stopb.name = 'London Road';
```

### 9.7. 
Proporcione una lista de todos los servicios que conectan las paradas 115 y 137 ('Haymarket' y 'Leith').
```sql
SELECT DISTINCT a.company, a.num
FROM route a JOIN route b ON
(a.company=b.company AND a.num=b.num)
JOIN stops stopa ON (a.stop=stopa.id)
JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Haymarket' AND stopb.name='Leith';
```

### 9.8.
Proporcione una lista de los servicios que conectan las paradas 'Craiglockhart' y 'Tollcross'.
```sql
SELECT DISTINCT a.company, a.num
FROM route a JOIN route b ON
(a.company=b.company AND a.num=b.num)
JOIN stops stopa ON (a.stop=stopa.id)
JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name='Tollcross';
```

### 9.9. 
Indique una lista detallada de las paradas a las que se puede llegar desde Craiglockhart tomando un solo autobús, incluyendo Craiglockhart, ofrecido por la compañía LRT. Incluya la compañía y el número de autobús de los servicios correspondientes.
```sql
SELECT DISTINCT stopb.name, a.company, a.num
FROM route a JOIN route b ON
(a.company=b.company AND a.num=b.num)
JOIN stops stopa ON (a.stop=stopa.id)
JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND a.company='LRT';
```

### 9.10. 
Encuentra las rutas de dos autobuses que pueden ir de Craiglockhart a Lochend.
Indica el número y la compañía del primer autobús, el nombre de la parada del transbordo y el número y la compañía del segundo autobús.
```sql
SELECT DISTINCT a.num, a.company, s2.name, d.num, d.company
FROM route a, route b, route c, route d, stops s1, stops s2, stops s3
WHERE a.stop = s1.id
  AND s1.name = 'Craiglockhart'
  AND a.company = b.company
  AND a.num = b.num
  AND b.stop = s2.id
  AND b.stop = c.stop
  AND c.company = d.company
  AND c.num = d.num
  AND d.stop = s3.id
  AND s3.name = 'Lochend'
ORDER BY a.num, s2.name, d.num;
```