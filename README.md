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
