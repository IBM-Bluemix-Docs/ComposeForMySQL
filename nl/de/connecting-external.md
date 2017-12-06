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

# Externe Anwendung verbinden
{: #connecting-external-app}

Es gibt zwei Möglichkeiten, eine externe Anwendung mit {{site.data.keyword.composeForMySQL_full}} zu verbinden:

- Eine **Verbindungszeichenfolge** kann von bestimmten Clientbibliotheken verwendet werden und enthält alle Informationen, die andere Bibliotheken zum Herstellen einer Verbindung benötigen.

- Die **Befehlszeile** ist ein vorformatierter Befehl, der `mysql` mit den korrekten Parametern aufruft. 

Beides finden Sie auf der Seite *Übersicht* Ihres {{site.data.keyword.composeForPostgreSQL}}-Service.

Alle Informationen, die Sie zum Herstellen einer Verbindung zu einer MySQL for Compose-Bereitstellung brauchen.
* Vorgehensweise zur Verwendung der [Verbindungszeichenfolgen](#section-the-connection-string) für Ihre Datenbanken.
* Vorgehensweise zur Verwendung von [SSL](#section-ssl-and-mysql) und des [selbst signierten Zertifikats](#section-using-the-self-signed-certificate).
* Vorgehensweise zum Herstellen einer Verbindung über die [Befehlszeile](#section-connecting-from-the-command-line) oder über Ihre [Anwendungen](#section-connecting-your-application).

## Verbindungszeichenfolge

Die Verbindungszeichenfolge ist Ihr erster Bezugspunkt, wenn Sie eine Verbindung zu Compose for MySQL herstellen. Sie enthält fast alle Informationen, die Sie zum Herstellen einer Verbindung zu einer Datenbank brauchen.

```
mysql://[username]:[password]@[host]:[port]/compose
```

**Hinweis:** In den Beispielen im vorliegenden Handbuch wird eine Verbindung mit dem Konto des Benutzers mit Verwaltungsaufgaben hergestellt. Der Benutzer mit Verwaltungsaufgaben ist ein vollständig privilegierter Benutzer, der Verwaltungszugriff auf alle Ihre Datenbanken besitzt. Aus Sicherheitsgründen sollte dieses Konto jedoch nur dazu verwendet werden, Benutzer zu erstellen und ihnen Berechtigungen zu erteilen, nicht zum Herstellen von Verbindungen mit Anwendungen.

Die Verbindungszeichenfolge ist als URI formatiert, der verwendet werden kann, wenn Treiber und Anwendungen das Standardformat verstehen. Andere Anwendungen können die wichtigen Details aus dem Verbindungszeichenfolgen-URI extrahieren.

Andere Treiber verwenden einzelne Komponenten des Verbindungs-URI – den Hostnamen und den Port – für Ihre Verbindungsparameter. Sie finden den Hostnamen nach dem Symbol `@` und die Portnummer nach dem Symbol `:`.

Wenn Sie eine Datenbank für die Verbindung bestimmen, müssen Sie mit dem Befehl `USE my_database` eine Datenbank auswählen. Bei einer MySQL-Verbindung muss keine zu verbindende Datenbank angegeben werden.

## SSL und MySQL

Bei allen Compose for MySQL-Bereitstellungen ist standardmäßig SSL aktiviert. Allerdings wird SSL von MySQL so ausgeführt, dass auch Nicht-SSL-Verbindungen akzeptiert werden. Sie müssen also beim Konfigurieren des MySQL-Treibers Ihrer Anwendung sicherstellen, dass MySQL eine sichere Verbindung erstellt. In der MySQL-Befehlszeile können Sie dazu `--ssl-mode=REQUIRED` zum Verbindungsbefehl hinzufügen. Bei Anwendungstreibern sind die Einstellungen treiberspezifisch. In den Beispielen werden Befehle gezeigt, mit deren Hilfe immer und ausschließlich bei aktiviertem SSL eine Verbindung hergestellt werden kann.

## Selbst signierte Zertifikate verwenden

Compose-Bereitstellungen stellen ein selbst signiertes Zertifikat bereit, mit dem Sie den Host validieren können, mit dem kommuniziert wird.

Kopieren Sie das selbst signierte Zertifikat in eine Datei, um es verwenden zu können. Sie finden das Zertifikat auf der Seite *Übersicht* Ihres {{site.data.keyword.composeForElasticsearch}}-Service. 

Kopieren Sie den Text von `-----BEGIN CERTIFICATE-----` bis `-----END CERTIFICATE-----` und fügen Sie ihn in eine Datei mit der Erweiterung `.cert` oder `.pem` ein, je nachdem, was der Verbindungstreiber benötigt. Speichern Sie die Datei an einer Position, auf die Sie zugreifen können, weil Sie den Zertifikatspfad später benötigen.

## Verbindung über die Befehlszeile herstellen

Sie können über die Befehlszeile eine Direktverbindung zu Ihrer Compose for MySQL-Bereitstellung herstellen und diese verwalten. Dazu müssen Sie MySQL auf Ihrer lokalen Maschine installieren. Jede Plattform hat eigene Installationspakete. Wählen Sie daher das Paket aus, das sich am besten für Ihre Zwecke eignet. Die Oracle-Community-Pakete finden Sie unter [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/). Bevor Sie das Paket von dort herunterladen, müssen Sie beachten, dass Sie MySQL unter Linux normalerweise in Ihrem Verteilerrepository finden. Wenn Sie einen Mac verwenden, können Sie MySQL mit Homebrew installieren, wodurch die neueste Version kompiliert und installiert wird.

Für den Zugriff auf Ihre Bereitstellung über das Terminal müssen Sie die in der Anzeige *Verbindungsinformationen* bereitgestellte Befehlszeilenzeichenfolge kopieren und in Ihr Terminal einfügen, um eine Verbindung zu Ihrer Bereitstellung herzustellen.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

Verwenden Sie `--ssl-mode=REQUIRED`, um beim Herstellen einer Verbindung SSL zu aktivieren. Der Standardbenutzer heißt "admin" und wird von Ihnen im Parameter `-u` als Benutzername verwendet. Nach der Ausführung des Befehls werden Sie aufgefordert, das Kennwort des Benutzers mit Verwaltungsaufgaben einzugeben, das Sie in der Anzeige *Verbindungsinformationen* im Bereich mit den Berechtigungsnachweisen finden.

Compose for MySQL hat SSL standardmäßig aktiviert. Dennoch sollten Sie beim Verbinden als zusätzliche Vorsichtsmaßnahme die Option `--ssl-mode=REQUIRED` in der Befehlszeile verwenden. Dies verhindert, dass MySQL aus irgendeinem Grund auf eine unverschlüsselte Verbindung zurückgesetzt wird.

Sie können für die Überprüfung das selbst signierte Zertifikat verwenden, wenn Ihnen das lieber ist. Ändern Sie den Parameter `--ssl-mode` in `--ssl-mode=VERIFY_CA` und fügen Sie `--ssl-ca` mit dem Pfad und dem Namen Ihrer .pem-Datei hinzu:

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## Verbindung mit Ihrer Anwendung herstellen

Ihre Anwendung stellt über die Verbindungszeichenfolge Ihrer Bereitstellung eine Verbindung zu Compose for MySQL her. Im vorliegenden Handbuch für Schnellverbindung werden die Verbindungstreiber beschrieben und Codebeispiele für JavaScript, Go, Python, Java und Ruby gegeben.

## Verbindung mit JavaScript und Node.js herstellen

Der wichtigste Treiber für MySQL for Node.js ist der [node-mysql-Treiber](https://github.com/mysqljs/mysql). Nachstehend werden Sie durch die Einrichtung einer einfachen Node.js/MySQL-Verbindung geführt. Wenn Sie das auf Ihrem System nachvollziehen wollen, müssen Sie sicherstellen, dass [Node.js](https://nodejs.org/) und [npm](https://github.com/npm/npm) installiert sind.

Installieren Sie nach der Initialisierung eines neuen Projekts mit `npm init` das Treiberpaket im Projektordner:

```shell
npm install mysql --save
```

Der Treiber und seine Abhängigkeiten werden im Ordner `node_modules` installiert und der Treiber wird unter `dependencies` in der Datei `package.json` angezeigt.

Sie können die Verbindung zu MySQL mit dem folgenden Code herstellen:

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

**Hinweise:**
- `SHOW DATABASES` ist ein MySQL-Befehl, mit dem die Datenbanken aufgelistet werden, für die ein Benutzer Berechtigungen besitzt.
- Es werden alle Datenbanken in der Bereitstellung angezeigt, weil das Script den Benutzer _admin_ verwendet.
- Die Ergebnisse der Abfrage werden als Array von Objekten zurückgegeben.

## Verbindung mit Go herstellen

Go besitzt eine [generische Schnittstelle für SQL-Datenbanken](https://golang.org/pkg/database/sql/). Ihre Verwendung mit dem [go-sql-Treiber](https://github.com/go-sql-driver/mysql) stellt mehrere Optionen zum Herstellen einer Verbindung mit MySQL bereit. Das Problem bei dem Treiber ist, dass Sie das selbst signierte Zertifikat nicht überprüfen können. Die einzige TLS/SSL-Option, die Sie bei selbst signierten Zertifikaten haben, ist `skip-verify`, was suboptimal ist.

Installieren Sie zum Verbinden von MySQL mithilfe von Go zuerst das Paket _go-sql-driver_ in Ihrem Pfad `$GOPATH`:

```shell
go get github.com/go-sql-driver/mysql
```

Sie können die Verbindung zu MySQL mit dem folgenden Code herstellen:

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

## Verbindung mit Python herstellen

Sie können die Verbindung zu MySQL mit Python über den [offiziellen Python-Connector von MySQL](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html) herstellen.

Installieren Sie zuerst das [Connectorpaket](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html). Nach der Installation des Pakets können Sie mit dem folgenden Code eine Verbindung zu Ihrer Datenbank herstellen:
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

Hinweise:
- Im Beispiel wird der MySQL-Connector importiert. Außerdem werden die Verbindungsparameter in einem Wörterverzeichnis namens `config` hinzugefügt. Im Wörterverzeichnis der Verbindung wird mithilfe des selbst signierten Zertifikats der Bereitstellung eine sichere Verbindung initialisiert.
- Für `ssl_verify_cert` ist die Option `ssl_ca` erforderlich. Mit der Verwendung der Option `'ssl_verify_cert': True` wird sichergestellt, dass das Serverzertifikat mit dem in `cert.pem` gespeicherten Zertifikat identisch ist. Bei einem Zertifikatsfehler wird `ValueError` zurückgegeben. Diese Nachricht zeigt an, dass die Zertifikate nicht übereinstimmen.
- Eine hilfreiche Liste der verfügbaren Verbindungsargumente finden Sie [hier](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html).
- Für den Python-Connector von MySQL muss ein `cursor`-Objekt instanziiert werden, damit SQL-Abfragen ausgeführt werden können. Im vorliegenden Codebeispiel wird der Methode `cursor` des hier verwendeten Verbindungsobjekts die Variable `cur` zugewiesen und die Variable `query` wird dem SQL-Befehl zugewiesen. Damit wird MySQL angewiesen, alle Datenbanken der Bereitstellung anzuzeigen.
- Die Methode `execute` führt Datenbankoperationen aus, die Python-Objekte über eine sichere Verbindung in MySQL-Befehle umwandeln. Im vorliegenden Beispiel weist die Ausführungsmethode MySQL an, alle Datenbanken anzuzeigen, sie zu iterieren, bevor die Ausgabe in der Konsole protokolliert wird, und die Verbindung zu schließen.

## Verbindung mit Java herstellen

Zum Herstellen einer Verbindung mit Java müssen Sie zuerst den [Connector/J-JDBC-Treiber](https://dev.mysql.com/downloads/connector/j/) von MySQL herunterladen und installieren.

Dann können Sie mit dem folgenden Code eine Verbindung zu einer Bereitstellung herstellen:

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
Hinweise:
- Die Basisinformationen zum Einrichten einer Verbindung befinden sich in der Verbindungszeichenfolge. Diese wird mit der JDBC-API verwendet und in der Variablen `URL` gespeichert:
- Der Benutzername und das Kennwort für die Bereitstellung werden in separaten Variablen gespeichert, die zum Herstellen einer Verbindung mit der JDBC-Methode `DriverManager.getConnection()` verwendet werden.
- Die Verbindungszeichenfolge umfasst den Hostnamen, den Port und die Datenbank. Die SSL-Optionen werden an die Verbindungszeichenfolge angehängt.
- Im Beispiel wird eine SSL-Verbindung erstellt, die mit dem selbst signierten Zertifikat überprüft wird. Sie können die Verbindung zum Server zwar ohne Optionen herstellen, doch eine solche Verbindung wäre unsicher und würde die folgende Warnung von MySQL auslösen:
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- Damit der Treiber das Zertifikat verarbeiten kann, werden die Berechtigungsnachweise in einer Datei namens `cert.pem` gespeichert. Das Zertifikat kann nicht direkt verwendet werden. Erstellen Sie stattdessen mit `keytool` einen Truststore, in dem die Berechtigungsnachweise des Zertifikats enthalten sein sollen. Mit dem folgenden Befehl wird die Datei `cert.pem` importiert, ihr wird der Aliasname `composeCert` zugewiesen und die Ausgabedatei wird als Schlüsselspeicher mit dem Namen `truststore` definiert. Zum Entsperren des Schlüsselspeichers wird das Kennwort `henrythedog` verwendet.
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- Die Methode `setProperty` für `javax.net.ssl.trustStore` und `javax.net.ssl.trustStorePassword` verwendet die Informationen aus dem Schlüsselspeicher. Die Systemeigenschaften sollten im oberen Bereich des Programms festgelegt werden, damit sie zu Beginn der Laufzeit ausgeführt werden, möglichst bevor die Variable `Connection` festgelegt wird, damit sie vor dem Start einer SSL-Verbindung gesperrt werden.
- Nach der Erstellung der Verbindung wird ein Objekt namens 'Statement' zurückgegeben und die Abfrage wird für das Objekt ausgeführt. Damit wird ein Objekt namens 'ResultSet' zurückgegeben, das die Datenbanknamen durchläuft und druckt.

## Verbindung mit Ruby herstellen

Es gibt eine Reihe von MySQL-Treibern für Ruby. Im Beispielverbindungscode wird [MySQL2](https://github.com/brianmario/mysql2) verwendet.

Sie können eine Verbindung zu MySQL erstellen, indem Sie MySQL2 entsprechend den Anweisungen im Github-Repository des Treibers installieren und den folgenden Code verwenden:
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
Hinweise:
- Der Hashwert `config` enthält die gesamte Verbindungskonfiguration, einschließlich der Einrichtung einer SSL-Verbindung. Weitere Informationen zu allen Konfigurationsoptionen finden Sie in der [MySQL2-Readme-Datei](https://github.com/brianmario/mysql2).
- Zum Einrichten einer sicheren Verbindung mit dem selbst signierten Zertifikat werden `sslCA` und `sslverify` festgelegt. `sslCA` ist der Pfad der `.pem`- oder `.cert`-Datei, die das Zertifikat enthält, und `sslverify` wird auf `true` festgelegt, um zu prüfen, ob ein Zertifikat gültig ist.
-  Der Konstruktor `Mysql2::Client.new` initialisiert eine neue Verbindungsvariable mithilfe der Verbindungskonfiguration in `config`.
- `results` enthält ein Array von Hashwerten, die durchlaufen und in die Konsole ausgegeben werden.
