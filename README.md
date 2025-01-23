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
CREATE DATABASE testdb;

USE testdb;

CREATE TABLE empleados (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100),
    puesto VARCHAR(100)
);

INSERT INTO empleados (nombre, puesto) VALUES 
('Juan Pérez', 'Desarrollador'),
('Ana López', 'Analista');
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
    val password = "tu_contraseña"
    
    DriverManager.getConnection(url, username, password)
  }

  def main(args: Array[String]): Unit = {
    val connection = conectar()
    println("Conexión establecida con éxito!")
    connection.close()
  }
}
```

