# APUNTES SOBRE SQL 

**SQL(Structured Query Language)** es un lenguaje diseñado para administrar y recuperar información de un sistema de bases de datos.

### Sentencias
Para ejecutar SQL necesitamos usar ciertas sentencias que nos permiten crear, consultar o borrar bases de datos.

- **Crear una base de datos**
Una base de datos tambien conocido como Schema, contiene un conjunto de tablas con su información respectiva:

```sql
CREATE DATABE nombredb;
```

- **Muestra todas las bases de datos**
```sql
SHOW DATABASES;
```
- **Especifica que base de datos se debe usar**
 ```sql
 USE nombredb
```

### TIPOS DE DATOS BASICOS
En SQL hay que especificar el tipo de dato que vamos a almacenar, existen muchos tipos de datos. Aquí los más básicos:

1.  **INT**:  Números enteros 0,2,15,255,etc...
2. **FLOAT**: Números decimales 6.25, 15.2566, etc...
3. **VARCHAR**: Cadena de caracteres que pretenden tener un tamaño definido en bytes, pueden ser palabras o frases

- **Crear una tabla**

La siguiente tabla crea tres columnas una con un nombre id, otra que dice tipo, y otra que dice estado.
La **PRIMARY KEY** es el identificador interno de la tabla, normalmente es asociado a un id.

 ```sql
 CREATE TABLE nombre_tabla(
 //Valores o columnas que va a tener la tabla asi como su tipo de dato que se espera.
 id int,
 tipo varchar(255),
 estado varchar(255),
 PRIMARY KEY(id)
 );
```


 - **Alterar o modificar una columna:**
 Modifica solo la columna y haciendo referencia al tipo de dato tambien.
 ```sql
 ALTER TABLE nombre_tabla MODIFY columna INT AUTO_INCREMENT;
```


 - **Actualizar un dato y Borrar**
Podemos actualizar y borrar datos de nuestra tabla usando la sentencia WHERE

 ```sql
 UPDATE nombre_tabla SET columna WHERE id = 3
 DELETE FROM nombre tabla WHERE columna = 'Feliz' AND id = 3;
```
 - **Insertar un valor a la tabla**
 Se especifica la tabla y las columnas a las que van agregar un registro, seguido de los valores en su columna correspondiente
 ```sql
 INSERT INTO nombre_tabla(columna1, columna2)
 VALUES('Felipe', 'Triste');
```
 - **Limit**
 Nos permite definir un limite de datos a traer y nos seleccionara los primeros datos que coincidan.
 
 ```sql
 SELECT * FROM tabla limit 2;
 SELECT * FROM tabla WHERE edad > 10 limit 1;
```
 - **AND & OR**
 Podemos usar el operador AND y OR para crear queries un poco más complejas:
 
 ```sql
 SELECT * FROM tabla WHERE edad > 30 AND edad < 50;
 SELEC * FROM tabla WHERE edad > 30 OR edad < 30;
```

 - **Like**
 Like nos permte usar '%' para hacer busquedas en textos o datos de tipo varchar.
 En pocas palabras '%' se traduce como (No importa el contenido como empiece o como termine o ambos)
 **%Palabras%*** //No importa como empiece o termine debe contener el termino Palabras
 **%Palabras*** //No importa como empiece debe terminar en el 'Palabras'
 **Palabras%*** //No importa como termine debe empezar en el 'Palabras'
 
 
 ```sql
 SELECT * FROM tabla WHERE nombre LIKE 'Carla%';
```

 - **Between**
Permite tener los valores que esten entre dos valores.
 
 ```sql
 SELECT * FROM tabla WHERE edad BETWEEN 20 and 30;
```

 - **Ordenas de manera ascendete y descendente**
 Traer datos de una manera ordenada especifica (mayor a menor o menor a mayor):
 
 ```sql
 SELECT * FROM tabla ORDER BY edad ASC;
 SELECT * FROM tabla ORDER BY edad DESC;
```

 - **Buscar el valor Maximo o Minimo**
 Podemos hacer uso de las funciones MAX y MIN para traer el valor maximo o mininmo de una tabla
 **NOTA: AS es para asignar un alias, este alias solo vive en el momento de hacer el query pero no se crea una tabla ni se mantiene el valor fuera de el query**
 
 ```sql
 SELECT MAX(edad) AS mayor_edad FROM tabla;
 SELECT MIN(edad) AS menor_edad FROM tabla;
```

- **Renombrar una tabla**
 ```sql
 RENAME TABLE tabla TO nueva_tabla;
```

 - **Ejemplo de una tabla con llave foranea**
 ```sql
 create table products(
 id int not null auto_increment,
 name varchar(50) not null,
 created_by int not null,
 marca varchar(50) not null,
 primary key(id),
 foreign key(created_by) references user(id)
 );
```

- **Left join**
Basicamente es asociar una tabla que trae todos los datos que corresponden a la tabla y solo trae los datos de otra tabla si solo si, estos coinciden con la tabla principal asociada:

 ```sql
 SELECT user_table.id, user_table.email, product_table.name 
 FROM user user_table 
 LEFT JOIN product product_table 
 ON user_table.id = product_table.created_by;
```

 - **Count**
 Nos regresa el total de elementos agrupados por una caracteristica en concreto:
 
 ```sql
 SELECT count(id) FROM users;
 SELECT count(id), marca FROM users GROUP BY marca;
```

- **In**
Permite pasar una colección de elementos para la query.

 ```sql
 SELECT * FROM users WHERE country in ('Mexico', 'Germany', 'USA');
```

 - **Proyección SELECT**

 El select más basico, hace una proyección de una entidad sin filtrar campos o columnas
 ```sql
 SELECT * FROM table_one;
```

- **Te permite cambiar el nombre o poner un alias a una columna, si esta no es muy descriptiva**
 ```sql
 SELECT fiedl AS alias;
```

 - **FUNCIONES**
 - Funciones matemáticas. Estas te permiten realizar conteos, sumas, realizar promedios y/o buscar minimos
y maximos
 ```sql
SELECT COUNT(id), SUM(quantity), AVG(age);
SELECT MIN(date), MAX(quantity);
```

- **ESTRUCTURAS DE CONTROL**
Podemos comparar una columna con otra y devolver un valor
 ```sql
 SELECT IF(500<1000, "YES", "NO");

SELECT OrderID, Quantity
CASE 
    WHEN Quantity > 30 THEN "Over 30"
    WHEN Quatity = 30 THEN "Equal 30"
    ELSE "Under 30"
END AS QuantityText;
```

 - **Producto cartesiano JOIN**
 Crea el equivalente a una intersección de diagrama de ven
 ```sql
 SELECT * 
FROM tabla_diaria AS td
	JOIN tabla_mensual AS tm
	ON td.pk = tm.fk;
```

- **WHERE**
WHERE nos permite hacer querys complejas combinandolas con operadores como estos
 ```sql
 SELECT * FROM users WHERE name = 'Israel'
AND (
 lastname = 'Vazquez'
 OR
 lastname = 'Lopez'
);


SELECT * FROM users
WHERE name = 'Israel'
  AND lastname = 'Vazquez'
  OR lastname = 'Lopez'
```

 - **LIKE**
 LIKE nos permite buscar por un tipo de caracteres si es que no se tiene todo el dato
 ```sql
 SELECT * FROM users
WHERE name LIKE 'Is%';

SELECT * 
FROM users
WHERE name LIKE 'Is_ael';

SELECT * FROM users
WHERE name NOT LIKE 'Is_ael';
```

- **NOT NULL**
Buscar valores nulos o no nulos
 ```sql
 SELECT * FROM users 
WHERE name IS NULL;

SELECT * FROM users 
WHERE name IS NOT NULL;
```

 - **IN**
 busca las considencias de los paraemtros que ponemos en parentesis
 ```sql
 SELECT * FROM users 
 WHERE name IN ('Omar', 'Karla', 'Gustavo');
```


- **ORDER**
Order by nos ayuda con el ordenamiento
 ```sql
 SELECT *
 FROM tabla_diaria ORDER BY fecha;
```

 - **Order desc**
 Ordenar de manera descendente

 ```sql
 SELECT *
 FROM tabla_diaria ORDER BY fecha DESC
```

- **Order asc**
Ordenar de manera ascendente

 ```sql
 SELECT *
 FROM tabla_diaria ORDER BY fecha ASC;
```

 - **GROUP BY**
Agregación, nos permite crear agrupaciones o reducir los datos en
grupos.
 ```sql
 SELECT * FROM tabla
 GROUP BY marca;

 SELECT * FROM tabla
 GROUP BY marca, modelo;
```

- **Limit**
Limites o Limit
Nos permite generar limites en queries para mejorar rendimiento.

 ```sql
 SELECT * FROM tabla
 LIMIT 120
```

 - **OFSSET** 
Nos permite brincar ciertos regitros, en el siguiente ejemplo:
Se brinca los primeros 150 registros y trae los primeros 30 despues
de esos.

 ```sql
 SELECT * FROM tabla
 OFFSET 150
 LIMIT 30
```


- **FECTH**
Es un estandar SQL para traer ciertos elementos de una tabla.
Trae el primer elemento de la tabla

 ```sql
 SELECT *
 FROM tabla_alumnos AS alumnos
 FETCH FIRST 1 ROWS ONLY;
```

 - **Window Function**
Las funciones ventana te permite hacer queries de subqueries

Genera una columna con el nombre "row_id" donde le asigna el numero de row
que tiene el registro. (No siempre puede coincidir con el id)
 
 ```sql
SELECT *
FROM (
	SELECT ROW_NUMBER () OVER() AS row_id, *
	FROM tabla_alumnos
 )AS alumnos_with_row_nums
 WHERE row_id = 1
```

- **Distinc**
Regresa el registro solo una vez sin importar si hay más registros con
ese valor.

Trae el valor de colegiatura más alto.
 ```sql
 SELECT DISTINCT colegiatura
FROM alumnos
ORDER BY colegiatura DESC
LIMIT 1;

SELECT DISTINCT colegiatura
FROM escuela AS a1
WHERE 2 = (
    SELECT COUNT (DISTINCT colegiatura)
    FROM escuela a2
    WHERE a1.colegiatura <= a2.colegiatura
)
```

 - **Ejemplo de conjuntos**
 Traer la lista de alumnos, que tienen al mismo profesor
 
 ```sql
 SELECT * FROM alumnos
WHERE id IN (
 SELECT id FROM alumnos
 WHERE tutor_id = 30

);
```

- **Extract**
Nos permite extraer un valor determinado para un campo en especifico.
Este es muy util para fechas o datos de tipo date o timestamp.

 ```sql
SELECT EXTRACT(YEAR FROM fecha_incorporacion) AS anio
FROM escuela
```

 - **Particionar fechas** 
Este es muy util para extraer años, meses o dias

 ```sql
 SELECT DATE_PART('YEAR', fecha_incorporacion) AS anio,
       DATE_PART('MONTH', fecha_incorporacion) AS mes,
       DATE_PART('MONTH', fecha_incorporacion) AS mes
FROM alumnos;
```


- **Particionar horas, minutos, segundos**
Al igual que para las fechas, podemos extraer horas, minutos o segundo 
de un query determinado.

 ```sql
 SELECT DATE_PART('HOUR', fecha_incorporacion) AS hour,
       DATE_PART('MINUTE', fecha_incorporacion) AS minute,
       DATE_PART('SECOND', fecha_incorporacion) AS second
FROM alumnos;
```

 - **Selectores de rango**
 Es una función que genera un rango de numeros enteros y retorna un boolean.

En este ejemplo evalua si el numero 3 esta dentro del rango de 10 a 20
y la respuesta es false

 ```sql
 SELECT int4range(10,20) @> 3;
```

- **Numrange**
Nos permite crear rangos con numeros y de forma decimal. De igual manera
regresa un boleano.

En este caso evalua si hay un valor dentro de ambos rangos, de ser asi devuelve 
true 

 ```sql
 --False
SELECT numrange(11.1, 19.9) && numrange(20.00, 30,00);

--True
SELECT numrange(11.1, 22.0) && numrange(20.00, 30,00);
```

 - **Valor mas alto de un rango**
 Upper nos regresa el valor mas alto de un rango númerico.
 
 ```sql
 SELECT UPPER(int8range(15,25));
```

- **Valor mas bajo de un rango**
lower nos regresa el valor mas alto de un rango númerico.
 ```sql
 SELECT LOWER(int8range(15,25));
```

 - **Rango vacio**
Nos devuelve un boolean evaluando si el rango esta vacio.

 ```sql
 SELECT ISEMPTY(numrange(1,5));
```


 - **LPad**
 (Rellena por la izquiersa)Nos permite generar una cadena con relleno donde recibe tres parametros
1.- una cadena de caracteres
2.- Numero de relleno
3.- El caracter por el que se rellena

Esto mantiene el lenght de ese numero.

 ```sql
SELECT lpad('Manuel', 15,'+');

SELECT lpad(nombre, id, '*')
FROM alumnos
WHERE id < 10;
```

- **RPad**
Es igual que left solo que en este caso es con relleno a la derecha.

 ```sql
 SELECT rpad('Manuel', 15,'+');
```

 - **Generar Series**
 Nos permite generar rangos o series en duplas. Recibe los rangos y como 
tercer paramtro los pasos que va a hacer.

 ```sql
 //Genera un rango del 1 al 5 de uno en uno
SELECT * FROM generate_series(1,5); 

//Genera un rango del 2 al 20 de dos en dos
SELECT *  FROM generate_series(2, 20, 2);
```

- **Series con fechas**
Tambien es posible usar el query anterior en fechas u horas.

 ```sql
 SELECT *
FROM generate_series('2020-09-01 00:00:00'::timestamp, 
'2020-09-04 12:00:00', '10 hours');
```

 - **SELECT para secuencias**
Es posible modificar la secuencia de una tabla, esto altera la manera en como se genera la numeración de los id
ejemplo podemos pasar del id = 10 al 150. Si es que se desea o incluso poder corregir las secuencias.
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```


 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```

- ****
 ```sql
```

 - ****
 ```sql
```


- ****
 ```sql
```

 - ****
 ```sql
```



## COMANDOS DE POSTGRES DESDE LA CONSOLA


1.- VER TODOS LOS COMANDOS \ DE POSTGRES
`\?`

2.- LISTAR TODAS LAS BASES DE DATOS
`\l` 

3.- VER LAS TABLAS DE UNA BASE DE DATOS
`\dt`

4.- CAMBIAR A OTRA BD
`\c nombre_BD`

5.- DESCRIBIR UNA TABLA
`\d nombre_tabla`

6.- VER TODOS LOS COMANDOS SQL
`\h`

7.- VER COMO SE EJECTUA UN COMANDO SQL
`\h nombre_de_la_funcion`

8.- CANCELAR TODO LO QUE HAY EN PANTALLA
`Ctrl + C`

9.- VER LA VERSION DE POSTGRES INSTALADA, IMPORTANTE PONER EL ';'
`SELECT version();`


10.- VOLVER A EJECUTAR LA FUNCION REALIADA ANTERIORMENTE
`\g`

11.- INICIALIZAR EL CONTADOR DE TIEMPO PARA QUE LA CONSOLA TE DIGA EN CADA EJECUCION ¿CUANTO DEMORO EN EJECUTAR ESA FUNCION?
`\timing`

12.- LIMPIAR PANTALLA DE LA CONSOLA PSQL
`Ctrl + L`


### CREAR ROLES
Basicamente es crear un "usuario" que puede tener ciertos permisos sobre nuestra Base de Datos. HAY QUE USARLOS CON PRECAUCION YA QUE ESTO PUEDE ALTERAR NUESTRAS TABALAS.

Que puede hacer un ROLE:

- Crear y Eliminar
- Asignar atributos
- Agrupar con otros roles
- Roles predeterminados

-- Ver las funciones del comando CREATE ROLE (help)

`\h CREATE ROLE;`

-- Creamos un ROLE (consultas -> lectura, insertar, actualizar)
 ```sql
 CREATE ROLE usuario_consulta;
```

-- Mostrar todos los usuarios junto a sus atributos

`\dg`
-- Agregamos atributos al usuario o role

 ```sql
ALTER ROLE  usuario_consulta WITH LOGIN;
ALTER ROLE  usuario_consulta WITH SUPERUSER;
ALTER ROLE  usuario_consulta WITH PASSWORD'1234';
```


-- Elimanos el usuario o role

 ```sql
 DROP ROLE usuario_consulta;
```

-- La mejor forma de crear un usuario o role por pgadmin

 ```sql
 CREATE ROLE usuario_consulta WITH
  LOGIN
  NOSUPERUSER
  NOCREATEDB
  NOCREATEROLE
  INHERIT
  NOREPLICATION
  CONNECTION LIMIT -1
  PASSWORD'1234';
```


--Para obtorgar privilegios a nuestro usuario_consulta

```sql
GRANT INSERT, SELECT, UPDATE ON TABLE public.estacion TO usuario_consulta;
GRANT INSERT, SELECT, UPDATE ON TABLE public.pasajero TO usuario_consulta;
GRANT INSERT, SELECT, UPDATE ON TABLE public.trayecto TO usuario_consulta;
GRANT INSERT, SELECT, UPDATE ON TABLE public.tren TO usuario_consulta;
GRANT INSERT, SELECT, UPDATE ON TABLE public.viaje TO usuario_consulta;
```

#### SP STORE PROCEDURES

Mirar el contenido de un Store Procedure en SQL
```sql
sp_showtext NOMBREDELSP
```
