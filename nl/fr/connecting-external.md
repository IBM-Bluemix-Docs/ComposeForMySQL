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

# Connexion d'une application externe
{: #connecting-external-app}

Deux moyens permettent de connecter une application externe à {{site.data.keyword.composeForMySQL_full}} :

- Une **chaîne de connexion**, qui peut être utilisée par certaines bibliothèques client et qui contient toutes les informations requises pour la connexion d'autres bibliothèques.

- Une **ligne de commande**, qui est une commande préformatée qui appellera `mysql` avec les paramètres appropriés.

Les deux sont disponibles sur la page *Vue d'ensemble* du service {{site.data.keyword.composeForPostgreSQL}}.

Vous trouverez toutes les informations dont vous avez besoin pour vous connecter à MySQL pour un déploiement Compose dans les rubriques suivantes :
* Comment utiliser les [chaînes de connexion](#section-the-connection-string) pour vos bases de données.
* Comment utiliser [SSL](#section-ssl-and-mysql) et le [certificat autosigné](#section-using-the-self-signed-certificate).
* Comment se connecter via la [ligne de commande](#section-connecting-from-the-command-line) ou à partir de vos [applications](#section-connecting-your-application).

## Chaîne de connexion

La chaîne de connexion est votre premier point de référence lors de la connexion à Compose for MySQL. Elle contient pratiquement toutes les informations nécessaires pour se connecter à une base de données.

```
mysql://[username]:[password]@[host]:[port]/compose
```

**Remarque :** Les exemples de ce guide établissent la connexion avec le compte administrateur. L'administrateur est un utilisateur privilégié doté de droits d'accès d'administration à toutes vos bases de données. Toutefois, pour des raisons de sécurité, le compte administrateur doit être utilisé uniquement pour créer des utilisateurs et leur accorder des privilèges, et non pour se connecter à des applications.

La chaîne de connexion est formatée comme un identificateur URI utilisable avec les pilotes et les applications qui reconnaissent le format standardisé. Les autres applications peuvent extraire les détails essentiels depuis l'URI de la chaîne de connexion.

D'autres pilotes utilisent des parties de composant de l'URI de connexion (nom d'hôte et port) pour leurs paramètres de connexion. Le nom d'hôte se trouve après le symbole `@` et le numéro de port après le signe `:`.

Si vous ne désignez pas une base de données à laquelle se connecter, vous avez besoin de la commande `USE my_database` pour sélectionner une base de données ; une connexion MySQL ne nécessite pas d'indiquer une base de données.

## SSL et MySQL

SSL est activé par défaut pour tous les déploiements Compose for MySQL. Toutefois, la manière dont MySQL traite SSL implique que les connexions non SSL sont également acceptées. Cela signifie que, lors de la configuration du pilote MySQL de l'application, vous devez vous assurer de la création d'une connexion sécurisée. La ligne de commande MySQL vous permet d'effectuer cette opération en ajoutant `--ssl-mode=REQUIRED` à la commande de connexion. Pour les pilotes d'application, le paramétrage est propre à chaque pilote. Dans les exemples, nous verrons des commandes qui doivent toujours et uniquement établir une connexion avec SSL activé.

## Utilisation du certificat autosigné

Les déploiements Compose offrent un certificat autosigné qui permet de valider l'hôte concerné.

Pour utiliser le certificat autosigné, copiez-le dans un fichier. Ce certificat se trouve sur la page *Vue d'ensemble* du service {{site.data.keyword.composeForElasticsearch}}. 

Copiez et collez le texte depuis `-----BEGIN CERTIFICATE-----` jusqu'à `-----END CERTIFICATE-----` dans un fichier avec extension `.cert` ou `.pem`, selon le pilote de connexion requis. Sauvegardez le fichier dans un emplacement auquel vous pouvez accéder car nous aurons besoin du chemin du certificat ultérieurement.

## Connexion à partir de la ligne de commande

Pour vous connecter directement à votre déploiement Compose for MySQL et l'administrer, vous pouvez utiliser la ligne de commande. Pour ce faire, vous devez installer MySQL sur votre machine locale. Etant donné que chaque plateforme a ses propres packages d'installation, sélectionnez celui qui fonctionne le mieux pour vous. Des packages de la communauté Oracle sont disponibles à l'adresse [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/). Avant d'effectuer un téléchargement, n'oubliez pas que sous Linux vous disposez généralement de MySQL dans votre référentiel de distribution. Si vous utilisez un Mac, vous pouvez installer MySQL avec Homebrew, qui compile et installe la version la plus récente.

Pour accéder à votre déploiement via le terminal, copiez et collez la chaîne de ligne de commande fournie dans le panneau *Informations de connexion* sur votre terminal pour vous connecter à votre déploiement.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

Pour activer SSL lors de la connexion, utilisez `--ssl-mode=REQUIRED`. L'utilisateur par défaut se nomme "admin" que vous utilisez comme nom d'utilisateur dans le paramètre `-u`. Une fois la commande exécutée, vous êtes invité à entrer le mot de passe de l'administrateur, qui se trouve dans la section des données d'identification du panneau *Informations de connexion*.

SSL est activé par défaut dans Compose for MySQL, mais lors de la connexion, vous devez pendre des précautions supplémentaires en utilisant l'option `--ssl-mode=REQUIRED` sur la ligne de commande. Cette option évite que MySQL revienne, pour une raison ou une autre, à une connexion non chiffrée.

Si vous préférez, vous pouvez utiliser le certificat autosigné pour vérifier. Modifiez le paramètre `--ssl-mode` en `--ssl-mode=VERIFY_CA` et ajoutez `--ssl-ca` avec le chemin et le nom de votre fichier .pem :

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## Connexion de votre application

Votre application se connectera à Compose for MySQL à l'aide de la chaîne de connexion de votre déploiement. Ce guide de connexion rapide traite des pilotes de connexion et donne des exemples de code pour JavaScript, Go, Python, Java et Ruby.

## Connexion avec JavaScript et Node.js

Le principal pilote pour MySQL pour Node.js est le [pilote node-mysql](https://github.com/mysqljs/mysql). Nous allons ici parcourir les étapes de configuration d'une connexion Node.js/MySQL simple. Avant de poursuivre, vérifiez que [Node.js](https://nodejs.org/) et [npm](https://github.com/npm/npm) sont installés sur votre système.

Après avoir initialisé un nouveau projet à l'aide de `npm init`, installez le package de pilote dans le dossier du projet :

```shell
npm install mysql --save
```

Le pilote et ses dépendances sont installés dans le dossier `node_modules` et le pilote s'affiche sous `dependencies` dans le fichier `package.json`.

Vous pouvez utiliser le code suivant pour vous connecter à MySQL.

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

**Remarques**
- `SHOW DATABASES` est une commande MySQL qui répertorie les bases de données sur lesquelles un utilisateur a des privilèges.
- Toutes les bases de données du déploiement sont affichées car le script se sert de l'utilisateur _admin_.
- Les résultats de la requête sont renvoyés sous forme de tableau d'objets.

## Connexion avec Go

Go dispose d'une [interface générique pour les bases de données SQL](https://golang.org/pkg/database/sql/) qui, lorsqu'elle est utilisée avec [go-sql-driver](https://github.com/go-sql-driver/mysql) nous fournit plusieurs options de connexion à MySQL. Le problème avec le pilote est que nous ne pouvons pas vérifier le certificat autosigné. La seule option TLS/SSL dont nous disposons avec les certificats autosignés est `skip-verify`, qui est moins performante.

Pour une connexion à MySQL à l'aide de Go, commencez par installer le package _go-sql-driver_ sur `$GOPATH` :

```shell
go get github.com/go-sql-driver/mysql
```

Vous pouvez utiliser le code suivant pour vous connecter à MySQL.

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

## Connexion avec Python

Vous pouvez vous connecter à MySQL avec Python en utilisant le [connecteur Python officiel de MySQL](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html).

Tout d'abord, installez le [package du connecteur](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html). Une fois le package installé, vous pouvez vous connecter à notre base de données à l'aide du code suivant :
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

Remarques :
- L'exemple importe le connecteur MySQL et ajoute tous les paramètres de connexion dans un dictionnaire `config`. Une connexion sécurisée est initialisée à l'aide du certificat autosigné du déploiement dans le dictionnaire de connexion.
- `ssl_verify_cert` requiert l'option `ssl_ca`. L'utilisation de l'option de configuration `'ssl_verify_cert': True` garantit que le certificat du serveur et le certificat stocké dans `cert.pem` sont identiques. En cas d'erreur de certificat, une `ValueError` est renvoyée, indiquant que les certificats ne correspondent pas.
- Une liste très utile des arguments de connexion disponibles se trouve [ici](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html).
- Le connecteur Python de MySQL nécessite qu'un objet `cursor` soit instancié pour exécuter des requêtes SQL. Dans cet exemple de code, la variable `cur` est affectée à la méthode `cursor` de l'objet connexion et la variable `query` est affectée à la commande SQL, qui demande à MySQL d'afficher toutes les bases de données du déploiement.
- La méthode `execute` exécute des opérations de base de données qui convertissent les objets Python en commandes MySQL via une connexion sécurisée. Dans cet exemple, la méthode d'exécution demande à MySQL d'afficher toutes les bases de données, en procédant par itération, avant de consigner la sortie sur la console et de fermer la connexion.

## Connexion avec Java

Pour vous connecter avec Java, commencez par télécharger et installer [pilote JDBC Connector/J](https://dev.mysql.com/downloads/connector/j/) de MySQL.

Vous pouvez ensuite vous connecter à un déploiement à l'aide du code suivant :

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
Remarques
- Les informations de base permettant de configurer une connexion se trouvent dans la chaîne de connexion. Nous l'utilisons cette chaîne avec l'API JDBC et nous la stockons dans la variable `URL`:
- Le nom d'utilisateur et le mot de passe du déploiement sont stockés dans des variables distinctes, utilisées pour établir une connexion avec la méthode JDBC `DriverManager.getConnection()`.
- La chaîne de connexion inclut le nom d'hôte, le port et la base de données ; les options SSL sont ajoutées à la chaîne de connexion.
- L'exemple établit une connexion SSL, qui est vérifiée à l'aide du certificat autosigné. Vous pouvez vous connecter au serveur sans ces options, mais la connexion ne sera pas sécurisée et générera un avertissement de MySQL :
```text
"Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default..."
```
- Pour permettre au pilote de traiter le certificat, les données d'identification sont sauvegardées dans un fichier nommé `cert.pem`. Le certificat ne peut pas être utilisé directement. A la place, créez un fichier de clés certifiées destiné à recevoir les données d'identification du certificat à l'aide de `keytool`. La commande suivante importe le fichier `cert.pem`, lui affecte l'alias `composeCert` et définit le fichier de sortie en tant que magasin de clés nommé `truststore`. Le mot de passe `henrythedog` est utilisé pour déverrouiller le magasin de clés.
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- La méthode `setProperty` sur `javax.net.ssl.trustStore` et `javax.net.ssl.trustStorePassword` utilise les informations issues du magasin de clés. Les propriétés système doivent être définies vers le début du programme afin d'être traitées très tôt lors de l'exécution, de préférence avant la définition de la variable `Connection` pour qu'elles soient verrouillées avant le démarrage d'une connexion SSL.
- Une fois la connexion créée, un objet Statement est renvoyé et la requête est exécutée par rapport à l'objet. Un ensemble de résultats, utilisé pour itérer et afficher les noms de base de données, est renvoyé.

## Connexion avec Ruby

Il existe de nombreux pilotes MySQL pour Ruby. L'exemple de code de connexion utilise [MySQL2](https://github.com/brianmario/mysql2).

Vous pouvez vous connecter à MySQL en installant MySQL2 selon les instructions fournies dans le référentiel Github du pilote et en utilisant le code suivant :
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
Remarques
- Le hachage `config` contient l'intégralité de la configuration de connexion, y compris la configuration d'une connexion SSL. Pour plus d'informations sur toutes les option de configuration, voir le fichier [Readme de MySQL2](https://github.com/brianmario/mysql2).
- Pour configurer une connexion sécurisée en utilisant le certificat autosigné, `sslCA` et `sslverify` sont définis. `sslCA` est le chemin d'accès au fichier`.pem` ou `.cert` qui contient le certificat et `sslverify` est défini sur `true` afin de vérifier la validité du certificat.
-  Le constructeur `Mysql2::Client.new` initialise une nouvelle variable de connexion en utilisant la configuration de connexion que contient `config`.
- `results` contient un tableau de hachages, qui sont itérés et affichés sur la console.
