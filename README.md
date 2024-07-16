# Tipos de Sentencias SQL
En SQL existen varios tipos de sentencias que se utilizan para realizar diferentes operaciones en una base de datos. Aquí te presento algunos de los tipos de sentencias más comunes:

Sentencias DDL (Data Definition Language): se utilizan para definir y modificar la estructura de la base de datos. Por ejemplo para crear o modificar la estructura de una tabla.
Sentencias DML (Data Manipulation Language): se utilizan para manipular los datos dentro de la base de datos. Por ejemplo las instrucciones del CRUD de datos (INSERT, SELECT, UPDTE y DELETE).
Sentencias DCL (Data Control Language): se utilizan para controlar el acceso a la base de datos y garantizar la seguridad. Por ejemplo para otorgar permisos a los usuarios para acceder a las bases de datos.
Sentencias TCL (Transaction Control Language): se utilizan para controlar las transacciones en una base de datos.

# Gestionado de Bases de Datos 
SHOW DATABASES;

CREATE DATABASE nombre_base;

CREATE DATABASE IF NOT EXISTS nombre_base;

DROP DATABASE nombre_base;

DROP DATABASE IF EXISTS nombre_base;

USE nombre_base;

# Sintaxis SQL Avanzada
Índices
En SQL existen varios tipos de índices, los principales son:

Índice único (UNIQUE): asegura que los valores de la columna indexada sean únicos en la tabla.
Índice primario (PRIMARY KEY): es un tipo especial de índice único que identifica de forma única cada fila de una tabla.
Índice secundario (INDEX): es un índice que no tiene restricciones de unicidad y se utiliza para mejorar el rendimiento de consultas que involucran la columna indexada.
Índice de texto completo (FULLTEXT): se utiliza para hacer búsquedas de texto completo en columnas de texto grandes, como VARCHAR y TEXT.

CREATE TABLE una_tabla(
  campo_id INTEGER UNSIGNED PRIMARY KEY,
  campo_unico VARCHAR(80) UNIQUE,
  campo_index VARCHAR(80),
  campo_3 VARCHAR(80),
  campo_4 VARCHAR(80),
  INDEX i_campo_index(campo_index)
  FULLTEXT INDEX fi_campo_fulltext(campo_3, campo_4)
);

# Foreing Keys
Foreign Keys
En SQL, una llave foránea (Foreign Key) es un campo o conjunto de campos en una tabla que hacen referencia a una clave única en otra tabla, estableciendo así una relación entre ambas tablas. Se utilizan para mantener la integridad referencial de los datos, lo que significa que garantizan que los datos en las tablas relacionadas sean coherentes y precisos.

Sintaxis
Se define dentro de una tabla de la siguiente forma:

FOREIGN KEY (nombre_campo) REFERENCES tabla_referencia(campo_referencia)

#JOINS 
Los JOINs en SQL sirven para combinar filas de dos o más tablas basándose en un campo común entre ellas, devolviendo por tanto datos de diferentes tablas. Un JOIN se produce cuando dos o más tablas se juntan en una sentencia SQL.

Los más importantes son los siguientes:

INNER JOIN: Devuelve todas las filas cuando hay al menos una coincidencia en ambas tablas.
LEFT JOIN: Devuelve todas las filas de la tabla de la izquierda, y las filas coincidentes de la tabla de la derecha.
RIGHT JOIN: Devuelve todas las filas de la tabla de la derecha, y las filas coincidentes de la tabla de la izquierda.
OUTER JOIN: Devuelve todas las filas de las dos tablas, la izquierda y la derecha, también se llama FULL OUTER JOIN.

#Subconsultas
Es una consulta dentro de otra:

SELECT t1.campo_1, t1.campo_2, (
    SELECT COUNT(*)
    FROM tabla_2 AS t2
    WHERE t2.campo_1 = t1.campo_1
  ) AS sub_consulta_campo
  FROM tabla_1 AS t1;

SELECT t1.campo_1, t1.campo_2, t1.campo_3, (
    SELECT campo_1
    FROM tabla_2 AS t2
    WHERE t2.campo_1 = t1.campo_1
  ) AS sub_consulta_campo
  FROM tabla_1 AS t1;

# Restricciones
En SQL, las restricciones ON DELETE y ON UPDATE se utilizan para especificar qué acciones se deben realizar en una tabla relacionada cuando se realiza una operación de eliminación o actualización en la tabla principal.

Las acciones que se pueden especificar para las restricciones ON DELETE y ON UPDATE son:

CASCADE: elimina o actualiza automáticamente los registros relacionados en la tabla relacionada.
SET NULL: establece los valores de la columna relacionada en NULL cuando se elimina o actualiza un registro en la tabla principal.
SET DEFAULT: establece los valores de la columna relacionada en su valor predeterminado cuando se elimina o actualiza un registro en la tabla principal.
RESTRICT: evita la eliminación o actualización de un registro en la tabla principal si hay registros relacionados en la tabla relacionada.
Ejemplo
CREATE TABLE lenguajes (
  lenguaje_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  lenguaje VARCHAR(30) NOT NULL
);

CREATE TABLE entornos (
  entorno_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  entorno VARCHAR(30) NOT NULL
);

CREATE TABLE frameworks (
  framework_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  framework VARCHAR(30) NOT NULL,
  lenguaje INT UNSIGNED,
  entorno INT UNSIGNED,
  FOREIGN KEY (lenguaje)
    REFERENCES lenguajes(lenguaje_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE,
  FOREIGN KEY (entorno)
    REFERENCES entornos(entorno_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE
);

# Transacciones 
En SQL, una transacción es una secuencia de operaciones que se ejecutan como una sola unidad lógica e indivisible, como si fueran una única operación. Una transacción garantiza la integridad de los datos y la consistencia de la base de datos en caso de errores o fallas.

Una transacción típica implica una serie de operaciones que se realizan en una base de datos, como agregar, modificar o eliminar registros en una o más tablas.

Todas las operaciones de la transacción se realizan como una sola unidad, lo que significa que todas las operaciones deben completarse con éxito o ninguna de ellas debe ser efectiva.

Para iniciar una transacción en SQL, se utiliza la sentencia START TRANSACTION. Luego, se realizan las operaciones de la transacción, y si todas ellas se ejecutan correctamente, se utiliza la sentencia COMMIT para confirmar los cambios en la base de datos.

En caso de que se produzca un error o falla en alguna de las operaciones, se utiliza la sentencia ROLLBACK para deshacer todos los cambios y volver a un estado consistente de la base de datos.

START TRANSACTION;

  INSERT INTO tabla_1 (campo_1, campo_2, campo_3)
    VALUES ('valor_1', 'valor_2', 'valor_3');

  INSERT INTO tabla_2 (campo_1, campo_2, campo_3)
    VALUES ('valor_1', 'valor_2', 'valor_3');

  INSERT INTO tabla_3 (campo_1, campo_2, campo_3)
    VALUES ('valor_1', 'valor_2', 'valor_3');

COMMIT;

START TRANSACTION;

  INSERT INTO tabla_1 (campo_1, campo_2, campo_3)
    VALUES ('valor_1', 'valor_2', 'valor_3');

  INSERT INTO tabla_2 (campo_1, campo_2, campo_3)
    VALUES ('valor_1', 'valor_2', 'valor_3');

  INSERT INTO tabla_3 (campo_1, campo_2, campo_3)
    VALUES ('valor_1', 'valor_2', 'valor_3');

ROLLBACK;


# Procedimientos Almacenados
Un procedimiento almacenado o Stored Procedure en SQL es un conjunto de instrucciones que se almacenan en la base de datos y se pueden llamar y ejecutar varias veces mediante una sola llamada al procedimiento.

Estos procedimientos pueden aceptar parámetros de entrada y devolver valores de salida, y pueden ser utilizados para realizar operaciones complejas en la base de datos de manera eficiente y segura.

Los procedimientos almacenados también pueden ser utilizados para encapsular lógica de negocio y reducir la complejidad de las aplicaciones cliente al mover la lógica de la base de datos al servidor.

Sintaxis
DELIMITER //

CREATE PROCEDURE nombre_procedimiento(
  IN valor_entrada TIPO_DATO,
  IN valor_entrada_2 TIPO_DATO,
  OUT valor_salida TIPO_DATO
)

  BEGIN
    Código del Procedimiento Almacenado
  END //

DELIMITER ;
Una vez creado el procedimiento almacenado, podemos llamarlo con el siguiente código:

CALL nombre_procedimiento();
Eliminar un procedimiento y mostrar los procedimientos de una base de datos:

DROP PROCEDURE nombre_procedimiento();

SHOW PROCEDURE STATUS WHERE db = 'nombre_base_datos';
Ejemplo
Primero creamos las tablas necesarias para el ejemplo del procedimiento:

CREATE TABLE suscripciones (
  suscripcion_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  suscripcion VARCHAR(30) NOT NULL,
  costo DECIMAL(5,2) NOT NULL
);

INSERT INTO suscripciones VALUES
  (0, 'Bronce', 199.99),
  (0, 'Plata', 299.99),
  (0, 'Oro', 399.99);

CREATE TABLE clientes (
  cliente_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(30) NOT NULL,
  correo VARCHAR(50) UNIQUE
);

CREATE TABLE tarjetas (
  tarjeta_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  cliente INT UNSIGNED,
  tarjeta BLOB,
  FOREIGN KEY (cliente)
    REFERENCES clientes(cliente_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE
);

CREATE TABLE servicios(
  servicio_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  cliente INT UNSIGNED,
  tarjeta INT UNSIGNED,
  suscripcion INT UNSIGNED,
  FOREIGN KEY(cliente)
    REFERENCES clientes(cliente_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE,
  FOREIGN KEY(tarjeta)
    REFERENCES tarjetas(tarjeta_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE,
  FOREIGN KEY(suscripcion)
    REFERENCES suscripciones(suscripcion_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE
);
Ahora el código del procedimiento:

CREATE PROCEDURE sp_asignar_servicio(
  IN i_suscripcion INT UNSIGNED,
  IN i_nombre VARCHAR(30),
  IN i_correo VARCHAR(50),
  IN i_tarjeta VARCHAR(16),
  OUT o_respuesta VARCHAR(50)
)

  BEGIN

    DECLARE existe_correo INT DEFAULT 0;
    DECLARE cliente_id INT DEFAULT 0;
    DECLARE tarjeta_id INT DEFAULT 0;

    START TRANSACTION;

      SELECT COUNT(*) INTO existe_correo
        FROM clientes
        WHERE correo = i_correo;

      IF existe_correo <> 0 THEN

        SELECT 'Tu correo ya ha sido registrado' INTO o_respuesta;

      ELSE

        INSERT INTO clientes VALUES (0, i_nombre, i_correo);
        SELECT LAST_INSERT_ID() INTO cliente_id;

        INSERT INTO tarjetas
          VALUES (0, cliente_id, AES_ENCRYPT(i_tarjeta, cliente_id));
        SELECT LAST_INSERT_ID() INTO tarjeta_id;

        INSERT INTO servicios VALUES (0, cliente_id, tarjeta_id, i_suscripcion);

        SELECT 'Servicio asignado con éxito' INTO o_respuesta;

      END IF;

    COMMIT;

  END //

DELIMITER ;
Finalmente lo ejecutamos y vemos el resultado de la variable de respuesta y en las correspondientes tablas la inserción de datos:

CALL sp_asignar_servicio(2, 'Kenai', 'kenai@gmail.com', '1234567890123490', @res);
SELECT @res;

SELECT * FROM clientes;
SELECT * FROM tarjetas;
SELECT * FROM servicios;


# Disparadores 
Un disparador o Trigger es un objeto que se utiliza para ejecutar automáticamente una acción en respuesta a ciertos eventos en una base de datos, como INSERT, UPDATE o DELETE en una tabla específica.

Los disparadores se pueden utilizar para asegurarse de que ciertas acciones se realicen automáticamente después de que se realice un cambio en una tabla, o para evitar que se realicen ciertas acciones.

Por ejemplo, un disparador se puede utilizar para actualizar automáticamente una tabla de resumen después de que se realice un cambio en una tabla de detalles, o para evitar que se elimine un registro importante de una tabla.

Sintaxis
DELIMITER //
CREATE TRIGGER nombre_disparador
  [BEFORE | AFTER] [INSERT | UPDATE | DELETE]
  ON nombre_tabla
  FOR EACH ROW

  BEGIN
    Código del Disparador
  END //

DELIMITER ;
Eliminar un disparador y mostrar los disparadores de una base de datos:

DROP TRIGGER nombre_disparador;

SHOW TRIGGERS FROM base_de_datos;
Ejemplo
Para el ejemplo de este disparador, seguiremos usando el código de ejemplo de los procedimeintos almacenados, primero creamos una tabla donde se almacene el resultado de nuestro disparador:

CREATE TABLE actividad_clientes(
  ac_id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
  cliente INT UNSIGNED,
  fecha DATETIME,
  FOREIGN KEY (cliente)
    REFERENCES clientes(cliente_id)
    ON DELETE RESTRICT
    ON UPDATE CASCADE
);
Ahora creamos nuestro disparador:

CREATE TRIGGER tg_actividad_clientes
  AFTER INSERT
  ON clientes
  FOR EACH ROW

  BEGIN

    INSERT INTO actividad_clientes VALUES (0, NEW.cliente_id, NOW());

  END //

DELIMITER ;
Finalmente ejecutamos nuevamente el ejemplo del procedimiento almacenado y en cuanto se haga el INSERT a la tabla "clientes", el disparador se lanzará automáticamente.

CALL sp_asignar_servicio(2, 'Kenai', 'kenai@gmail.com', '1234567890123490', @res);
SELECT @res;
Para comprobar que el disparador se ejecuto revisamos la tabla "actividad_clientes":

SELECT * FROM actividad_clientes;

