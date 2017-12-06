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

# 외부 애플리케이션 연결
{: #connecting-external-app}

외부 애플리케이션을 {{site.data.keyword.composeForMySQL_full}}에 연결하는 두 가지 방법이 있습니다.

- **연결 문자열**은 일부 클라이언트 라이브러리에서 사용될 수 있으며 다른 라이브러리가 연결하는 데 필요한 모든 정보를 포함합니다. 

- **명령행**은 올바른 매개변수와 함께 `mysql`을 호출하는 사전 형식화된 명령입니다.

둘 다 {{site.data.keyword.composeForPostgreSQL}} 서비스의 *개요* 페이지에서 찾을 수 있습니다.

MySQL for Compose 배치에 연결하는 데 필요한 모든 정보입니다.
* 데이터베이스에 대한 [연결 문자열](#section-the-connection-string)을 사용하는 방법
* [SSL](#section-ssl-and-mysql) 및 [자체 서명된 인증서](#section-using-the-self-signed-certificate)를 사용하는 방법
* [명령행](#section-connecting-from-the-command-line)을 통하거나 [애플리케이션](#section-connecting-your-application)에서 연결하는 방법

## 연결 문자열

연결 문자열은 Compose for MySQL에 연결할 때 첫 번째 참조 지점이며 데이터베이스에 연결하는 데 필요한 거의 모든 정보를 포함합니다.

```
mysql://[username]:[password]@[host]:[port]/compose
```

**참고:** 이 안내서의 예제에서는 관리자 계정을 사용하여 연결합니다. 관리자는 모든 데이터베이스에 대한 관리 액세스 권한이 있는 전체 권한이 부여된 사용자입니다. 그러나 보안을 이유로 admin 계정은 애플리케이션에 연결하는 데 사용되지 않고 사용자를 작성하여 권한을 부여하는 데만 사용되어야 합니다.

연결 문자열은 드라이버 및 애플리케이션이 표준화된 형식을 이해하는 경우에 사용될 수 있는 URI로 형식화됩니다. 기타 애플리케이션이 연결 문자열 URI에서 필수 세부사항을 추출할 수 있습니다.

기타 드라이버는 해당 연결 매개변수에 대한 연결 URI의 컴포넌트 파트(호스트 이름 및 포트)를 사용합니다. 호스트 이름은 `@` 기호 다음에 있고 포트 번호는 `:` 다음에 있습니다.

연결할 데이터베이스를 지정하지 않는 경우 데이터베이스를 선택하기 위한 `USE my_database` 명령이 필요합니다. MySQL 연결은 연결할 데이터베이스를 지정할 필요가 없습니다.

## SSL 및 MySQL

기본적으로 모든 Compose for MySQL 배치에서는 SSL이 사용 가능합니다. 그러나 MySQL이 SSL을 수행하는 방법은 비SSL 연결도 허용하지 않음을 의미합니다. 즉, 애플리케이션의 MySQL을 구성할 때 보안 연결을 작성하는지 확인해야 합니다. MySQL 명령행을 사용하면 `--ssl-mode=REQUIRED`를 연결 명령에 추가하여 이를 수행할 수 있습니다. 애플리케이션 드라이버의 경우 설정은 드라이버에 따라 다릅니다. 이 예제에서는 항상 SSL이 사용 가능한 상태로만 연결해야 하는 명령을 표시합니다.

## 자체 서명된 인증서 사용

Compose 배치는 통신 중인 호스트의 유효성을 검증하는 데 사용될 수 있는 자체 서명된 인증서를 제공합니다.

자체 서명된 인증서를 사용하려면 해당 인증서를 파일에 복사하십시오. 인증서는 {{site.data.keyword.composeForElasticsearch}} 서비스의 *개요* 페이지에 있습니다. 

`-----BEGIN CERTIFICATE-----`부터 `-----END CERTIFICATE-----`까지의 텍스트를 복사하여 파일에 붙여넣으십시오. 파일의 확장자는 필요한 연결 드라이버에 따라 `.cert` 또는 `.pem`입니다. 나중에 인증서의 경로가 필요하기 때문에 액세스할 수 있는 위치에 파일을 저장하십시오.

## 명령행에서 연결

명령행을 사용하여 Compose for MySQL 배치에 직접 연결하여 관리할 수 있습니다. 이를 수행하려면 로컬 시스템에 MySQL을 설치해야 합니다. 각 플랫폼에는 고유한 설치 패키지가 있으므로 가장 적합한 설치 패키지를 선택하십시오. [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/)에서 Oracle 커뮤니티 패키지를 찾을 수 있습니다. 그 위치에서 다운로드하기 전에 Linux에서는 일반적으로 배포 저장소에서 MySQL을 찾을 수 있다는 점에 유의하십시오. Mac을 사용 중인 경우 최신 버전을 컴파일하고 설치하는 Homebrew로 MySQL을 설치할 수 있습니다.

터미널을 통해 배치에 액세스하려면 *연결 정보* 패널에서 제공되는 명령행 문자열을 복사하여 배치에 연결할 터미널에 붙여넣으십시오.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

연결할 때 SSL을 사용으로 설정하려면 `--ssl-mode=REQUIRED`를 사용하십시오. 기본 사용자의 이름은 `-u` 매개변수에서 사용자 이름으로 사용하는 "admin"으로 지정됩니다. 명령을 실행한 후 admin 사용자의 비밀번호를 입력하라는 프롬프트가 표시됩니다. 비밀번호는 *연결 정보* 패널의 신임 정보 섹션에서 가져올 수 있습니다.

Compose for MySQL에서는 기본으로 SSL이 사용 가능하지만 연결할 때 명령행에서 `--ssl-mode=REQUIRED` 옵션을 사용하여 추가 예방조치를 취해야 합니다. 이 옵션은 어떤 이유로든 암호화되지 않은 연결로의 MySQL 폴백을 중지합니다.

원하는 경우 자체 서명된 인증서를 사용하여 확인할 수 있습니다. `--ssl-mode` 매개변수를 `--ssl-mode=VERIFY_CA`로 변경하고 .pem 파일의 경로 및 이름과 함께 `--ssl-ca`를 추가하십시오.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## 애플리케이션 연결

애플리케이션은 배치의 연결 문자열을 사용하여 Compose for MySQL에 연결합니다. 이 빠른 연결 안내서에서는 연결 드라이버에 대해 다루고 JavaScript, Go, Python, Java 및 Ruby에 대한 코드 샘플을 제공합니다.

## JavaScript 및 Node.js를 사용하여 연결

Node.js용 MySQL의 업계 선두 드라이버는 [node-mysql 드라이버](https://github.com/mysqljs/mysql)입니다. 여기서는 단순 Node.js/MySQL 연결을 설정하는 과정을 보여줍니다. 이 과정을 따르려면 [Node.js](https://nodejs.org/) 및 [npm](https://github.com/npm/npm)이 시스템에 설치되었는지 확인하십시오.

`npm init`를 사용하여 새 프로젝트를 초기화한 후 프로젝트의 폴더에 드라이버 패키지를 설치하십시오.

```shell
npm install mysql --save
```

드라이버 및 해당 종속 항목은 `node_modules` 폴더에 설치되고 드라이버는 `package.json` 파일의 `dependencies` 아래에 표시됩니다.

다음 코드를 사용하여 MySQL에 연결할 수 있습니다.

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

**참고**
- `SHOW DATABASES`는 사용자가 권한을 가지는 데이터베이스를 나열하는 MySQL 명령입니다.
- 이 스크립트는 _admin_ 사용자를 사용하므로 배치의 모든 데이터베이스가 표시됩니다.
- 조회의 결과는 오브젝트의 배열로 리턴됩니다.

## Go를 사용하여 연결

Go에는 [SQL 데이터베이스에 대한 일반 인터페이스](https://golang.org/pkg/database/sql/)가 있으며 이를 [go-sql-driver](https://github.com/go-sql-driver/mysql)와 함께 사용하면 MySQL에 연결하기 위한 여러 옵션이 제공됩니다. 드라이버의 문제점은 자체 서명된 인증서를 확인할 수 없다는 점입니다. 자체 서명된 인증서에 대해 가지는 유일한 TLS/SSL 옵션은 최적에 미치지 못하는 `skip-verify`입니다. 

Go를 사용하여 MySQL에 연결하려면 먼저 `$GOPATH`에 _go-sql-driver_ 패키지를 설치하십시오.

```shell
go get github.com/go-sql-driver/mysql
```

다음 코드를 사용하여 MySQL에 연결할 수 있습니다.

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

## Python을 사용하여 연결

[MySQL의 공식 Python 연결](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html)을 사용하여 Python으로 MySQL에 연결할 수 있습니다.

먼저, [커넥터 패키지](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html)를 설치하십시오. 패키지를 설치한 후 다음 코드를 사용하여 데이터베이스에 연결할 수 있습니다.
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

참고:
- 이 예제에서는 MySQL 커넥터를 가져오고 `config` 사전 내에 연결 매개변수를 추가합니다. 연결 사전에 있는 배치의 자체 설명된 인증서를 사용하여 보안 연결이 초기화됩니다. 
- `ssl_verify_cert`에는 `ssl_ca` 옵션이 필요합니다. 구성 옵션 `'ssl_verify_cert': True`를 사용하여 서버의 인증서와 `cert.pem`에 저장된 인증서가 동일한지 확인합니다. 인증서 오류가 있는 경우 인증서가 일치하지 않음을 표시하는 `ValueError`가 리턴됩니다. 
- 사용 가능한 연결 인수의 유용한 목록은 [여기](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)에서 찾을 수 있습니다.
- MySQL Python 커넥터에서 SQL 조회를 실행하려면 `cursor` 오브젝트가 인스턴스화되어야 합니다. 이 코드 샘플에서는 여기 연결 오브젝트의 `cursor` 메소드가 `cur` 변수에 지정되고 MySQL에 모든 배치 데이터베이스를 표시하도록 알리는 SQL 명령에 `query` 변수가 지정됩니다.
- `execute` 메소드는 보안 연결을 통해 Python 오브젝트를 MySQL 명령으로 변환하는 데이터베이스 오퍼레이션을 실행합니다. 이 예제에서는 실행 메소드가 출력을 콘솔에 로깅하고 연결을 닫기 전에 반복하여 모든 데이터베이스를 표시하도록 MySQL에 알립니다.

## Java를 사용하여 연결

Java를 사용하여 연결하려면 먼저 MySQL의 [Connector/J JDBC 드라이버](https://dev.mysql.com/downloads/connector/j/)를 다운로드하여 설치하십시오.

그런 다음, 다음 코드를 사용하여 배치에 연결할 수 있습니다.

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
참고
- 연결을 설정하기 위한 기본 정보는 연결 문자열 내에 있습니다. 이를 JDBC API와 함께 사용하고 해당 문자열을 `URL` 변수에 저장합니다.
- 배치를 위한 사용자 이름과 비밀번호는 별도의 변수에 저장되며, JDBC `DriverManager.getConnection()` 메소드를 사용하여 연결을 설정하는 데 사용됩니다.
- 연결 문자열에는 호스트 이름, 포트 및 데이터베이스가 포함됩니다. SSL 옵션이 연결 문자열에 추가됩니다.
- 샘플이 자체 서명된 인증서를 사용하여 확인되는 SSL 연결을 설정합니다. 이러한 옵션 없이 서버에 연결할 수 있지만 연결이 보안되지 않고 MySQL에서 경고가 발생할 수 있습니다.
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- 드라이버가 인증서를 처리할 수 있도록 신임 정보가 `cert.pem`이라는 파일에 저장됩니다. 신임 정보를 직접 사용할 수 없습니다. 대신, `keytool`을 사용하여 인증서의 신임 정보를 보유할 신뢰 저장소를 작성하십시오. 다음 명령은 `cert.pem` 파일을 가져와서 별명을 `composeCert`로 지정하고 출력 파일을 `truststore`라는 키 저장소로 정의합니다. 비밀번호 `henrythedog`를 사용하여 키 저장소의 잠금을 해제합니다.
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- `javax.net.ssl.trustStore` 및 `javax.net.ssl.trustStorePassword`에 대한 `setProperty` 메소드는 키 저장소의 정보를 사용합니다. 이 시스템 특성은 런타임 시 빠르게 실행되도록 프로그램의 맨 위에 설정되어야 합니다. SSL 연결을 시작하기 전에 잠겨 있을 수 있도록 `Connection` 변수가 설정되기 전에 설정되는 것이 바람직합니다.
- 연결을 작성한 후 오브젝트 오브젝트가 리턴되고 오브젝트에 대해 조회가 실행됩니다. 이는 데이터베이스 이름을 반복하고 인쇄하는 데 사용되는 ResultSet를 리턴합니다.

## Ruby를 사용하여 연결

다수의 Ruby용 MySQL 드라이버가 있습니다. 샘플 연결 코드에서는 [MySQL2](https://github.com/brianmario/mysql2)를 사용합니다.

드라이버의 Github 저장소에 있는 지시사항에 따라 MySQL2를 설치하고 다음 코드를 사용하여 MySQL에 연결할 수 있습니다.
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
참고
- `config` 해시에는 SSL 연결 설정을 포함하여 모든 연결 구성이 포함됩니다. 모든 구성 옵션에 대한 세부사항은 [MySQL2 readme](https://github.com/brianmario/mysql2)를 참조하십시오.
- 자체 서명된 인증서를 사용하여 보안 연결을 설정하도록 `sslCA` 및 `sslverify`가 설정되었습니다. `sslCA`는 인증서를 포함하는 `.pem` 또는 `.cert` 파일의 경로이며 유효한 인증서를 확인하기 위해`sslverify`가 `true`로 설정됩니다.
-  `Mysql2::Client.new` 생성자는 `config`의 연결 구성을 사용하여 새 연결 변수를 초기화합니다.
- `results`에는 반복되고 콘솔에 인쇄되는 해시의 배열이 포함됩니다.
