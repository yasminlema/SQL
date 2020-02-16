# SQL
## Índice
* [¿Que es SQL?](#que-es-sql)
* [Estructura SQL](#estructura-sql)
* [Clausulas SQL](#clausulas-sql)
  * [SELECT](#select)
  * [FROM](#from)
  * [WHERE](#where)
    * [Simbolos](#simbolos)
    * [IN](#in)
    * [BETWEEN](#between)
    * [LIKE](#like)
  * [ORDER BY](#order-by)
  * [DISTINCT](#distinct)
  * [HAVING](#having)
  * [GROUP BY](#group-by)
  * [ROUND](#round)
  * [LENGTH](#length)
  * [CONCAT](#concat)
  * [SUM](#sum)
  * [COUNT](#count)
  * [JOIN](#join)
    * [LEFT JOIN](#left-join)
    * [RIGHT JOIN](#right-join)
    * [INNER JOIN](#INNER-JOIN)
  
### ¿Que es SQL?
Es un lenguaje declarativo de comunicación dentro de las bases de datos que nos permite el acceso y manipulación de datos en una base de datos, y además se puede integrar a lenguajes de programación, por ejemplo ASP o PHP, y en combinación con cualquier base de datos específica, por ejemplo MySQL, SQL Server, MS Access, entre otras.

### Estructura SQL
* La primera línea es una cláusula SELECT que sirve para indicarle a la base de datos que columnas queremos ver.
* La segunda línea usa FROM para especificar en que tabla se encuentra lo que buscamos.
* La tercera línea es donde utilizaremos el resto de sentencias 
* la consulta **_SIEMPRE_** tiene que tener al final un punto y coma  

### Clausulas SQL
#### SELECT
Sirve para que en la tabla se nos muestren las columnas que nosotros queremos 
  ```ruby
  SELECT population 
  FROM world
  WHERE name = 'Germany' ;
  ```
  Con esta consulta solo nos aparecera la columna de la poblacion 
#### FROM
Sirve para seleccionar la tabla de donde vamos a seleccionar los datos
  ```ruby
  SELECT population
  FROM world ;
  ```
  Con esta consulta le estamos indicando que los datos que le pedimos se encuentran en la tabla world
#### WHERE
Aquí es donde estableceremos la condición que van a tener que cumplir todas las filas para salir en el resultado de la consulta
  ```ruby
  SELECT name 
  FROM world
  WHERE population >= 200000000
  ```
  Con esta consulta ponemos la condicion de que la poblacion tiene que ser mayor o igual a 200000000
  
##### Simbolos
* % : sutituye de cero a varios caracteres
  ```ruby
  SELECT name
  FROM world
  WHERE name = '%United%' ;
  ```
    El resultado de esta consulta seran todos los paises que contengan el nombre United (United Kingdom)
    
* _ : sustituye **_un solo_** caracter 
  ```ruby
  SELECT name 
  FROM world
  WHERE name = 'Cub_' ;
  ```
    El resultado de esta consulta seran todos los paises que empiecen por Cub y a continuacion tengan un caracter mas (Cuba)
* = : igual a 
  ```ruby
  SELECT population
  FROM world
  WHERE name = 'Germany' ;
  ```
    El resultado de esta consulta sera la poblacion de Alemania
 * </>/<=/>= : menor o mayor y igual que 
  ```ruby
  SELECT name
  FROM world
  WHERE population >= 1000000 ;
  ```
    El resultado de esta consulta seran todos los paises con una poblacion mayor o igual a 1000000
* <> : no es igual a 
  ```ruby
  SELECT name
  FROM world
  WHERE name <> '%United%' ;
  ```
    El resultado de esta consulta sera una lista de todos los paises que no tengan en su nombre United
    
##### IN
Coje todos los miembros que estan entre paréntesis 
 ```ruby
 SELECT name, population
 FROM world
 WHERE name IN ('France', 'Germany', 'Italy');
 ```
 En esta consulta pedimos el nombre y poblacion de Francia, Alemania e Italia
 
##### BETWEEN 
Coje todos los miembros contenidos en el rango 
 ```ruby
 SELECT name, area
 FROM world
 WHERE area BETWEEN 200000 AND 250000;
 ```
 El resultado de esta consulta es el nombre y area de todos los paises con un area entre 200000 y 250000
 
##### LIKE
Es utilizado para buscar un patron especifico
 ```ruby
 SELECT name
 FROM world
 WHERE name LIKE '%United%'
 ```
 El resultado de esta consulta es el nombre de todos los paises que contengan United
 
#### ORDER BY
Sirve para especificar el orden en el que quieres que aparezca la respuesta
 ```ruby
 SELECT name, population 
 FROM world
 WHERE name IN ('Sweden', 'Norway', 'Denmark')
 ORDER BY population DESC;
 ```
 En esta consulta la poblacion aparecera de forma descendente
 
#### DISTINCT
 Sirve para que en las consultas no aparezcan filas repetidas
  ```ruby
  SELECT DISTINCT continent
  FROM world;
  ```
  Si ponemos el distinct los continenetes solo apareceran una vez. No se repetiran 
  
#### HAVING
Se utiliza para incluir condiciones del tipo SUM, MAX, .. 
 ```ruby
 SELECT name
 FROM casting JOIN actor
   ON  actorid = actor.id
 WHERE ord = 1
 GROUP BY name
 HAVING COUNT(movieid) >= 15;
 ```
 Con esta consulta nos saldra una lista en oreden alfabetico, de los actores que por lo menos tubieron 15 papeles protagonistas
 
#### GROUP BY
Nos permite agrupar las filas resultado de una consulta en conjuntos y aplicar funciones sobre esos conjuntos de filas
 ```ruby
 SELECT 
  teamname,
  COUNT(teamid)
 FROM eteam JOIN goal ON id = teamid
 GROUP BY teamname;
 ```
 Con esta consulta nos saldra el total de goles de cada equipo en orden alfabetico
 
#### ROUND
Se utiliza para redondear a número de decimales especificado
 ```ruby
 SELECT name, 
        CONCAT(CAST(ROUND(100*population/
                                (SELECT population 
                                 FROM world 
                                 WHERE name = 'Germany'),
                           0),
                      '%')
 FROM world
 WHERE continent = 'Europe';
 ```
 Con esta consulta redondearemos los porcentajes a decimales
 
#### LENGTH
Se utiliza para obtenes la longitud de una cadena 
 ```ruby
 SELECT name, capital
 FROM world
 WHERE LENGTH(name) = LENGTH(capital);
 ```
 Con esta consulta obtenemos los paises y capitales cuyo nombre tiene el mismo numero de letras
 
#### CONCAT
Esta función devuelve una cadena resultante de la combinación de dos o más valores de cadena de una manera integral
 ```ruby
 SELECT CONCAT("SQL ", "is ", "fun!") AS ConcatenatedString;
 ```
 Esta consulta nos daria una columna llamada ConcatenatedString donde pondria "SQL is fun!"
#### SUM
Permite obtener la suma total de los valores de una columna de tipo numérico
```ruby
SELECT SUM(population)
FROM world;
```
Esta consultara sumara las poblaciones de todos los paises y nos enseñara el resutado, que seria la poblacion total en todo el mundo

#### COUNT
Devuelve el número de registros que cumplen una determinada condición
 ```ruby
 SELECT COUNT(name)
 FROM world
 WHERE area >= 1000000;
 ```
 En esta consulta pedimos los paises que tienen un area de al menos 1000000
 
#### JOIN
Se utiliza para cuando necesitamos utilizar varias tablas para hacer la consulta
 ```ruby
 SELECT player,teamid,stadium,mdate
 FROM game JOIN goal ON (id=matchid)
 WHERE teamid='GER';
 ```
 Esta consulta nos muestra todos los goles que hizo Alemania y necesitamos el join porque vamos a utilizar la tabla game y la goal 
 
##### LEFT JOIN
Se obtienen todas las filas de la tabla colocada a la izquierda, aunque haya nulos en la tabla de la derecha
 ```ruby
 SELECT teacher.name, dept.name
 FROM teacher 
 LEFT JOIN dept ON (teacher.dept=dept.id);
 ```
 Esta consulta lista todos los departamentos sean nulos o no ya que va a listar a todos los profesores 
 
##### RIGHT JOIN
Se obtienen todas las filas de la tabla de la derecha, aunque haya nulos en la tabla de la izquierda
 ```ruby
 SELECT teacher.name, dept.name
 FROM teacher 
 RIGHT JOIN dept ON (teacher.dept=dept.id);
 ```
 Esta consulta lista todos los detartamentos y si hay alguno nulo no lo lista
 
##### INNER JOIN
Devuelven únicamente aquellos registros/filas que tienen elementos en las dos tablas
 ```ruby
 SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept ON (teacher.dept=dept.id);
 ```
Esta consulta nos lista todos los departamentos y profesores pero si hay algun nulo en cualquiera de los dos no los lista
