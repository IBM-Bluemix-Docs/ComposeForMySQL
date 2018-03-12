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

# 連接外部應用程式
{: #connecting-external-app}

將外部應用程式連接至 {{site.data.keyword.composeForMySQL_full}} 的方式有兩種：

- **連線字串**可由某些用戶端程式庫使用，且包含其他程式庫進行連接時所需的一切資訊。

- **指令行**是一個預先格式化的指令，它會使用正確的參數來呼叫 `mysql`。

您將在 {{site.data.keyword.composeForPostgreSQL}} 服務的*概觀* 頁面上找到這兩者。

連接至 MySQL for Compose 部署時所需的一切資訊。
* 如何針對您的資料庫使用[連線字串](#section-the-connection-string)。
* 如何使用 [SSL](#section-ssl-and-mysql) 和[自簽憑證](#section-using-the-self-signed-certificate)。
* 如何透過[指令行](#section-connecting-from-the-command-line)或從[應用程式](#section-connecting-your-application)進行連接。

## 連線字串

連線字串是連接至 Compose for MySQL 時的第一個參照點；它幾乎包含連接至資料庫所需的一切資訊。

```
mysql://[username]:[password]@[host]:[port]/compose
```

**附註：**此手冊中的範例使用管理使用者帳戶進行連接。管理使用者是具有所有資料庫管理存取權的完整特許使用者。不過，基於安全理由，管理者帳戶只應該用來建立使用者，以及授與他們專用權，而不是連接至應用程式。

連線字串會格式化為 URI，您可以在驅動程式和應用程式瞭解標準化格式之處使用此 URI。其他應用程式可以從連線字串 URI 中擷取必要的詳細資料。

其他驅動程式會針對其連線參數使用連線 URI 的元件部分（主機名稱和埠）。主機名稱位於 `@` 符號之後，而埠號則位於 `:` 之後。

如果您未指定要連接至的資料庫，則需要 `USE my_database` 指令來選取資料庫；MySQL 連線不需要指定要連接的資料庫。

## SSL 及 MySQL

依預設，所有 Compose for MySQL 部署都已啟用 SSL；但是 MySQL 執行 SSL 的方式表示也會接受非 SSL 連線。這表示在配置應用程式的 MySQL 驅動程式時，您需要確保它會建立安全的連線。藉由 MySQL 指令行，您可以將 `--ssl-mode=REQUIRED` 新增至連線指令來執行此動作。對於應用程式驅動程式，這些設定是驅動程式特有的設定。在這些範例中，我們會顯示應該一律只在 SSL 已啟用的情況下才進行連接的指令。

## 使用自簽憑證

Compose 部署提供自簽憑證，可用來驗證要與其交談的主機。

若要使用自簽憑證，請將它複製到檔案。此憑證位於 {{site.data.keyword.composeForElasticsearch}} 服務的*概觀* 頁面上。 

複製從 `-----BEGIN CERTIFICATE-----` 到 `-----END CERTIFICATE-----` 的文字，並貼至副檔名為 `.cert` 或 `.pem` 的檔案，視連線驅動程式需要哪個檔案而定。將檔案儲存到您可以存取的位置，因為稍後我們將需要憑證的路徑。

## 從指令行連接

若要直接連接及管理 Compose for MySQL 部署，您可以使用指令行。若要這樣做，您必須在本端機器上安裝 MySQL。每一個平台都有自己的安裝套件，因此請選擇最適合您的安裝套件。您可以在 [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/) 上找到 Oracle 社群套件。從該處下載之前，請注意，在 Linux 上，您通常會在配送儲存庫中找到 MySQL。如果您是使用 Mac，則可以使用 Homebrew 來安裝 MySQL，這會編譯並安裝最新版本。

若要透過終端機存取部署，請複製*連線資訊* 畫面中提供的指令行字串並貼至您的終端機，以連接至您的部署。

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

若要在連接時啟用 SSL，請使用 `--ssl-mode=REQUIRED`。預設使用者的名稱為 "admin"，用來作為 `-u` 參數中的使用者名稱。執行該指令之後，系統會提示您輸入管理使用者的密碼，您可以從*連線資訊* 畫面的認證區段中取得此密碼。

依預設，Compose for MySQL 已啟用 SSL，但在連接時，您應該在指令行上使用 `--ssl-mode=REQUIRED` 選項，以採取額外的預防措施。這會阻止 MySQL 由於任何原因而回復至未加密的連線。

如果您偏好的話，可以使用自簽憑證來進行驗證。將 `--ssl-mode` 參數變更為 `--ssl-mode=VERIFY_CA`，並新增含有 .pem 檔案之路徑和名稱的 `--ssl-ca`：

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## 連接您的應用程式

您的應用程式將使用部署連線字串連接至 Compose for MySQ。此快速連線手冊涵蓋連線驅動程式，並為 JavaScript、Go、Python、Java 及 Ruby 提供程式碼範例。

## 使用 JavaScript 及 Node.js 連接

MySQL for Node.js 的先進驅動程式是 [node-mysql 驅動程式](https://github.com/mysqljs/mysql)。我們將在這裡逐步設定簡單的 Node.js/MySQL 連線。如果您想要跟進，請確定 [Node.js](https://nodejs.org/) 和 [npm](https://github.com/npm/npm) 已安裝在您的系統上。

使用 `npm init` 起始設定新專案之後，請在專案的資料夾中安裝驅動程式套件：

```shell
npm install mysql --save
```

驅動程式及其相依關係會安裝在 `node_modules` 資料夾中，而驅動程式將出現在 `package.json` 檔案的 `dependencies` 下。

您可以使用下列程式碼來連接至 MySQL。

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

**附註**
- `SHOW DATABASES` 是一個 MySQL 指令，其中列出使用者具有其專用權的資料庫。
- 部署中的所有資料庫都會顯示，因為 Script 使用_管理_ 使用者。
- 查詢的結果會以物件陣列傳回。

## 使用 Go 連接

Go 具有 [SQL Database 的一般介面](https://golang.org/pkg/database/sql/)，因此，使用此介面與 [go-sql-driver](https://github.com/go-sql-driver/mysql) 搭配，將提供數個選項來連接至 MySQL。驅動程式的問題是我們無法驗證自簽憑證。使用自簽憑證的唯一 TLS/SSL 選項為 `skip-verify`，但這不是最佳選項。

若要使用 Go 連接至 MySQL，請先將 _go-sql-driver_ 套件安裝到 `$GOPATH`：

```shell
go get github.com/go-sql-driver/mysql
```

您可以使用下列程式碼來連接至 MySQL。

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

## 使用 Python 連接

您可以利用 Python 連接至 MySQL，方法為使用 [MySQL 的官方 Python 連接器](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html)。

首先，安裝[連接器套件](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html)。安裝套件之後，您可以使用下列程式碼來連接至我們的資料庫：
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

附註：
- 範例會匯入 MySQL 連接器，並在 `config` 字典內新增任何連線參數。安全連線是使用連線字典中的部署自簽憑證來起始設定。
- `ssl_verify_cert` 需要 `ssl_ca` 選項。使用配置選項 `'ssl_verify_cert': True`，可確保伺服器的憑證與 `cert.pem` 中儲存的憑證相同。如果發生憑證錯誤，則會傳回 `ValueError`，指出憑證不符。
- 可在[這裡](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)找到可用連線引數的有用清單。
- MySQL Python 連接器需要實例化 `cursor` 物件，才能執行 SQL 查詢。在此程式碼範例中，此處之連線物件的 `cursor` 方法會獲指派變數 `cur`，而且變數 `query` 會指派給 SQL 指令，以告知 MySQL 顯示所有部署的資料庫。
- `execute` 方法會執行透過安全連線將 Python 物件轉換為 MySQL 指令的資料庫作業。在此範例中，執行方法會告知 MySQL 顯示所有資料庫，先反覆運算它們，然後再將輸出記載至主控台並關閉連線。

## 使用 Java 連接

若要使用 Java 連接，請先下載並安裝 MySQL 的 [Connector/J JDBC 驅動程式](https://dev.mysql.com/downloads/connector/j/)。

然後，您可以使用下列程式碼來連接至部署：

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
附註
- 設定連線的基本資訊在連線字串內。我們會使用該資訊與 JDBC API 搭配，並將該字串儲存在變數 `URL` 中：
- 部署的使用者名稱和密碼儲存在不同變數中，其用來建立與 JDBC `DriverManager.getConnection()` 方法的連線。
- 連線字串包括主機名稱、埠及資料庫；SSL 選項會附加至連線字串。
- 範例會建立 SSL 連線，這會使用自簽憑證進行驗證。您可以在不使用這些選項的情況下連接至伺服器，但連線將會不安全，因此導致 MySQL 發出警告：
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- 為了讓驅動程式處理憑證，認證會儲存在一個稱為 `cert.pem` 的檔案中。無法直接使用此憑證。請改為建立信任儲存庫，以使用 `keytool` 來保留憑證的認證。下列指令會匯入 `cert.pem` 檔案、將別名 `composeCert` 指派給它，並將輸出檔定義為稱為 `truststore` 的金鑰儲存庫。它使用密碼 `henrythedog` 來解除鎖定金鑰儲存庫。
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- `javax.net.ssl.trustStore` 及 `javax.net.ssl.trustStorePassword` 上的 `setProperty` 方法會使用金鑰儲存庫中的資訊。系統內容應該設定在程式頂端，以便在運行環境中提早執行；最好是在設定 `Connection` 變數之前，先將它們鎖定，再啟動 SSL 連線。
- 建立連線之後，會傳回 Statement 物件，並對該物件執行查詢。這會傳回 ResultSet，用來反覆運算及列印資料庫名稱。

## 使用 Ruby 連接

Ruby 有許多 MySQL 驅動程式。範例連線程式碼使用 [MySQL2](https://github.com/brianmario/mysql2)。

您可以根據驅動程式的 Github 儲存庫中的指示來安裝 MySQL2，並使用下列程式碼來連接至 MySQL：
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
附註
- `config` 雜湊包含所有連線配置，其中包括設定 SSL 連線。如需所有配置選項的詳細資料，請參閱 [MySQL2 Readme](https://github.com/brianmario/mysql2)。
- 若要使用自簽憑證設定安全連線，請設定 `sslCA` 和 `sslverify`。`sslCA` 是包含憑證之 `.pem` 或 `.cert` 檔案的路徑，而 `sslverify` 會設為 `true`，以便檢查是否有有效憑證。
-  `Mysql2::Client.new` 建構子會使用 `config` 中的連線配置，起始設定新的連線變數。
- `results` 包含雜湊陣列，而這些雜湊會反覆運算並列印至主控台。
