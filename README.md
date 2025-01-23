
# JDBC: Java Database Connectivity

### ¿Qué es JDBC y cuáles son sus componentes?


**JDBC** (Java Database Connectivity) es una API estándar de Java que permite a las aplicaciones interactuar con bases de datos relacionales. Proporciona una interfaz para enviar consultas, realizar actualizaciones y administrar conexiones entre una aplicación Java y la base de datos.

## Componentes de JDBC

JDBC consta de varios elementos clave que permiten su funcionalidad:

**1.Driver JDBC**

    -Es un controlador que traduce las solicitudes de la aplicación Java al lenguaje de la base de datos.

    -Tipos de drivers:

  **Tipo 1**: Driver puente JDBC-ODBC.
       
  **Tipo 2**: Driver de API nativa.
       
  **Tipo 3**: Driver puente de red.
       
  **Tipo 4**: Driver directo (Thin Driver).

**2. DriverManager**

    -Administra los drivers registrados y facilita el establecimiento de conexiones.

    -Proporciona el método getConnection() para obtener una conexión a la base de datos.

    -Es el encargado de seleccionar el driver adecuado para interactuar con la base de datos.

**3. Connection**

    -Representa una conexión activa con la base de datos.
     
    -Es el punto de entrada para ejecutar sentencias SQL y manejar transacciones.
    
    -Métodos clave:
   
         *createStatement(): Crea un objeto Statement.
         
         *prepareStatement(): Crea un objeto PreparedStatement.
         
         *setAutoCommit(boolean autoCommit): Controla las transacciones.




  **4. Statement**
     -Es una interfaz que permite ejecutar consultas SQL y obtener resultados.
     
     -Tipos:

  **Statement**: Para ejecutar consultas simples.
     
 **PreparedStatement**: Para consultas SQL precompiladas con parámetros.

 **CallableStatement**: Para ejecutar procedimientos almacenados.


**5. ResultSet**
    -Es el conjunto de resultados devueltos por una consulta SQL.
    -Permite iterar por los datos fila por fila.
    -Métodos clave:
         *next(): Avanza a la siguiente fila.
         
         *getInt(String columnLabel), getString(String columnLabel): Obtiene datos de una columna.

**6. SQLException**
    -Es la excepción que se lanza cuando ocurre un error al interactuar con la base de datos.
    
    -Métodos importantes:
    
            *getMessage(): Proporciona un mensaje detallado del error.
            
            *getErrorCode(): Devuelve el código de error del proveedor de la base de datos.

### Documente 2 librerías de Scala que permitan conectarse a una base de datos relacional. En una tabla resuma sus diferencias.

# Conexión a Bases de Datos Relacionales en Scala

En Scala, dos de las principales bibliotecas utilizadas para interactuar con bases de datos relacionales son Slick y Doobie. Ambas permiten manejar bases de datos mediante el uso de la API JDBC, pero ofrecen enfoques diferentes para lograrlo.

## 1.Slick (Scala Language-Integrated Connection Kit

  **Descripción:**

     Slick es una biblioteca ORM funcional que traduce consultas Scala a SQL, permitiendo trabajar de forma declarativa y tipada con bases de datos. Es ideal para quienes 
     prefieren un enfoque más abstracto y orientado a objetos.

  **Características principales:**

      -Consultas SQL generadas automáticamente desde código Scala.
   
      -Validación tipada en tiempo de compilación.
   
     -Soporte para múltiples bases de datos como PostgreSQL, MySQL, SQLite, entre otras.
   
     -Compatible con programación asincrónica utilizando Future.

## 2. Doobie

  **Descripción:**
  
      Doobie es una biblioteca funcional pura que permite trabajar directamente con SQL, sin la capa de abstracción de un ORM. Está diseñada para ser altamente flexible y se 
      integra perfectamente con el ecosistema funcional de Scala (Cats, ZIO).
      
  **Características principales:**
        -Consultas SQL escritas directamente.
        -Validación tipada de consultas SQL en tiempo de compilación.
        
        -Manejo explícito de transacciones y alto control sobre las operaciones.
        
        -Compatible con asincronía mediante Cats Effect o ZIO.

 ## Tabla

 | **Aspecto**          | **Slick**                                              | **Doobie**                                               |
|----------------------|--------------------------------------------------------|----------------------------------------------------------|
| **Paradigma**        | ORM funcional con consultas Scala tipadas.             | Funcional puro con consultas SQL en crudo.               |
| **Flexibilidad**     | Moderada: Traduce Scala a SQL automáticamente.         | Alta: Consultas SQL totalmente personalizables.          |
| **Tipado**           | Validación tipada en tiempo de compilación.            | Validación SQL tipada en tiempo de compilación.          |
| **Integración**      | Compatible con Future y Akka Streams.                  | Integración con Cats, ZIO y monadas funcionales.         |
| **Soporte Asincrónico**| Sí, mediante Future.                                 | Sí, mediante Cats Effect o ZIO.                          |
| **Transacciones**    | Soporte limitado; manejo implícito.                    | Manejo explícito y detallado de transacciones.           |
| **Facilidad de Uso** | Ideal para principiantes que vienen de ORM.            | Más complejo, pero con mayor control.                    |


 

## Documentar cómo establecer una conexión a una base de datos relacional (mysql). Siga los siguientes pasos:

# Conexión a una Base de Datos MySQL desde Scala

Esta guía describe cómo establecer una conexión a una base de datos relacional MySQL desde Scala. Sigue los pasos descritos para crear una base de datos, una tabla con datos de prueba y realizar la conexión desde Scala.

### Genere una base de datos en mysql

**1. Crear una Base de Datos en MySQL**

  1.Abre tu cliente MySQL (MySQL Workbench, phpMyAdmin o terminal).

  2.Ejecuta el siguiente comando para crear una base de datos llamada testdb:

![image](https://github.com/user-attachments/assets/c728526a-9a49-436a-9913-e7b00fa5efb4)

  3.Selecciona la base de datos creada:

![image](https://github.com/user-attachments/assets/e85b1548-e2b2-413e-9e48-7e0f95810320)

### Genere una tabla con datos de prueba

**2. Crear una Tabla con Datos de Prueba**

   1.Crea una tabla llamada usuarios:

 ![image](https://github.com/user-attachments/assets/304e1aa9-4542-4268-8f49-c85eeb377b10)

   2.Inserta datos de prueba en la tabla:
   
![image](https://github.com/user-attachments/assets/aeb96380-ded5-40d4-bb49-9c03610bda61)

   3.Verifica los datos insertados:

 ![image](https://github.com/user-attachments/assets/b1c11428-1e91-4600-a819-f7f6ee0412e4)


### Desde Scala establezca la conexión a la base datos

**3. Establecer la Conexión desde Scala**

     Requisitos previos
     
     1.Tener instalado Scala y un IDE o entorno compatible(https://www.jetbrains.com/es-es/idea/download/?section=windows).
     
     2.Descargar el controlador JDBC para MySQL (https://dev.mysql.com/downloads/connector/j/). 
     
     3.Agregar el archivo .jar del conector al classpath del proyecto.
     
```scala
   libraryDependencies += "mysql" % "mysql-connector-java" % "8.0.29"

```
    
![image](https://github.com/user-attachments/assets/78f68984-f9ea-4fd8-af12-3f55e0530713)

# Código Scala

El siguiente código establece una conexión a la base de datos y muestra los datos de la tabla usuarios:

```scala
import java.sql.{Connection, DriverManager, ResultSet}

object ConsultaMySQL {
  def main(args: Array[String]): Unit = {
    // Datos de conexión
    val url = "jdbc:mysql://localhost:3306/testdata"  // URL de conexión
    val user = "root"                              // Usuario de MySQL
    val password = "nila"                 // Contraseña de MySQL

    var connection: Connection = null

    try {
      // Cargar el controlador JDBC
      Class.forName("com.mysql.cj.jdbc.Driver")

      // Establecer la conexión
      connection = DriverManager.getConnection(url, user, password)
      println("Conexión establecida correctamente.")

      // Crear una declaración para ejecutar la consulta
      val statement = connection.createStatement()

      // Ejecutar la consulta para seleccionar todos los datos de la tabla 'usuarios'
      val resultSet: ResultSet = statement.executeQuery("SELECT * FROM usuarios")

      // Imprimir los resultados
      println("Datos de la tabla 'usuarios':")
      while (resultSet.next()) {
        val id = resultSet.getInt("id")
        val nombre = resultSet.getString("nombre")
        val correo = resultSet.getString("correo")
        println(s"ID: $id, Nombre: $nombre, Correo: $correo")
      }
    } catch {
      case e: Exception =>
        // Si hay un error, imprimir el mensaje
        e.printStackTrace()
    } finally {
      // Cerrar la conexión si se ha establecido
      if (connection != null) connection.close()
    }
  }
}
```

**Conexión a la Base de Datos:**

Se utiliza DriverManager.getConnection para conectar a la base de datos testdb.
```Scala
// Establecer la conexión
      connection = DriverManager.getConnection(url, user, password)
      println("Conexión establecida correctamente.")
```
![image](https://github.com/user-attachments/assets/747eebaa-26c7-42e2-9ff7-38e9e3b167fe)


Asegúrate de reemplazar "tu_contraseña" con la contraseña de tu base de datos.
![image](https://github.com/user-attachments/assets/fb0402f1-ce3a-4079-9443-8a71022c6f6a)

**Consulta SQL:**

El código ejecuta una consulta SELECT * FROM usuarios para obtener todos los registros de la tabla usuarios.
```Scala
 // Ejecutar la consulta para seleccionar todos los datos de la tabla 'usuarios'
      val resultSet: ResultSet = statement.executeQuery("SELECT * FROM usuarios")
```

**Impresión de Resultados:**

Utiliza un ResultSet para recorrer y mostrar los datos obtenidos de la consulta.
```Scala
// Imprimir los resultados
      println("Datos de la tabla 'usuarios':")
      while (resultSet.next()) {
        val id = resultSet.getInt("id")
        val nombre = resultSet.getString("nombre")
        val correo = resultSet.getString("correo")
        println(s"ID: $id, Nombre: $nombre, Correo: $correo")
      }
```
![image](https://github.com/user-attachments/assets/a2c5c3c2-cc43-41d4-abec-450fbde8fc9f)

## Referencias:
**Baeldung - Introducción a Slick (Scala)**
https://www.baeldung.com/scala/slick-intro

**Baeldung - Introducción a Doobie (Scala)**
https://www.baeldung.com/scala/doobie-intro

**MySQL - Crear una Tabla**
https://dev.mysql.com/doc/refman/8.0/en/create-table.html

**CodersFree - Creación de Tablas en MySQL (Curso)**
https://codersfree.com/courses-status/aprende-php-y-mysql-desde-cero/creacion-de-tablas-en-mysql
