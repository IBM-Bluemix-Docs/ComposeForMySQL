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

# 外部アプリケーションの接続
{: #connecting-external-app}

{{site.data.keyword.composeForMySQL_full}} に外部アプリケーションを接続するには、2 つの方法があります。

- 一部のクライアント・ライブラリーでは**接続ストリング**を使用できます。接続ストリングに、他のライブラリーからの接続に必要な情報をすべて組み込みます。

- **コマンド・ライン**は、形式の決まっているコマンドです。正しいパラメーターを指定して `mysql` を呼び出します。

両方の方法が {{site.data.keyword.composeForPostgreSQL}} サービスの*「概要」*ページにあります。

MySQL for Compose のデプロイメントに接続するために必要なすべての情報
* データベースの[接続ストリング](#section-the-connection-string)の使用方法
* [SSL](#section-ssl-and-mysql) と[自己署名証明書](#section-using-the-self-signed-certificate)の使用方法
* [コマンド・ライン](#section-connecting-from-the-command-line)による接続方法や[アプリケーション](#section-connecting-your-application)からの接続方法

## 接続ストリング

接続ストリングは、Compose for MySQL に接続するための最初の参照ポイントになります。データベース接続に必要なほぼすべての情報を接続ストリングに組み込みます。

```
mysql://[username]:[password]@[host]:[port]/compose
```

**注:** このガイドのサンプルでは、接続に admin ユーザー・アカウントを使用します。admin ユーザーは、全特権を持ったユーザーであり、すべてのデータベースへの管理アクセスが可能です。ただし、セキュリティー上の理由から、admin アカウントは、ユーザーの作成と特権の付与という用途に限定し、アプリケーションへの接続には使用しないほうが望ましいと言えます。

接続ストリングは URI の形式になっており、ドライバーやアプリケーションが URI の標準形式を理解できる環境で使用できます。その他のアプリケーションは、接続ストリングの URI から重要な詳細情報を抽出できます。

その他のドライバーは、接続 URI の構成要素 (ホスト名とポート) を接続パラメーターとして使用します。ホスト名は `@` 記号の後、ポート番号は `:` の後にあります。

接続先のデータベースを指定しない場合は、`USE my_database` コマンドでデータベースを選択する必要があります。MySQL 接続では、接続先のデータベースを指定しなくてもかまいません。

## SSL と MySQL

Compose for MySQL のすべてのデプロイメントでは、デフォルトで SSL が有効になりますが、MySQL では SSL 以外の接続も可能です。したがって、アプリケーションの MySQL ドライバーの構成時に、必ずセキュア接続を作成するようにしなければなりません。MySQL のコマンド・ラインでは、そのために `--ssl-mode=REQUIRED` を接続コマンドに追加してください。アプリケーション・ドライバーの場合は、ドライバーごとに固有の設定があります。ここで取り上げるサンプルでは、どんな場合でも SSL を有効にした接続コマンドを示します。

## 自己署名証明書の使用

Compose のデプロイメントには自己署名証明書が用意されており、通信先のホストの検証のために、その証明書を使用できます。

自己署名証明書を使用するには、まずその証明書をファイルにコピーします。その証明書は、{{site.data.keyword.composeForElasticsearch}} サービスの*「概要」*ページにあります。 

`-----BEGIN CERTIFICATE-----` から `-----END CERTIFICATE-----` までのテキストをコピーしてファイルに貼り付けてください。拡張子は、接続ドライバーの要件に応じて `.cert` か `.pem` にします。アクセス可能な場所にそのファイルを保存してください。証明書のパスが後で必要になります。

## コマンド・ラインからの接続

Compose for MySQL のデプロイメントに直接接続して管理タスクを実行するために、コマンド・ラインを使用できます。そのためには、ローカル・マシンに MySQL をインストールしておく必要があります。プラットフォームごとにインストール・パッケージがあるので、一番適しているパッケージを選択してください。Oracle コミュニティー・パッケージは、[http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/) にあります。そのサイトからダウンロードする前に、Linux では通常、ディストリビューション・リポジトリーに MySQL が入っているので、その点を確認してください。Mac を使用している場合は、Homebrew で MySQL をインストールできます。そうすると、最新バージョンがコンパイルされ、インストールされます。

端末からデプロイメントにアクセスする場合は、*「接続情報」*パネルに表示されるコマンド・ライン・ストリングをコピーして端末に貼り付けることによって、デプロイメントに接続できます。

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

接続時に SSL を有効にするために、`--ssl-mode=REQUIRED` を使用します。デフォルトのユーザー名は admin です。`-u` パラメーターでそのユーザー名を使用してください。このコマンドを実行すると、admin ユーザーのパスワードを入力するためのプロンプトが表示されます。パスワードは、*「接続情報」*パネルの資格情報セクションで確認できます。

Compose for MySQL では、デフォルトで SSL が有効になりますが、接続時にコマンド・ラインで `--ssl-mode=REQUIRED` オプションを使用することによって、追加の予防策を講じてください。そうすれば、MySQL が何かの理由で、暗号化されていない接続を使用する事態を防止できます。

検証のために自己署名証明書を使用することもできます。その場合は、`--ssl-mode` パラメーターを `--ssl-mode=VERIFY_CA` に変更し、`--ssl-ca` に .pem ファイルのパスと名前を追加します。

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## アプリケーションの接続

アプリケーションは、デプロイメントの接続ストリングを使用して Compose for MySQL に接続します。このクイック・ガイドでは、JavaScript、Go、Python、Java、Ruby に対応した接続ドライバーとコード・サンプルを取り上げます。

## JavaScript と Node.js による接続

MySQL for Node.js に対応した優れたドライバーとして、[node-mysql driver](https://github.com/mysqljs/mysql)があります。ここでは、シンプルな Node.js/MySQL 接続をセットアップします。この作業を実行する場合は、[Node.js](https://nodejs.org/) と [npm](https://github.com/npm/npm) をシステムにインストールしておく必要があります。

`npm init` を使用して新しいプロジェクトを初期化したら、ドライバー・パッケージをプロジェクトのフォルダーにインストールします。

```shell
npm install mysql --save
```

ドライバーとドライバーの実行に必要な従属項目が `node_modules` フォルダーにインストールされ、`package.json` ファイルの `dependencies` にそのドライバーが書き込まれます。

以下のコードで MySQL に接続できます。

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

**注**
- `SHOW DATABASES` は、ユーザーが特権を持っているデータベースのリストを出力する MySQL コマンドです。
- このスクリプトでは _admin_ ユーザーを使用しているので、デプロイメントに含まれているすべてのデータベースが表示されます。
- 照会結果は、オブジェクトの配列として返されます。

## Go による接続

Go には、[SQL データベースに対応した汎用インターフェース](https://golang.org/pkg/database/sql/)があり、そのインターフェースと [go-sql-driver](https://github.com/go-sql-driver/mysql) を使用する場合は、MySQL に接続するためのオプションをいくつか選択できます。そのドライバーの問題点は、自己署名証明書を検証できないということです。自己署名証明書に関する TLS/SSL オプションは `skip-verify` しかなく、とても最適なオプションとは言えません。

Go を使用して MySQL に接続するには、まず _go-sql-driver_ パッケージを `$GOPATH` にインストールします。

```shell
go get github.com/go-sql-driver/mysql
```

以下のコードで MySQL に接続できます。

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

## Python による接続

Python で MySQL に接続する場合は、[MySQL の公式 Python コネクター](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html)を使用できます。

まず、[コネクター・パッケージ](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html)をインストールします。パッケージをインストールしたら、以下のコードでデータベースに接続できます。
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

注:
- このサンプルでは、MySQL コネクターをインポートし、`config` 辞書に接続パラメーターを追加します。接続辞書で指定するデプロイメントの自己署名証明書を使用してセキュア接続を初期化します。
- `ssl_verify_cert` を指定する場合は、`ssl_ca` オプションが必要です。`'ssl_verify_cert': True` 構成オプションを使用する場合は、サーバーの証明書と `cert.pem` に保管されている証明書が同じであることを確認してください。証明書にエラーがある場合は、証明書が一致しないという趣旨の `ValueError` が返されます。
- 使用可能な接続引数をまとめた便利なリストが[ここ](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html)にあります。
- MySQL Python コネクターの場合は、SQL 照会を実行するために `cursor` オブジェクトをインスタンス化する必要があります。このコード・サンプルでは、接続オブジェクトの `cursor` メソッドに `cur` という変数、SQL コマンドに `query` という変数を割り当てることによって、デプロイメントのすべてのデータベースを MySQL で表示するようにしています。
- `execute` メソッドによって、セキュア接続で Python オブジェクトを MySQL コマンドに変換するデータベース操作を実行します。このサンプルでは、実行メソッドに基づいて MySQL がすべてのデータベースを反復処理で表示し、出力をコンソールのログに書き出して接続を閉じます。

## Java による接続

Java で接続する場合は、まず MySQL の [Connector/J JDBC ドライバー](https://dev.mysql.com/downloads/connector/j/)をダウンロードしてインストールします。

以下のコードでデプロイメントに接続できます。

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
注
- 接続をセットアップするための基本情報は、接続ストリングの中にあります。ここでは、JDBC API でその情報を使用し、そのストリングを `URL` 変数に格納します。
- デプロイメントのユーザー名とパスワードを別の変数に格納し、JDBC の `DriverManager.getConnection()` メソッドで接続を確立する時に使用します。
- 接続ストリングには、ホスト名、ポート、データベースが含まれており、SSL オプションが接続ストリングの最後に追加されています。
- このサンプルでは、SSL 接続を確立し、自己署名証明書による検証を実行します。そのようなオプションを使用しなくてもサーバーに接続することは可能ですが、その場合は接続がセキュアでなくなり、MySQL から警告が出されます。
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- ドライバーが証明書を処理できるように、資格情報を `cert.pem` というファイルに保存します。証明書を直接使用することはできません。`keytool` を使用して、証明書の資格情報を格納するトラストストアを作成する必要があります。以下に示すのは、`cert.pem` ファイルをインポートし、そのファイルに `composeCert` という別名を割り当てて、出力ファイルを `truststore` という鍵ストアとして定義するためのコマンドです。また、鍵ストアのロックを解除するために `henrythedog` というパスワードを使用します。
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- `javax.net.ssl.trustStore` と `javax.net.ssl.trustStorePassword` の `setProperty` メソッドでは、鍵ストアから取得した情報を使用します。システム・プロパティーは、実行時の初期の段階で処理できるように、プログラムの先頭付近で設定してください。可能なら、`Connection` 変数を設定する前にそうします。そうすれば、 SSL 接続の開始前にそうしたプロパティーをロックした状態で設定できます。
- 接続を作成したら、Statement オブジェクトが返されるので、そのオブジェクトに対して照会を実行します。その結果、データベース名を反復処理で出力する ResultSet が返されます。

## Ruby による接続

Ruby に対応した MySQL ドライバーはいくつもあります。サンプルの接続コードでは、[MySQL2](https://github.com/brianmario/mysql2) を使用しています。

MySQL2 をインストールして MySQL に接続できます。そのドライバーの Github リポジトリーにある手順に基づいて、以下のコードを使用してください。
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
注
- `config` ハッシュに、すべての接続構成を組み込み、SSL 接続のセットアップ情報も含めます。すべての構成オプションの詳細については、[MySQL2 README](https://github.com/brianmario/mysql2) を参照してください。
- 自己署名証明書を使用してセキュア接続をセットアップするために、`sslCA` と `sslverify` を設定します。`sslCA` は、証明書を組み込んだ `.pem` ファイルか `.cert` ファイルのパスです。`sslverify` は、有効な証明書かどうかの確認を行うために `true` に設定します。
-  `Mysql2::Client.new` コンストラクターによって、`config` の接続構成に基づいて新しい接続変数を初期化します。
- `results` にハッシュの配列を組み込み、反復処理で結果を生成してコンソールに出力します。
