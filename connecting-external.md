---

copyright:
  years: 2017,2018
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connecting an external application
{: #connecting-external-app}

There are two ways of connecting an external application to {{site.data.keyword.composeForMySQL_full}}:

- A **Connection String** can be used by some client libraries and contains all the information needed for other libraries to connect.

- **Command Line** is a preformatted command which will invoke `mysql` with the correct parameters.

You'll find both on the *Overview* page of your {{site.data.keyword.composeForPostgreSQL}} service.

All the information you need to connect to a MySQL for Compose deployment.
* How to use the [connection strings](#section-the-connection-string) for your databases.
* How to use [SSL](#section-ssl-and-mysql) and the [self-signed certificate](#section-using-the-self-signed-certificate).
* How to connect via the [command line](#section-connecting-from-the-command-line) or from your [applications](#section-connecting-your-application).

## The Connection String

The connection string is your first point of reference when connecting to Compose for MySQL; it contains almost all the information you need to connect to a database.

```
mysql://[username]:[password]@[host]:[port]/compose
```

**Note:** The examples in this guide connect with the admin user account. The admin user is a fully privileged user who has administrative access to all our databases. However, for security reasons, the admin account should only be used to create users and grant them privileges, and not to connect to applications.

The connection string is formatted as a URI that can be used where drivers and applications understand the standardized format. Other applications can extract the essential details from the connection string URI.

Other drivers use component parts of the connection URI – the host name and port – for their connection parameters. The host name is found after the `@` symbol and the port number is after the `:`.

If you don't designate a database to connect to, you need the `USE my_database` command to select a database; a MySQL connection doesn't have to specify a database to connect.

## SSL and MySQL

All Compose for MySQL deployments have SSL enabled by default; however, the way MySQL does SSL means it will also accept non-SSL connections. This means that, when configuring your application's MySQL driver, you need to ensure that it creates a secure connection. With the MySQL command line, you can do this by adding `--ssl-mode=REQUIRED` to the connection command. For application drivers, the settings are specific to the driver. In the examples we will show commands that should always and only connect with SSL enabled.

## Using the Self-Signed Certificate

Compose deployments offer a self-signed certificate, which can be used to validate the host being talked to.

To use the self-signed certificate, copy it to a file. The certificate is found on the *Overview* page of your {{site.data.keyword.composeForElasticsearch}} service. 

Copy and paste the text from `-----BEGIN CERTIFICATE-----` to `-----END CERTIFICATE-----` into a file with the extension `.cert` or `.pem`, depending on which the connection driver requires. Save the file to a location that you can access because we'll need the certificate's path later.

## Connecting from the Command Line

To directly connect to and administrate your Compose for MySQL deployment, you can use the command line. To do so, you have to install MySQL on your local machine. Each platform has its own installation packages, so choose the one that works best for you. You can find Oracle community packages at [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/). Before you download from there, be aware that on Linux you will usually find MySQL in your distributions repository. If you're using a Mac, you can install MySQL with Homebrew, which compiles and installs the latest version.

To access your deployment via the terminal, copy and paste the command line string provided in the *Connection info* panel into your terminal to connect to your deployment.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

To enable SSL when connecting, use `--ssl-mode=REQUIRED`. The default user is named "admin" which you use as the username in the `-u` parameter. After running the command, you'll be prompted to enter the admin user's password, which you can get from the credentials section of the *Connection info* panel.

Compose for MySQL has SSL enabled by default, but when connecting, you should take extra precautions by using the`--ssl-mode=REQUIRED` option on the command line. This stops MySQL falling back, for whatever reason, to an unencrypted connection.

If you prefer, you can use the self-signed certificate to verify. Change the `--ssl-mode` parameter to `--ssl-mode=VERIFY_CA` and add `--ssl-ca` with the path and name of your .pem file:

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## Connecting Your Application

Your application will connect to Compose for MySQL using your deployment's connection string, This quick connection guide covers connection drivers and gives code samples for JavaScript, Go, Python, Java, and Ruby.

## Connecting with JavaScript and Node.js

The leading driver for MySQL for Node.js is the [node-mysql driver](https://github.com/mysqljs/mysql). We'll walk through setting up a simple Node.js/MySQL connection here. If you want to follow along, make sure that [Node.js](https://nodejs.org/) and [npm](https://github.com/npm/npm) are installed on your system.

After initializing a new project using `npm init`, install the driver package in the project’s folder:

```shell
npm install mysql --save
```

The driver and its dependencies are installed in the `node_modules` folder, and the driver will appear under `dependencies` in the `package.json` file.

You can use the following code to connect to MySQL.

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

**Notes**
- `SHOW DATABASES` is a MySQL command that lists the databases that a user has privileges for.
- All the databases in the deployment are displayed because the script uses the _admin_ user.
- The results of the query are returned as an array of objects.

## Connecting with Go

Go has a [generic interface for SQL databases](https://golang.org/pkg/database/sql/) and using it with the [go-sql-driver](https://github.com/go-sql-driver/mysql) will provide us with several options to connect to MySQL. The problem with the driver is that we cannot verify the self-signed certificate. The only TLS/SSL option we have with self-signed certificates is `skip-verify`, which is less than optimal.

To connect to MySQL using Go, first install the _go-sql-driver_ package to your `$GOPATH`:

```shell
go get github.com/go-sql-driver/mysql
```

You can use the following code to connect to MySQL.

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

## Connecting with Python

You can connect to MySQL with Python using  [MySQL's official Python connector](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html).

First, install the [connector package](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html). After installing the package, you can connect to our database using the following code:
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

Notes:
- The example imports the MySQL connector and adds any connection parameters within a `config` dictionary. A secure connection is initialized using the deployment's self-signed certificate in the connection dictionary.
- `ssl_verify_cert` requires the `ssl_ca` option. Using the configuration option `'ssl_verify_cert': True`, ensures that the server's certificate and the certificate stored in `cert.pem` are the same. If there's a certificate error, a `ValueError` is returned, indicating that the certificates don't match.
- A useful list of the available connection arguments can be found [here](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html).
- The MySQL Python connector requires that a `cursor` object be instantiated in order to execute SQL queries. In this code sample, the `cursor` method of the connection object here is assigned the variable `cur`, and the variable `query` is assigned to the SQL command, which tells MySQL to show all of the deployment's databases.
- The `execute` method executes database operations that convert Python objects to MySQL commands over a secure connection. In this example, the execution method tells MySQL to show all the databases, iterating over them, before logging the output to the console and closing the connection.

## Connecting with Java

To connect with Java, first download and install MySQL's [Connector/J JDBC driver](https://dev.mysql.com/downloads/connector/j/).

You can then connect to a deployment using the following code:

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
Notes
- The basic information to set up a connection is within the connection string. We use that with the JDBC API and store that string in the variable `URL`:
- The username and password for the deployment are stored in separate variables, which are used to establish a connection with the JDBC `DriverManager.getConnection()` method.
- The connection string includes the host name, port, and database; the SSL options are appended to the connection string.
- The sample establishes an SSL connection, which is verified using the self-signed certificate. You can connect to the server without these options, but the connection would be insecure and would result in a warning from MySQL:
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- To allow the driver to process the certificate, the credentials are saved in a file called `cert.pem`. The certificate cannot be used directly. Instead, create a trust store to hold the certificate's credentials using `keytool`, The following command imports the `cert.pem` file, assigns it the alias `composeCert`, and defines the output file as a keystore called `truststore`. It uses the password `henrythedog` to unlock the keystore.
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- The `setProperty` method on `javax.net.ssl.trustStore` and `javax.net.ssl.trustStorePassword` uses the information from the keystore. The system properties should be set towards the top of the program to run early at runtime; preferably before the `Connection` variable is set, so that they're locked in before starting an SSL connection.
- After creating the connection, a Statement object is returned and the query is executed against the object. This returns a ResultSet which is used to iterate through and print the database names.

## Connecting with Ruby

There are a number of MySQL drivers for Ruby. The sample connection code uses [MySQL2](https://github.com/brianmario/mysql2).

You can connect to MySQL by installing MySQL2 according to the instructions in the driver's Github repository and using the following code:
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
Notes
- The `config` hash contains all of the connection configuration, including setting up an SSL connection. For details of all the configuration options, see the [MySQL2 readme](https://github.com/brianmario/mysql2).
- To set up a secure connection using the self-signed certificate, `sslCA` and `sslverify` are set. `sslCA` is the path of the `.pem` or `.cert` file containing the certificate, and `sslverify` is set to `true` in order to check for a valid certificate.
-  The `Mysql2::Client.new` constructor initializes a new connection variable, using the connection configuration in `config`.
- `results` contains an array of hashes, which are iterated through and printed to the console.