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
