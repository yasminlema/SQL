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
* [DDL](#DDL)
  * [Tipos de datos](#Tipos-de-datos)
    * [Datos de carácter](#Datos-de-carácter)
    * [Datos numericos](#Datos-numericos)
    * [Datos de fecha y hora](#Datos-de-fecha-y-hora)
    * [Datos monetarios](#Datos-monetarios)
    * [Propiedades de datos](#Propiedades-de-datos)
  * [CREATE](#CREATE)
    * [CREATE DOMAIN](#CREATE-DOMAIN)
      * [Parametros](#Parametros)
  * [ALTER](#ALTER)
  * [DROP](#DROP)
  * [TRUCATE](#TRUCATE)
* [DML](#DML)
  * [INSERT INTO](#INSERT-INTO)
  * [UPDATE](#UPDATE)
  * [DELETE FROM](#DELETE-FROM)
* [Instalacion de MySQL](#Instalacion-de-MySQL)
  
## ¿Que es SQL?
Es un lenguaje declarativo de comunicación dentro de las bases de datos que nos permite el acceso y manipulación de datos en una base de datos, y además se puede integrar a lenguajes de programación, por ejemplo ASP o PHP, y en combinación con cualquier base de datos específica, por ejemplo MySQL, SQL Server, MS Access, entre otras. Dentro de SQL podemos encontrar 6 sublenguajes:
* DQL (Data Query Language): permite a los usuarios la consulta y manipulación de datos.
* DDL (Data Definition Language): es el encargado de la modificación de la estructura de los objetos de la base de datos.
* TCL (Transaction Control Language): se utiliza para controlar el procesamiento de transacciones en una base de datos.
* DCL (Data Control Language): permiten la administración del control de acceso de datos contenidos en la base de datos.
* DML (Data Manipulation Language): permite a los usuarios llevar a cabo las tareas de consulta o manipulación de los datos.
* SCL (Session Control Language): permite la gestión de una sesión de usuario.

## Estructura SQL
* La primera línea es una cláusula SELECT que sirve para indicarle a la base de datos que columnas queremos ver.
* La segunda línea usa FROM para especificar en que tabla se encuentra lo que buscamos.
* La tercera línea es donde utilizaremos el resto de sentencias 
* la consulta **_SIEMPRE_** tiene que tener al final un punto y coma

## Clausulas SQL
### SELECT
Sirve para que en la tabla se nos muestren las columnas que nosotros queremos 
  ```ruby
  SELECT population 
  FROM world
  WHERE name = 'Germany';
  ```
  Con esta consulta solo nos aparecera la columna de la poblacion 
### FROM
Sirve para seleccionar la tabla de donde vamos a seleccionar los datos
  ```ruby
  SELECT population
  FROM world;
  ```
  Con esta consulta le estamos indicando que los datos que le pedimos se encuentran en la tabla world
### WHERE
Aquí es donde estableceremos la condición que van a tener que cumplir todas las filas para salir en el resultado de la consulta
  ```ruby
  SELECT name 
  FROM world
  WHERE population >= 200000000;
  ```
  Con esta consulta ponemos la condicion de que la poblacion tiene que ser mayor o igual a 200000000
  
#### Simbolos
* % : sutituye de cero a varios caracteres
  ```ruby
  SELECT name
  FROM world
  WHERE name = '%United%';
  ```
   El resultado de esta consulta seran todos los paises que contengan el nombre United (United Kingdom)
    
* _ : sustituye **_un solo_** caracter 
  ```ruby
  SELECT name 
  FROM world
  WHERE name = 'Cub_';
  ```
   El resultado de esta consulta seran todos los paises que empiecen por Cub y a continuacion tengan un caracter mas (Cuba)
* = : igual a 
  ```ruby
  SELECT population
  FROM world
  WHERE name = 'Germany';
  ```
    El resultado de esta consulta sera la poblacion de Alemania
 * </>/<=/>= : menor o mayor y igual que 
   ```ruby
   SELECT name
   FROM world
   WHERE population >= 1000000;
   ```
    El resultado de esta consulta seran todos los paises con una poblacion mayor o igual a 1000000
* <> : no es igual a 
  ```ruby
  SELECT name
  FROM world
  WHERE name <> '%United%';
  ```
    El resultado de esta consulta sera una lista de todos los paises que no tengan en su nombre United
    
#### IN
Coje todos los miembros que estan entre paréntesis 
 ```ruby
 SELECT name, population
 FROM world
 WHERE name IN ('France', 'Germany', 'Italy');
 ```
  En esta consulta pedimos el nombre y poblacion de Francia, Alemania e Italia
 
#### BETWEEN 
Coje todos los miembros contenidos en el rango 
 ```ruby
 SELECT name, area
 FROM world
 WHERE area BETWEEN 200000 AND 250000;
 ```
  El resultado de esta consulta es el nombre y area de todos los paises con un area entre 200000 y 250000
 
#### LIKE
Es utilizado para buscar un patron especifico
 ```ruby
 SELECT name
 FROM world
 WHERE name LIKE '%United%';
 ```
  El resultado de esta consulta es el nombre de todos los paises que contengan United
 
### ORDER BY
Sirve para especificar el orden en el que quieres que aparezca la respuesta
 ```ruby
 SELECT name, population 
 FROM world
 WHERE name IN ('Sweden', 'Norway', 'Denmark')
 ORDER BY population DESC;
 ```
  En esta consulta la poblacion aparecera de forma descendente
 
### DISTINCT
 Sirve para que en las consultas no aparezcan filas repetidas
  ```ruby
  SELECT DISTINCT continent
  FROM world;
  ```
   Si ponemos el distinct los continenetes solo apareceran una vez. No se repetiran 
  
### HAVING
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
 
### GROUP BY
Nos permite agrupar las filas resultado de una consulta en conjuntos y aplicar funciones sobre esos conjuntos de filas
 ```ruby
 SELECT 
  teamname,
  COUNT(teamid)
 FROM eteam JOIN goal ON id = teamid
 GROUP BY teamname;
 ```
  Con esta consulta nos saldra el total de goles de cada equipo en orden alfabetico
 
### ROUND
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
 
### LENGTH
Se utiliza para obtenes la longitud de una cadena 
 ```ruby
 SELECT name, capital
 FROM world
 WHERE LENGTH(name) = LENGTH(capital);
 ```
  Con esta consulta obtenemos los paises y capitales cuyo nombre tiene el mismo numero de letras
 
### CONCAT
Esta función devuelve una cadena resultante de la combinación de dos o más valores de cadena de una manera integral
 ```ruby
 SELECT CONCAT("SQL ", "is ", "fun!") AS ConcatenatedString;
 ```
  Esta consulta nos daria una columna llamada ConcatenatedString donde pondria "SQL is fun!"
### SUM
Permite obtener la suma total de los valores de una columna de tipo numérico
```ruby
SELECT SUM(population)
FROM world;
```
 Esta consultara sumara las poblaciones de todos los paises y nos enseñara el resutado, que seria la poblacion total en todo el mundo

### COUNT
Devuelve el número de registros que cumplen una determinada condición
 ```ruby
 SELECT COUNT(name)
 FROM world
 WHERE area >= 1000000;
 ```
  En esta consulta pedimos los paises que tienen un area de al menos 1000000
 
### JOIN
Se utiliza para cuando necesitamos utilizar varias tablas para hacer la consulta
 ```ruby
 SELECT player,teamid,stadium,mdate
 FROM game JOIN goal ON (id = matchid)
 WHERE teamid = 'GER';
 ```
  Esta consulta nos muestra todos los goles que hizo Alemania y necesitamos el join porque vamos a utilizar la tabla game y la goal 
 
#### LEFT JOIN
Se obtienen todas las filas de la tabla colocada a la izquierda, aunque haya nulos en la tabla de la derecha
 ```ruby
 SELECT teacher.name, dept.name
 FROM teacher 
 LEFT JOIN dept ON (teacher.dept = dept.id);
 ```
  Esta consulta lista todos los departamentos sean nulos o no ya que va a listar a todos los profesores 
 
#### RIGHT JOIN
Se obtienen todas las filas de la tabla de la derecha, aunque haya nulos en la tabla de la izquierda
 ```ruby
 SELECT teacher.name, dept.name
 FROM teacher 
 RIGHT JOIN dept ON (teacher.dept = dept.id);
 ```
  Esta consulta lista todos los detartamentos y si hay alguno nulo no lo lista
 
#### INNER JOIN
Devuelven únicamente aquellos registros/filas que tienen elementos en las dos tablas
 ```ruby
 SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept ON (teacher.dept = dept.id);
 ```
  Esta consulta nos lista todos los departamentos y profesores pero si hay algun nulo en cualquiera de los dos no los lista

## DDL
DDL o lenguaje de definición de datos (en inglés Data Definition Language), es el encargado modificar la estructura de los objetos de la base de datos. Las ordenes que se incluyen para modificar, borrar o definir las tablas en las que se almacenan los datos son: CREATE, ALTER, DROP y TRUNCATE.

### Tipos de datos
#### Datos de carácter
* CHAR: Los datos deben de tener una longitud fija.
* VARCHAR: Puede variar en el número de carácteres, es decir, el valor asignado no es fijo.

#### Datos numericos
* INT: numero entero
* SMALLINT: numero entero pequeño
* DECIMAL: Tipo de datos que se utiliza para almacenar números decimales que pueden tener hasta 38 dígitos.
* FLOAT: numero en coma flotante
#### Datos de fecha y hora
* DATE: año, mes y dia
* TIME: hora, minuto y segundo
* TIMESTAMP: DATE + TIME

#### Datos monetarios 
* MONEY: Cantidad monetaria positiva o negativa.
 
#### Propiedades de datos
* NULL/NOT NULL: al poner NULL estamos indicando que el contenido de dicha columna no es obligatorio, si se necesita especificar que el campo es obligatorio se implementará con NOT NULL.
* IDENTITY: Propiedad sólo aplicada a campos numéricos, ya que define un autoincremento  automático de valores.

### CREATE
Este comando permite crear nuevas bases de datos, tablas y usuarios.
* Para crear usuarios usamos la formula "CREATE USER"
* Para crear tablas usamos la formula "CREATE TABLE"
* Para crear una nueva base de datos hay dos formulas:
  * Con permisos restrictivos -> CREATE DATABASE
  * Con permisos menos restrictivos -> CREATE SHEMA

* Ejemplo de como creariamos una tabla:
 ```ruby
 CREATE TABLE nombre_tabla;
 ```
 ```ruby
 CREATE TABLE alumnos;
 ```
 
 #### CREATE DOMAIN
 Sirve para crear tipos de datos 
 ```ruby
 CREATE DOMAIN nombre_dato  TipoDato;
 ```
 
 ##### Parametros
 * nombre_dato: nombre del tipo de dato que queremos crear.
 * TipoDato: tipo de dato que vamos a crear. Puede ser:
   * MONEY, DATE, INT, NUMBER, CHAR, VARCHAR
 * CONSTRAINT: establece un nombre opcional a una restriccion. Si no especificamos    el nombre el sistema genera uno el mismo.
 * NUL/NOT NULL: al poner NULL estamos indicando que el contenido de dicha columna no es obligatorio, si se necesita especificar que el campo es obligatorio se implementará con NOT NULL. El valor por defecto es NULL.
 * UNIQUE: lo pondremos cuando el dato sea unico.
 * ON DELETE CASCADE: permite eliminar datos de las tablas secundarias automáticamente cuando elimina los datos de la tabla primaria.
 * ON UPDATE CASCADE: permite actualizar datos de las tablas secundarias automáticamente cuando añade los datos a la tabla primaria.
 
 ```rudy
 CREATE DOMAIN nombre_válido VARCHAR(30);
CREATE TABLE Ubicación (
  Nome_Sede         Nome_Válido,
  Nome_Departamento Nome_Válido,
  CONSTRAINT PK_Ubicación
    PRIMARY KEY (Nome_Sede, Nome_Departamento),
  CONSTRAINT FK_Sede
    FOREIGN KEY (Nome_Sede)
    REFERENCES Sede (Nome_Sede)
    ON DELETE CASCADE
    ON UPDATE CASCADE,
  CONSTRAINT FK_Departamento
    FOREIGN KEY (Nome_Departamento)
    REFERENCES Departamento (Nome_Departamento)
    ON DELETE CASCADE
    ON UPDATE CASCADE
);
 ```

### ALTER
Este comando permite modificar la estructura de una tabla u objeto. Se pueden agregar/quitar campos a una tabla, modificar el tipo de un campo, agregar/quitar índices a una tabla, etc.

* Ejemplo de como agregar una columna a una tabla
 ```ruby
 ALTER TABLE nombre_tabla 
 ADD nombre_columna TipoDato;
 ```
 ```ruby
 ALTER TABLE alumnos
 ADD nombre VARCHAR(50);
 ```

### DROP
Este comando sirve para eliminar un objeto de la base de datos. Puede ser una tabla, vista, índice, función, procedimiento o cualquier objeto que el motor de la base de datos soporte.

* Ejemplo de como eliminar una columna de una tabla
 ```ruby
 ALTER TABLE nombre_tabla
 DROP COLUMN nombre_columna;
 ```
 ```ruby
 ALTER TABLE alumnos
 DROP COLUMN nombre;
 ```
 
### TRUCATE
Este comando trunca todo el contenido de una tabla, es decir, borra todo el contenido sin borrar la tabla en si.

* Ejemplo de como truncar una tabla
 ```ruby
 TRUCATE TABLE nombre_tabla;
 ```
 ```ruby
 TRUCATE TABLE alumnos;
 ```
## DML
DML o lenguaje de manipulación de datos (en inglés Data Manipulation Language) es un lenguaje proporcionado por el sistema de gestión de base de datos que permite a los usuarios llevar a cabo las tareas de consulta o manipulación de los datos, organizados por el modelo de datos adecuado.
### INSERT INTO
Agrega uno o más registros a una (**_y sólo una_**) tabla en una base de datos relacional.
```ruby
INSERT INTO nombre_tabla [(<columna1>,<columna2>,...)] 
[VALUES (<valor1A>,<valor2A>,...),(<valor1B>,<valor2B>,...)
...| SELECT...);
```
Ejemplo:
```ruby
INSERT INTO world (name, continent, area)
 VALUES ('France', 'Europe', 100),
   ('Germany', 'Europe', 10)
```
### UPDATE
Se utiliza para modificar los valores de un conjunto de registros existentes en una tabla.
```ruby
UPDATE nombre_tabla
SET <atributo1> = <valor1>, <atributo2> = <valor2>;
```
Ejemplo:
```ruby
UPDATE world
SET continent='Asia';
```
### DELETE FROM
Borra uno o más registros existentes en una tabla.
```ruby
DELETE FROM nombre_tabla
[WHERE <predicado>];
```
Ejemplo:
```ruby
DELETE FROM world
WHERE continent='Africa';
```

## Instalacion de MySQL
Lo primero que debemos hacer es entrar en la Web oficial de MySQL y despues una vez que hayamos entrado clicaremos en "MySQL Comunnity Server". Una vez ahi elegimos la plataforma en la que queremos instalar MySQL. A continuacion clicaremos sobre "Go to Download Page".

![captura1](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura.png)

En la siguiente pagina escogeremos la segunda opcion (la de mas tamaño) ya que en una descargaremos el paquete completo y en el otro no.

![captura2](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura2.png)

Una vez descargado se nos abrira la siguiente ventana donde elegiremos la opcion de "Developer Default" que nos instalara todo automaticamente y clicamos en next.

![captura3](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura3.png)

A continuación, nos aparecera la ventana de preparacion de los paquetes para su instalacion. Algunos en vez de poner  "INSTL DONE" pondra "Manual" porque no se van a poder instalar ya que nos faltan algunos paquetes necesarios en nuestro equipo. Clicamos en next.

![captura4](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura4.png)

El siguiente paso sera ejecutar la instalacion de los paquetes.

![captura5](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura5.png)

Una vez finalizada la instalacion de todos los paquetes procederemos a la configuracion de MySQL. Elegiremos la primera opcion: "Standalone MySQL Server/Classic MySQL Replication".

![captura7](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura7.png)

Despues elegiremos la opcion que mas se ajuste a lo nosotros queremos:
* Development Computer: Está orientado a ser un equipo en el que está instalado el servidor SQL, pero también el cliente para las consultas de bases de datos. Si nuestro equipo es doméstico y trabajamos de forma normal en él está será la opción que debemos elegir.
* Server Computer: esta segunda opción será orientada a ordenadores utilizados para funciones de servidor, por ejemplo, servidor web con bases de datos.
* Dedicated Computer: la tercera opción es par el caso en que queremos crear un equipo solo y exclusivamente orientado a bases de datos. Por ejemplo, una máquina virtual en la que se almacenen nuestras bases de datos.
Yo elegi la opcion de "Dedicated Computer" ya cree una maquina virtual para las bases de datos y es donde estoy instalando el programa.

![captura8](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura8.png)

A continuacion, estableceremos una contraseña para conectarnos al servidor SQL y crearemos un usuario.

![captura9](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura9.png)

Configuramos el nombre del servicio para MySQL

![captura10](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura10.png)

Para finalizar, en la ultima  pantalla pulsamos en "Execute" para las acciones y activar los servicios.

![captura11](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura11.png)

Lo ultimo que debemos hacer sera conectar con el servidor mediante el usuario root y la contraseña que hayamos definido anteriormente clicando en "Check"

![captura12](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura12.png)

Y como podemos ver ha sido instalado correctamente.

![captura14](https://github.com/yasminlema/apuntes-SQL/blob/master/Imagenes/Captura14.PNG)
