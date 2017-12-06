---

copyright:
  years: 2017
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión de una aplicación externa
{: #connecting-external-app}

Hay dos formas de conectar una aplicación externa a {{site.data.keyword.composeForMySQL_full}}:

- Algunas bibliotecas de cliente pueden utilizar una **serie de conexión**, que contiene toda la información necesaria para que se conecten otras bibliotecas.

- La **línea de mandatos** es un mandato preformateado que invocará `mysql` con los parámetros correctos.

Encontrará ambas en la página *Visión general* del servicio {{site.data.keyword.composeForPostgreSQL}}.

Toda la información que necesita para establecer conexión con un despliegue de MySQL for Compose.
* Cómo utilizar las [series de conexión](#section-the-connection-string) para las bases de datos.
* Cómo utilizar [SSL](#section-ssl-and-mysql) y el [certificado autofirmado](#section-using-the-self-signed-certificate).
* Cómo conectarse a través de la [línea de mandatos](#section-connecting-from-the-command-line) o desde las [aplicaciones](#section-connecting-your-application).

## La serie de conexión

La serie de conexión es el primer punto de referencia cuando se conecta a Compose for MySQL; contiene casi toda la información que necesita para conectarse a una base de datos.

```
mysql://[username]:[password]@[host]:[port]/compose
```

**Nota:** Los ejemplos de esta guía conectan con la cuenta de usuario admin. El usuario administrador es un usuario con privilegios completos que tiene acceso administrativo a todas nuestras bases de datos. Sin embargo, por razones de seguridad, la cuenta admin solo debe utilizarse para crear usuarios y otorgarles privilegios, no para conectar con aplicaciones.

La serie de conexión está formateada como un URI que se pueden utilizar cuando los controladores y las aplicaciones comprenden el formato estandarizado. Otras aplicaciones pueden extraer los detalles esenciales del URI de la serie de conexión.

Otros controladores utilizan piezas de componentes del URI de la conexión - el nombre de host y el puerto - para sus parámetros de conexión. El nombre del host está después del símbolo `@` y el número de puerto después de `:`.

Si no indica una base de datos con la que conectarse, necesita el mandato `USE my_database` para seleccionar una base de datos; una conexión MySQL no tiene que especificar una base de datos a la que conectarse.

## SSL y MySQL

Todos los despliegues de Compose for MySQL tienen SSL habilitado de forma predeterminada; sin embargo, la forma en que MySQL utiliza SSL implica que también aceptará conexiones que no sean SSL. Esto significa que, cuando configure el controlador MySQL de la aplicación, deberá asegurarse de que crea una conexión segura. Con la línea de mandatos de MySQL, puede hacerlo añadiendo `--ssl-mode=REQUIRED` al mandato de conexión. Para los controladores de aplicaciones, los valores son específicos del controlador. En los ejemplos mostraremos mandatos que siempre y solo deben conectarse con SSL habilitado.

## Utilización del certificado autofirmado

Los despliegues de Compose ofrecen un certificado autofirmado, que se puede utilizar para validar el host con el que se establece conexión.

Para utilizar el certificado autofirmado, cópielo en un archivo. El certificado se encuentra en la página *Visión general* del servicio {{site.data.keyword.composeForElasticsearch}}. 

Copie y pegue el texto comprendido entre `-----BEGIN CERTIFICATE-----` y `-----END CERTIFICATE-----` en un archivo con la extensión `.cert` o `.pem`, en función de cuál necesite el controlador de la conexión. Guarde el archivo en una ubicación a la que pueda acceder porque necesitará esta vía de acceso al certificado más adelante.

## Conexión desde la línea de mandatos

Para conectarse directamente al despliegue de Compose MySQL y administrarlo, puede utilizar la línea de mandatos. Para ello, debe instalar MySQL en la máquina local. Cada plataforma tiene sus propios paquetes de instalación; elija el que mejor se adapte a su plataforma. Encontrará los paquetes de la comunidad Oracle en [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/). Antes de descargarlos desde allí, tenga en cuenta que en Linux normalmente encontrará MySQL en el repositorio de distribuciones. Si utiliza un Mac, puede instalar MySQL con Homebrew, que compila e instala la versión más reciente.

Para acceder a su despliegue a través del terminal, copie y pegue la serie de línea de mandatos proporcionada en el panel *Información de conexión* del terminal para conectarse a su despliegue.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

Para habilitar SSL al conectarse, utilice `--ssl-mode=REQUIRED`. El usuario predeterminado se denomina "admin", que se utiliza como nombre de usuario en el parámetro `-u`. Después de ejecutar el mandato, se le solicitará que especifique la contraseña del usuario admin, que puede obtener de la sección de credenciales del panel *Información de conexión*.

Compose for MySQL tiene SSL habilitado de forma predeterminada, pero, cuando se conecte, debe tomar precauciones adicionales utilizando la opción `--ssl-mode=REQUIRED` en la línea de mandatos. Esto detiene la reserva de MySQL, por alguna razón, a una conexión no cifrada.

Si lo prefiere, puede utilizar el certificado autofirmado para la verificación. Cambie el parámetro `--ssl-mode` por `--ssl-mode=VERIFY_CA` y añada `--ssl-ca` con el nombre y vía de acceso del archivo .pem:

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## Conexión de la aplicación

La aplicación se conectará a Compose for MySQL utilizando la serie de conexión de su despliegue. Esta guía rápida de conexión cubre los controladores de conexión y proporciona ejemplos de código para JavaScript, Go, Python, Java y Ruby.

## Conexión con JavaScript y Node.js

El principal controlador de MySQL for Node.js es el [controlador node-mysql](https://github.com/mysqljs/mysql). Aquí examinaremos una conexión Node.js/MySQL sencilla. Si desea examinarla, asegúrese de que [Node.js](https://nodejs.org/) y [npm](https://github.com/npm/npm) estén instalados en el sistema.

Después de inicializar un proyecto nuevo mediante `npm init`, instale el paquete del controlador en la carpeta del proyecto:

```shell
npm install mysql --save
```

El controlador y sus dependencias se instalan en la carpeta `node_modules` y el controlador aparecerá bajo `dependencies` en el archivo `package.json`.

Puede utilizar el código siguiente para conectarse a MySQL.

```javascript
const mysql = require('mysql');
const fs = require('fs');

const connection = mysql.createConnection(
    {
        host: 'aws-us-east-1-portal.23.dblayer.com',
        port: 15942,
        user: 'admin',
        password: 'mypass',
        ssl: {
            ca: fs.readFileSync(__dirname + '/cert.crt')
        }
});

connection.query('SHOW DATABASES', (err, rows) => {  
    if (err) throw err;
    console.log('Connected!');
    for (let i = 0, len = rows.length; i < len; i++) {
        console.log(rows[i]['Database'])
    }
});
```

**Notas**
- `SHOW DATABASES` es un mandato de MySQL que muestra una lista de las bases de datos sobre las que un usuario tiene privilegios.
- Se muestran todas las bases de datos del despliegue porque el script utiliza el usuario _admin_.
- Los resultados de la consulta se devuelven como una matriz de objetos.

## Conexión con Go

Go tiene una [interfaz genérica para bases de datos SQL](https://golang.org/pkg/database/sql/) y si se utiliza con [go-sql-driver](https://github.com/go-sql-driver/mysql) se puede disponer de varias opciones para conectar con MySQL. El problema con el controlador es que no podemos verificar el certificado autofirmado. La única opción de TLS/SSL que tenemos con certificados autofirmados es `skip-verify`, que no es lo óptimo.

Para conectar con MySQL mediante Go, primero instale el paquete _go-sql-driver_ en `$GOPATH`:

```shell
go get github.com/go-sql-driver/mysql
```

Puede utilizar el código siguiente para conectarse a MySQL.

```go
package main

import (
    "database/sql"
    "log"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

func main() {  
    db, err := sql.Open("mysql", "admin:mypass@tcp(aws-us-east-1-portal.23.dblayer.com:15918)/compose?tls=skip-verify")
	if err != nil {
        log.Fatal(err)
    }
    defer db.Close()

	rows, err := db.Query("SHOW DATABASES")
    if err != nil {
    	log.Fatal(err)
    }

	var dbNames string
    for rows.Next() {
    	err := rows.Scan(&dbNames)
    	if err != nil {
        log.Fatal(err)
    	}
    	fmt.Println(dbNames)
    }
}
```

## Conexión con Python

Puede conectarse a MySQL con Python utilizando el [conector Python oficial de MySQL](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html).

En primer lugar, instale el [paquete del conector](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html). Después de instalar el paquete, puede conectarse a la base de datos con el código siguiente:
```python
import mysql.connector

config = {
    'user': 'admin',
    'password': 'mypass',
    'host': 'aws-us-east-1-portal.23.dblayer.com',
    'port': 15942,
    'database': 'compose',

    # Create SSL connection with the self-signed certificate
    'ssl_verify_cert': True,
    'ssl_ca': 'cert.pem'
}

connect = mysql.connector.connect(**config)
cur = connect.cursor()
cur.execute("SHOW DATABASES")

for row in cur:
    print(row[0])

connect.close() 
```

Notas:
- El ejemplo importa el conector MySQL y añade los parámetros de conexión en un diccionario `config`. Se inicializa una conexión segura utilizando el certificado autofirmado del despliegue del diccionario de conexión.
- `ssl_verify_cert` necesita la opción `ssl_ca`. Si utiliza la opción de configuración `'ssl_verify_cert': True` se asegura de que el certificado del servidor y el certificado guardado en `cert.pem` coinciden. Si hay un error de certificado, se devuelve un `ValueError`, que indica que los certificados no coinciden.
- Encontrará una lista útil de los argumentos de conexión disponibles [aquí](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html).
- El conector MySQL Python necesita que se cree una instancia del objeto `cursor` para poder ejecutar consultas SQL. En este ejemplo de código, al método `cursor` del objeto de conexión se le asigna la variable `cur` y la variable `query` se asigna al mandato SQL, lo que indica a MySQL que muestre todas las bases de datos del despliegue.
- El método `execute` ejecuta operaciones de base de datos que convierten objetos Python en mandatos MySQL sobre una conexión segura. En este ejemplo, el método de ejecución indica a MySQL que muestre todas las bases de datos, iterando sobre las mismas, antes de registrar la salida en la consola y de cerrar la conexión.

## Conexión con Java

Para conectarse con Java, primero descargar e instalar el [controlador JDBC Connector/J](https://dev.mysql.com/downloads/connector/j/) de MySQL.

Luego podrá conectarse a un despliegue con el siguiente código:

```java
import java.sql.*;

public class Main {

    public static void main(String[] args) {

       System.setProperty("javax.net.ssl.trustStore","/home/project/truststore");
   		System.setProperty("javax.net.ssl.trustStorePassword","somepass");

       String user = "admin";
       String password = "mypass";
       String URL = "jdbc:mysql://aws-us-east-1-portal.23.dblayer.com:15942/compose" +

                "?verifyServerCertificate=true"+
                "&useSSL=true" +
                "&requireSSL=true";
        try {

            Connection conn = DriverManager.getConnection(URL, user, password);

            Statement st = conn.createStatement();
            ResultSet rs = st.executeQuery("SHOW DATABASES");

            while (rs.next()) {
                String dbname = rs.getString("Database");
                System.out.format("%s\n", dbname);
            }

            st.close();

        } catch (Exception ex) {
            ex.printStackTrace();
            System.out.println("Failed");
        }
    }
}
```
Notas
- La información básica para configurar una conexión está dentro de la serie de conexión. La utilizamos que con la API JDBC y almacenamos dicha serie en la variable `URL`:
- El nombre de usuario y la contraseña del despliegue se almacenan en variables separadas, que se utilizan para establecer una conexión con el método `DriverManager.getConnection()` de JDBC.
- La serie de conexión incluye el nombre de host, el puerto y la base de datos; las opciones de SSL se añaden a la serie de conexión.
- El ejemplo establece una conexión SSL, que se verifica mediante el certificado autofirmado. Puede conectarse al servidor sin estas opciones, pero la conexión sería insegura y generaría un aviso de MySQL:
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- Para permitir que el controlador procese el certificado, las credenciales se guardan en un archivo denominado `cert.pem`. El certificado no se puede utilizar directamente. Debe crear un almacén de confianza que contendrá las credenciales del certificado utilizando `keytool`. El mandato siguiente importa el archivo `cert.pem`, le asigna el alias `composeCert` y define el archivo de salida como un almacén de claves llamado `truststore`. Utiliza la contraseña `henrythedog` para desbloquear el almacén de claves.
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- El método `setProperty` de `javax.net.ssl.trustStore` y `javax.net.ssl.trustStorePassword` utiliza la información del almacén de claves. Las propiedades del sistema se deben establecer hacia el principio del programa para que se ejecuten pronto durante el tiempo de ejecución; preferiblemente antes de que se defina la variable `Connection`, para que se bloqueen antes de iniciar una conexión SSL.
- Después de crear la conexión, se devuelve un objeto Statement y la consulta se ejecuta sobre el objeto. Esto devuelve un ResultSet que se utiliza para iterar y mostrar los nombres de base de datos.

## Conexión con Ruby

Hay varios controladores de MySQl para Ruby. El código de conexión de ejemplo utiliza [MySQL2](https://github.com/brianmario/mysql2).

Puede conectarse a MySQL instalando MySQL2 según las instrucciones del repositorio Github del controlador y utilizando el código siguiente:
```ruby
require "mysql2"  
config = {
    "hostname": "aws-us-east-1-portal.23.dblayer.com",
    "port": 15942,
    "database": "compose",
    "username": "admin",
    "password": "mypass",
    "sslCA": "cert.pem",
    "sslverify": true
}
conn = Mysql2::Client.new(config)
results = conn.query("SHOW DATABASES")
results.each {|row| puts row["Database"]}  
```
Notas
- El hash `config` contiene toda la configuración de conexión, incluida la configuración de una conexión SSL. Para obtener más información sobre todas las opciones de configuración, consulte el archivo [readme de MySQL2](https://github.com/brianmario/mysql2).
- Para configurar una conexión segura mediante el certificado autofirmado, se establecen `sslCA` y `sslverify`. `sslCA` es la vía de acceso del archivo `.pem` o `.cert` que contiene el certificado y `sslverify` se establece en `true` para comprobar si el certificado es válido.
-  El constructor `Mysql2::Client.new` inicializa una nueva variable de conexión utilizando la configuración de la conexión de `config`.
- `results` contiene una matriz de hashes, por los que se itera y que se muestran en la consola.
