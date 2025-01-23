# B2 Trabajo-Consulta 2

## JDBC y Conexión a Base de Datos Relacional con Scala

Este repositorio contiene información y ejemplos sobre cómo conectar una aplicación Scala a una base de datos relacional utilizando JDBC y algunas librerías de Scala.

## ¿Qué es JDBC y cuáles son sus componentes?

JDBC (Java Database Connectivity) es una API de Java que permite a las aplicaciones Java (y por extensión, aplicaciones Scala) interactuar con bases de datos relacionales. JDBC proporciona una interfaz estándar para realizar consultas, actualizaciones y otras operaciones sobre bases de datos.

### Componentes principales de JDBC:

- **Driver**: Un controlador que implementa la interfaz `java.sql.Driver` y se comunica con la base de datos.
- **Connection**: Representa una conexión a la base de datos.
- **Statement**: Se usa para ejecutar consultas SQL.
- **ResultSet**: Contiene los resultados de una consulta SQL.
- **SQLException**: Excepción que se lanza en caso de errores durante la conexión o ejecución de consultas.

---

## Librerías Scala para Conexión a Base de Datos Relacional

Existen varias librerías en Scala para interactuar con bases de datos relacionales. Aquí se describen dos de ellas: `Slick` y `Doobie`.

| Característica      | **Slick**                                         | **Doobie**                                    |
|---------------------|--------------------------------------------------|-----------------------------------------------|
| **Tipo de API**     | ORM (Mapeo objeto-relacional)                    | JDBC funcional y funcionalmente pura          |
| **Soporte de bases de datos** | Compatible con varias bases de datos como MySQL, PostgreSQL, etc. | Compatible con MySQL, PostgreSQL, H2, entre otros |
| **Abstracción**     | Proporciona un nivel alto de abstracción con funciones como `Table` y `Query`. | Menos abstracción, más control sobre el SQL. |
| **Comodidad**       | Ofrece más comodidad al trabajar con Scala gracias a su integración con el lenguaje. | Menos integración directa con Scala, pero más flexibilidad. |

---

## Establecer Conexión a una Base de Datos Relacional (MySQL)

### Paso 1: Crear la base de datos en MySQL

Para crear la base de datos en MySQL, puedes usar el siguiente comando:

```sql
CREATE DATABASE test_db;
USE test_db;

CREATE TABLE estudiantes (
    cedula INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    edad INT NOT NULL
);

INSERT INTO estudiantes (nombre, edad) VALUES
('Luis Aguilar', 18),
('Andres Cardenas', 20),
('Alex Serrano', 21);

select * from estudiantes;
```
### Conectar a MySQL desde Scala:
> Para conectar desde Scala a MySQL, se requiere un controlador JDBC. Se debe incluir la dependencia en el archivo build.sbt:

```scala
libraryDependencies += "mysql" % "mysql-connector-java" % "8.0.23"
```

### El siguiente código establece la conexión:

```scala
import java.sql.{Connection, DriverManager}

object ConexionMySQL {

  def conectar(): Connection = {
    val url = "jdbc:mysql://localhost:3306/testdb"
    val username = "root"
    val password = "utpl"
    
    DriverManager.getConnection(url, username, password)
  }

  def main(args: Array[String]): Unit = {
    val connection = conectar()
    println("Conexion establecida")
    connection.close()
  }
}
```
## CAPTURA EN Mysql
![WhatsApp Image 2025-01-22 at 20 38 56_20f37a3e](https://github.com/user-attachments/assets/553d53d2-b415-4cb1-b09f-250692ec1072)

## CAPTURA EN SCALA
![1](https://github.com/user-attachments/assets/0bb3f20a-a20f-454a-8a39-89af1ffd7037)


