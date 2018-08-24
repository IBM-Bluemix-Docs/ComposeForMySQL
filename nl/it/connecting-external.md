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

# Connessione a un'applicazione esterna
{: #connecting-external-app}

Esistono due modi per collegare un'applicazione esterna a {{site.data.keyword.composeForMySQL_full}}:

- Può essere utilizzata una **Stringa di connessione** in alcune librerie client che contiene tutte le informazioni necessarie per il collegamento di altre librerie.

- La **Riga di comando** è un comando pre-formattato che richiamerà `mysql` con i parametri corretti.

Troverai entrambe nella pagina *Overview* del tuo servizio {{site.data.keyword.composeForPostgreSQL}}.

Tutte le informazioni necessarie al collegamento una distribuzione MySQL per Compose.
* Come utilizzare le [stringhe di connessione](#section-the-connection-string) per i tuoi database.
* Come utilizzare [SSL](#section-ssl-and-mysql) e il  [certificato autofirmato](#section-using-the-self-signed-certificate).
* Come collegarti tramite la [riga di comando](#section-connecting-from-the-command-line) o dalle tue [applicazioni](#section-connecting-your-application).

## La stringa di connessione

La stringa di connessione è il tuo primo punto di riferimento durante la connessione a Compose for MySQL; contiene quasi tutte le informazioni necessarie per il collegamento a un database.

```
mysql://[username]:[password]@[host]:[port]/compose
```

**Nota:** gli esempi in questa guida si collegano con l'account utente amministratore. L'utente amministratore è un utente con tutti i privilegi che dispone dell'accesso amministrativo a tutti i nostri database. Tuttavia, per motivi di sicurezza, l'account amministratore dovrebbe essere utilizzato solo per creare gli utenti e concedere loro i privilegi e non per collegarsi alle applicazioni.

La stringa di connessione viene formattata come un URI che può essere utilizzato dove i driver e le applicazioni comprendono il formato standardizzato. Le altre applicazioni possono estrarre i dettagli essenziali dall'URI della stringa di connessione.

Gli altri driver utilizzano le parti del componente dell'URI di connessione - il nome host e la porta - per i loro parametri di connessione. Il nome host si trova dopo il simbolo `@` e il numero di porta dopo `:`.

Se non hai progettato una database a cui collegarti, devi utilizzare il comando `USE my_database` per selezionarne uno; una stringa di connessione MySQL non deve specificare un database a cui collegarsi.

## SSL e MySQL

Tutte le distribuzioni Compose for MySQL hanno SSL  abilitato per impostazione predefinita; tuttavia, il modo in cui MySQL utilizza SSL significa che accetta anche connessioni non SSL. Questo significa che, quando configuri il driver MySQL della tua applicazione, devi assicurarti che crei una connessione sicura. Con la riga di comando MySQL, puoi farlo aggiungendo `--ssl-mode=REQUIRED` al comando di connessione. Per i driver dell'applicazione, le impostazioni sono specifiche per il driver. Negli esempi mostreremo i comandi che devono essere sempre e soltanto collegati con SSL abilitato.

## Utilizzo di un certificato autofirmato

Le distribuzioni Compose offrono un certificato autofirmato, che può essere utilizzato per convalidare l'host con cui si sta comunicando.

Per utilizzare un certificato autofirmato, copialo in un file. Il certificato si trova nella pagina *Overview* del tuo servizio {{site.data.keyword.composeForElasticsearch}}. 

Copia e incolla il testo da `-----BEGIN CERTIFICATE-----` a `-----END CERTIFICATE-----` in un file con l'estensione `.cert` o `.pem`, a seconda di quale driver di connessione è richiesto. Salva il file in un'ubicazione a cui puoi accedere perché avrai bisogno del percorso del certificato successivamente.

## Connessione dalla riga di comando

Per collegarti direttamente e gestire la tua distribuzione Compose for MySQL, puoi utilizzare la riga di comando. Per farlo, devi installare MySQL nella tua macchina locale. Ogni piattaforma dispone dei propri pacchetti di installazione, per cui scegli quello migliore per te. Puoi trovare i pacchetti della comunità Oracle all'indirizzo [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/). Prima di scaricarli, tieni presente che su Linux normalmente troverai MySQL nel tuo repository delle distribuzioni. Se stai utilizzando un Mac, puoi installare MySQL con Homebrew, che compila e installa l'ultima versione.

Per accedere alla tua distribuzione tramite il terminale, copia e incolla la stringa della riga di comando fornita nel pannello *Connection info* nel tuo terminale per connetterti alla tua distribuzione.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

Per abilitare SSL durante la connessione, utilizza `--ssl-mode=REQUIRED`. L'utente predefinito viene denominato "admin" che utilizzi come nome utente nel parametro `-u`. Dopo aver eseguito il comando, ti verrà richiesto di immettere la password dell'utente admin, che puoi ottenere dalla sezione delle credenziali del pannello *Connection info*.

Compose for MySQL ha SSL abilitato per impostazione predefinita, ma durante la connessione, dovresti prendere ulteriori precauzioni utilizzando l'opzione `--ssl-mode=REQUIRED` nella riga di comando. Questo impedisce il fallback di MySQL, per qualsiasi motivo, in una connessione non crittografata.

Se preferisci, puoi utilizzare il certificato autofirmato per verificare. Modifica il parametro `--ssl-mode` con `--ssl-mode=VERIFY_CA` e aggiungi `--ssl-ca` al percorso e al nome del tuo file .pem:

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## Connessione della tua applicazione

La tua applicazione si collegherà a Compose for MySQL utilizzando la stringa di connessione della tua distribuzione, questa guida di connessione rapida copre i driver di connessione e fornisce gli esempi di codice per JavaScript, Go, Python, Java e Ruby.

## Connessione con JavaScript e Node.js

Il driver principale per MySQL per Node.js è [node-mysql driver](https://github.com/mysqljs/mysql). Ne abbiamo parlato durante la configurazione di una connessione Node.js/MySQL semplice. Se desideri proseguire, assicurati che [Node.js](https://nodejs.org/) e [npm](https://github.com/npm/npm) siano installati sul tuo sistema.

Dopo aver inizializzato un nuovo progetto utilizzano `npm init`, installa il pacchetto del driver nella cartella del progetto:

```shell
npm install mysql --save
```

Il driver e le relative dipendenze sono installati nella cartella `node_modules` e il driver sarà visualizzato in `dependencies` nel `package.json`.

Puoi utilizzare il seguente codice per collegarti a MySQL.

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

**Note**
- `SHOW DATABASES` è un comando MySQL che elenca i database di cui un utente ha i privilegi.
- Vengono visualizzati tutti i database nella distribuzione perché lo script utilizza l'utente _admin_.
- I risultati della query vengono restituiti come un array di oggetti.

## Connessione con Go

Go dispone di [generic interface for SQL databases](https://golang.org/pkg/database/sql/) che utilizzato con [go-sql-driver](https://github.com/go-sql-driver/mysql) ci fornirà molte opzioni per il collegamento a MySQL. Il problema con il driver è che non possiamo verificare il certificato autofirmato. L'unica opzione TLS/SSL che abbiamo con i certificati autofirmati è `skip-verify`, che non è l'ottimale.

Per collegarti a MySQL utilizzando Go, installa prima il pacchetto _go-sql-driver_ nel tuo `$GOPATH`:

```shell
go get github.com/go-sql-driver/mysql
```

Puoi utilizzare il seguente codice per collegarti a MySQL.

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

## Connessione con Python

Puoi collegarti a MySQL con Python utilizzando [MySQL's official Python connector](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html).

Per prima cosa, installa [connector package](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html). Dopo aver installato il pacchetto, puoi collegarti al nostro database utilizzando il seguente codice:
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

Note:
- L'esempio importa il connettore MySQL e aggiunge tutti i parametri di connessione all'interno della directory `config`. Viene inizializzata una connessione sicura utilizzando il certificato autofirmato della distribuzione nella directory di connessione.
- `ssl_verify_cert` richiede l'opzione `ssl_ca`. Utilizzando l'opzione di configurazione `'ssl_verify_cert': True`, garantisci che il certificato del server e il certificato archiviato in `cert.pem` siano uguali. Se si verifica un errore con il certificato, viene restituito `ValueError`, che indica che i certificati non corrispondono.
- Un elenco utile di argomenti di connessione disponibili può essere trovato [qui](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html).
- Il connettore MySQL Python richiede che sia avviato un oggetto `cursor` per poter eseguire le query SQL. In questo esempio di codice, al metodo `cursor` dell'oggetto di connessione viene assegnata la variabile `cur` e la variabile `query` viene assegnata al comando SQL, che comunica a MySQL di visualizzare tutti i database della distribuzione.
- Il metodo `execute` esegue le operazioni del database che convertono gli oggetti Python in comandi MySQL in una connessione sicura. In questo esempio, il metodo di esecuzione comunica a MySQL di visualizzare tutti i database, interagire con loro, registrando prima l'output della console e chiudendo la connessione.

## Connessione con Java

Per collegarti con Java, per prima cosa scarica e installa [Connector/J JDBC driver](https://dev.mysql.com/downloads/connector/j/) di MySQL.

Puoi quindi collegarti a una distribuzione utilizzando il seguente codice:

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
Note
- Le informazioni di base per configurare la connessione sono all'interno della stringa di connessione. Utilizziamo questa stringa con l'API JDBC e la archiviamo nella variabile `URL`:
- Il nome utente e la password della distribuzione sono archiviati in variabili separate, che sono utilizzate per stabilire una connessione con il metodo `DriverManager.getConnection()` JDBC.
- La stringa di connessione include il nome host, la porta e il database; le opzioni SSL sono accodate alla stringa di connessione.
- L'esempio stabilisce una connessione SSL, che viene verificata utilizzando il certificato autofirmato. Puoi collegarti al server senza queste opzioni, ma la connessione potrebbe non essere sicura e creare un'avvertenza da MySQL:
```text
"Stabilire una connessione SSL senza la verifica dell'identità del server non è consigliato. In base ai requisiti MySQL 5.5.45+, 5.6.26+ e 5.7.6+, la connessione SSL deve essere stabilita per impostazione predefinita..."
```
- Per consentire al driver di elaborare il certificato, le credenziali sono salvate in un file denominato `cert.pem`. Il certificato non può essere utilizzato direttamente. Invece, crea un truststore per ospitare le credenziali del certificato utilizzando `keytool`, il seguente comando importa il file `cert.pem`, gli assegna l'alias `composeCert` e definisce il file di output come un keystore denominato `truststore`. Utilizza la password `henrythedog` per sbloccare il keystore.
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- Il metodo `setProperty` in `javax.net.ssl.trustStore` e `javax.net.ssl.trustStorePassword` utilizza le informazioni dal keystore. Le proprietà del sistema dovrebbero essere impostate all'inizio del programma da eseguire prima del runtime; preferibilmente prima che sia impostata la variabile `Connection`, in modo che possano essere bloccate prima dell'avvio della connessione SSL.
- Dopo aver creato la connessione, viene restituito un oggetto Statement e la query viene eseguita per questo oggetto. Viene restituito un ResultSet che viene utilizzato per interagire e stampare i nomi del database.

## Connessione con Ruby

Esistono molti driver MySQL per Ruby. Il codice della connessione di esempio utilizza [MySQL2](https://github.com/brianmario/mysql2).

Puoi collegarti a MySQL installando MySQL2 in base alle istruzioni nel repository Github del driver e utilizzando il seguente codice:
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
Note
- L'hash `config` contiene tutte le configurazioni di connessione, inclusa la configurazione di una connessione SSL. Per i dettagli su tutte le opzioni di configurazione, consulta [MySQL2 readme](https://github.com/brianmario/mysql2).
- Per configurare una connessione sicura utilizzando il certificato autofirmato, sono impostati `sslCA` e `sslverify`. `sslCA` è il percorso del file `.pem` o `.cert` che contiene il certificato e `sslverify` viene impostato su `true` per poter verificare se il certificato è valido.
-  Il constructor `Mysql2::Client.new` inizializza una nuova variabile di connessione, utilizzando la configurazione di connessione in `config`.
- `results` contiene un array di hash, che hanno interagito e sono stampati nella console.
