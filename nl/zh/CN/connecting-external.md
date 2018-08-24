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

# 连接外部应用程序
{: #connecting-external-app}

有两种方法可将外部应用程序连接到 {{site.data.keyword.composeForMySQL_full}}：

- **连接字符串**可由某些客户机库使用，并包含其他库连接所需的所有信息。

- **命令行**是一个预先格式化的命令，它将使用正确的参数来调用 `mysql`。

您将在 {{site.data.keyword.composeForPostgreSQL}} 服务的*概述*页面上找到这两项。

连接到 MySQL for Compose 部署所需的所有信息。
* 如何对数据库使用[连接字符串](#section-the-connection-string)。
* 如何使用 [SSL](#section-ssl-and-mysql) 和[自签名证书](#section-using-the-self-signed-certificate)。
* 如何通过[命令行](#section-connecting-from-the-command-line)或[应用程序](#section-connecting-your-application)进行连接。

## 连接字符串

连接字符串是连接至 Compose for MySQL 时的第一个引用点；它包含连接到数据库所需的几乎所有信息。

```
mysql://[username]:[password]@[host]:[port]/compose
```

**注：**本指南中的示例使用管理员用户帐户进行连接。管理员用户是具有完全特权的用户，对所有数据库具有管理访问权。但是，出于安全原因，管理员帐户只能用于创建用户并授予其特权，而不得连接到应用程序。

连接字符串将格式化为可在驱动程序和应用程序理解标准化格式的情况下使用的 URI。其他应用程序可以从连接字符串 URI 中抽取基本详细信息。

其他驱动程序使用连接 URI 的组成部分（主机名和端口）作为它们的连接参数。主机名可在 `@` 符号后找到，而端口号位于 `:` 的后面。

如果未指定要连接到的数据库，那么需要 `USE my_database` 命令来选择数据库；MySQL 连接不必指定要连接的数据库。

## SSL 和 MySQL

缺省情况下，所有 Compose for MySQL 部署都会启用 SSL；但是，MySQL 通过 SSL 的方式表示它也接受非 SSL 连接。这意味着在配置应用程序的 MySQL 驱动程序时，需要确保它创建安全连接。使用 MySQL 命令行，可以通过将 `--ssl-mode=REQUIRED` 添加到连接命令来完成此操作。对于应用程序驱动程序，设置特定于驱动程序。在以下示例中，我们将显示应始终连接以及仅在启用 SSL 的情况下才连接的命令。

## 使用自签名证书

Compose 部署提供了自签名证书，可用于验证要交谈的主机。

要使用自签名证书，请将其复制到文件。该证书可在 {{site.data.keyword.composeForElasticsearch}} 服务的*概述*页面上找到。 

将 `-----BEGIN CERTIFICATE-----` 到 `-----END CERTIFICATE-----` 的文本复制并粘贴到扩展名为 `.cert` 或 `.pem` 文件中，具体取决于连接驱动程序的需要。将文件保存到您可以访问的位置，因为稍后将需要证书的路径。

## 通过命令行进行连接

要直接连接到 Compose for MySQL 部署并对其进行管理，可以使用命令行。要这样做，必须在本地机器上安装 MySQL。每个平台都有自己的安装软件包，因此请选择最适合您的安装软件包。您可以在以下网址找到 Oracle 社区包：[http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/)。在从该处进行下载之前，请注意在 Linux 上，您通常会在分发库中找到 MySQL。如果您使用的是 Mac，那么可以使用 Homebrew 安装 MySQL，其会编译和安装最新版本。

要通过终端访问部署，请将*连接信息*面板中提供的命令行字符串复制并粘贴到您的终端以连接到您的部署。

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

要在连接时启用 SSL，请使用 `--ssl-mode=REQUIRED`。缺省用户名为“admin”，在 `-u` 参数中用作该用户名。运行该命令后，将提示您输入 admin 用户的密码，您可以从*连接信息*面板的凭证部分获取该密码。

缺省情况下，Compose for MySQL 会启用 SSL，但是在连接时，应在命令行上使用 `--ssl-mode=REQUIRED` 选项来采取额外的预防措施。这会防止 MySQL 因任何原因回退到未加密连接。

如果愿意，可以使用自签名证书进行验证。将 `--ssl-mode` 参数更改为 `--ssl-mode=VERIFY_CA`，然后使用 .pem 文件的路径和名称添加 `--ssl-ca`：

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## 连接您的应用程序

您的应用程序将使用部署的连接字符串连接到 Compose for MySQL。此快速连接指南涵盖了连接驱动程序，并提供了适用于 JavaScript、Go、Python、Java 和 Ruby 的代码样本。

## 使用 JavaScript 和 Node.js 进行连接

MySQL for Node.js 的主要驱动程序是 [node-mysql 驱动程序](https://github.com/mysqljs/mysql)。我们将在此了解设置简单 Node.js/MySQL 连接。如果要继续执行此操作，请确保系统上安装了 [Node.js](https://nodejs.org/) 和 [npm](https://github.com/npm/npm)。

使用 `npm init` 初始化新项目后，在项目的文件夹中安装驱动软件包：

```shell
npm install mysql --save
```

驱动程序及其依赖项安装在 `node_modules` 文件夹中，并且驱动程序将出现在 `package.json` 文件中的 `dependencies` 下。

您可以使用以下代码连接到 MySQL。

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

**注释**
- `SHOW DATABASES` 是一个 MySQL 命令，它会列示用户具有特权的数据库。
- 因为脚本使用 _admin_ 用户，所以将显示部署中的所有数据库。
- 查询结果作为对象数组返回。

## 使用 Go 进行连接

Go 具有 [SQL 数据库的通用接口](https://golang.org/pkg/database/sql/)，将其与 [go-sql-driver](https://github.com/go-sql-driver/mysql) 配合使用将为我们提供多种选择以连接到 MySQL。驱动程序的问题是我们无法验证自签名证书。具有自签名证书的唯一 TLS/SSL 选项是 `skip-verify`，这不太理想。

要使用 Go 连接到 MySQL，首先将 _go-sql-driver_ 软件包安装到 `$GOPATH`：

```shell
go get github.com/go-sql-driver/mysql
```

您可以使用以下代码连接到 MySQL。

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

## 使用 Python 进行连接

您可以使用 [MySQL 的官方 Python 连接器](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html)连接到具有 Python 的 MySQL。

首先，安装[连接器软件包](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html)。安装软件包后，可以使用以下代码连接到数据库：
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

注：
- 此示例导入 MySQL 连接器，并在 `config` 字典中添加任何连接参数。使用连接字典中部署的自签名证书来初始化安全连接。
- `ssl_verify_cert` 需要 `ssl_ca` 选项。使用配置选项 `'ssl_verify_cert': True`，确保服务器的证书和 `cert.pem` 中存储的证书相同。如果存在证书错误，那么会返回 `ValueError`，指示证书不匹配。
- 可以在[此处](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)找到可用连接自变量的有用列表。
- MySQL Python 连接器要求对 `cursor` 对象进行实例化，以便执行 SQL 查询。在此代码样本中，将为此处的连接对象的 `cursor` 方法指定变量 `cur`，并将变量 `query` 指定给 SQL 命令，告诉 MySQL 显示所有部署数据库。
- `execute` 方法用于执行通过安全连接将 Python 对象转换为 MySQL 命令的数据库操作。在此示例中，执行方法告诉 MySQL 在将输出记录到控制台并关闭连接之前，将显示所有数据库并对它们进行迭代。

## 使用 Java 进行连接

要使用 Java 进行连接，请首先下载并安装 MySQL 的 [Connector/J JDBC 驱动程序](https://dev.mysql.com/downloads/connector/j/)。

然后，您可以使用以下代码连接到部署：

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
注释
- 用于设置连接的基本信息在连接字符串中。我们使用连接字符串搭配 JDBC API 并在变量 `URL` 中存储该字符串：
- 部署的用户名和密码存储在单独的变量中，这些变量用于搭配 JDBC `DriverManager.getConnection()` 方法来建立连接。
- 连接字符串包括主机名、端口和数据库；SSL 选项将附加到连接字符串。
- 样本会建立 SSL 连接，该连接使用自签名证书进行验证。您可以不使用这些选项连接到服务器，但连接会不安全，并会导致 MySQL 警告：
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- 为允许驱动程序处理证书，凭证会保存在名为 `cert.pem` 的文件中。无法直接使用证书。相反，请使用 `keytool` 创建信任库以保存证书的凭证。以下命令将导入 `cert.pem` 文件、为其指定别名 `composeCert`，并将输出文件定义为称为 `truststore` 的密钥库。它使用密码 `henrythedog` 来将密钥库解锁。
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- `javax.net.ssl.trustStore` 和 `javax.net.ssl.trustStorePassword` 上的 `setProperty` 方法使用密钥库中的信息。系统属性应设置在程序的顶部以在运行时及早运行；最好在设置 `Connection` 变量之前，以便在启动 SSL 连接之前锁定这些系统属性。
- 创建连接后，将返回 Statement 对象并对该对象执行查询。这将返回一个 ResultSet，用于迭代和打印数据库名称。

## 使用 Ruby 进行连接

有许多适用于 Ruby 的 MySQL 驱动程序。样本连接代码使用 [MySQL2](https://github.com/brianmario/mysql2)。

您可以根据驱动程序 Github 存储库中的指示信息安装 MySQL2 并使用以下代码连接到 MySQL：
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
注释
- `config` 散列包含所有连接配置，包括设置 SSL 连接。有关所有配置选项的详细信息，请参阅 [MySQL2 自述文件](https://github.com/brianmario/mysql2)。
- 要使用自签名证书设置安全连接，请设置 `sslCA` 和 `sslverify`。`sslCA` 是包含证书的 `.pem` 或 `.cert` 文件的路径，`sslverify` 设置为 `true` 以检查有效证书。
-  `Mysql2::Client.new` 构造函数使用 `config` 中的连接配置来初始化新的连接变量。
- `results` 包含一组散列，这些散列会迭代并打印到控制台。
