# SQL
### Índice
* [¿Que es SQL?](#8)
* [Estructura del lenguaje SQL](#11)
* [Clausulas SQL](#55)
  * [SELECT](#)
  * [FROM](#)
  * [WHERE](#)
    * [Simbolos](#)
    * [IN](#)
  * [ORDER BY](#)
  
#### ¿Que es SQL?
Es un lenguaje declarativo de comunicación dentro de las bases de datos que nos permite el acceso y manipulación de datos en una base de datos, y además se puede integrar a lenguajes de programación, por ejemplo ASP o PHP, y en combinación con cualquier base de datos específica, por ejemplo MySQL, SQL Server, MS Access, entre otras.

#### Estructura SQL
* La primera línea es una cláusula SELECT que sirve para indicarle a la base de datos que columnas queremos ver.
* La segunda línea usa FROM para especificar en que tabla se encuentra lo que buscamos.
* La tercera línea es donde utilizaremos el resto de sentencias 
* la consulta **_SIEMPRE_** tiene que tener al final un punto y coma  

#### Clausulas SQL
##### SELECT
Sirve para que en la tabla se nos muestren las columnas que nosotros queremos 
  ```
  SELECT population 
  FROM world
  WHERE name = 'Germany' ;
  ```
  Con esta consulta solo nos aparecera la columna de la poblacion 
##### FROM
Sirve para seleccionar la tabla de donde vamos a seleccionar los datos
  ```
  SELECT population
  FROM world ;
  ```
  Con esta consulta le estamos indicando que los datos que le pedimos se encuentran en la tabla world
##### WHERE
Aquí es donde estableceremos la condición que van a tener que cumplir todas las filas para salir en el resultado de la consulta
  ```
  SELECT name 
  FROM world
  WHERE population >= 200000000
  ```
  Con esta consulta ponemos la condicion de que la poblacion tiene que ser mayor o igual a 200000000
  
###### Simbolos
* % : sutituye de cero a varios caracteres
  ```
  SELECT name
  FROM world
  WHERE name = '%United%' ;
  ```
    El resultado de esta consulta seran todos los paises que contengan el nombre United (United Kingdom)
    
* _ : sustituye **_un solo_** caracter 
  ```
  SELECT name 
  FROM WORLD
  WHERE name = 'Cub_' ;
  ```
    El resultado de esta consulta seran todos los paises que empiecen por Cub y a continuacion tengan un caracter mas (Cuba)
* = : igual a 
  ```
  SELECT population
  FROM world
  WHERE name = 'Germany' ;
  ```
    El resultado de esta consulta sera la poblacion de Alemania
 * </>/<=/>= : menor o mayor y igual que 
  ```
  SELECT name
  FROM world
  WHERE population >= 1000000 ;
  ```
    El resultado de esta consulta seran todos los paises con una poblacion mayor o igual a 1000000
* <> : no es igual a 
  ```
  SELECT name
  FROM world
  WHERE name <> '%United%' ;
  ```
    El resultado de esta consulta sera una lista de todos los paises que no tengan en su nombre United

##### ORDER BY
