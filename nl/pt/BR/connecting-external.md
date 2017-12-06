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

# Conectando um aplicativo externo
{: #connecting-external-app}

Há duas maneiras de conectar um aplicativo externo ao {{site.data.keyword.composeForMySQL_full}}:

- Uma **Sequência de conexões** pode ser usada por algumas bibliotecas do cliente e contém todas as informações necessárias para outras bibliotecas se conectarem.

- **Linha de comandos** é um comando pré-formatado que chamará `mysql` com os parâmetros corretos.

Você localizará ambos na página *Visão geral* de seu serviço {{site.data.keyword.composeForPostgreSQL}}.

Todas as informações que você precisa para se conectar a uma implementação do MySQL for Compose.
* Como usar as [sequências de conexões](#section-the-connection-string) para seus bancos de dados.
* Como usar o [SSL](#section-ssl-and-mysql) e o [certificado autoassinado](#section-using-the-self-signed-certificate).
* Como se conectar por meio da [linha de comandos](#section-connecting-from-the-command-line) ou de seus [aplicativos](#section-connecting-your-application).

## A sequência de conexões

A sequência de conexões é seu primeiro ponto de referência ao se conectar ao Compose for MySQL; ele contém quase todas as informações que você precisa para se conectar a um banco de dados.

```
mysql://[username]:[password]@[host]:[port]/compose
```

**Nota:** os exemplos neste guia se conectam à conta do usuário administrativo. O usuário administrativo é um usuário totalmente privilegiado que possui acesso administrativo a todos os nossos bancos de dados. No entanto, por motivos de segurança, a conta de administrador deve ser usada somente para criar usuários e conceder os privilégios a eles e não para se conectar a aplicativos.

A sequência de conexões é formatada como um URI que pode ser usado onde os drivers e aplicativos entendem o formato padronizado. Outros aplicativos podem extrair os detalhes essenciais do URI da sequência de conexões.

Outros drivers usam partes do componente do URI de conexão, o nome do host e a porta, para seus parâmetros de conexão. O nome do host está localizado após o símbolo `@` e o número da porta está após `:`.

Se não designar um banco de dados para se conectar, você precisará do comando `USE my_database` para selecionar um banco de dados; uma conexão MySQL não precisa especificar um banco de dados para se conectar.

## SSL e MySQL

Todas as implementações do Compose for MySQL têm o SSL ativado por padrão; no entanto, a maneira como o MySQL executa o SSL significa que ele também aceitará conexões não SSL. Isso significa que, ao configurar o driver MySQL de seu aplicativo, você precisará assegurar que ele crie uma conexão segura. Com a linha de comandos do MySQL, é possível executar isso incluindo `--ssl-mode=REQUIRED` no comando de conexão. Para drivers de aplicativos, as configurações são específicas para o driver. Nos exemplos, mostraremos comandos que devem sempre e somente se conectar ao SSL ativado.

## Usando o certificado autoassinado

As implementações do Compose oferecem um certificado autoassinado, que pode ser usado para validar o host com o qual se está conversando.

Para usar o certificado autoassinado, copie-o para um arquivo. O certificado está localizado na página *Visão geral* de seu serviço {{site.data.keyword.composeForElasticsearch}}. 

Copie e cole o texto de `-----BEGIN CERTIFICATE-----` para `-----END CERTIFICATE-----` em um arquivo com a extensão `.cert` ou `.pem`, dependendo de qual o driver de conexão requer. Salve o arquivo em um local que seja possível acessar porque precisaremos do caminho do certificado mais tarde.

## Conectando-se por meio da linha de comandos

Para conectar-se diretamente e administrar sua implementação do Compose for MySQL, é possível usar a linha de comandos. Para fazer isso, você precisa instalar o MySQL em sua máquina local. Cada plataforma tem os seus próprios pacotes de instalação, portanto escolha um que funcione melhor para você. É possível localizar pacotes da comunidade Oracle em [http://dev.mysql.com/downloads/](http://dev.mysql.com/downloads/). Antes de fazer download de lá, esteja ciente de que no Linux você geralmente localizará o MySQL em seu repositório de distribuição. Se você está usando um Mac, é possível instalar o MySQL com Homebrew, que compila e instala a versão mais recente.

Para acessar sua implementação por meio do terminal, copie e cole a sequência de linha de comandos fornecida no painel *Informações de conexão* em seu terminal para conectar-se à sua implementação.

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=REQUIRED
```

Para ativar o SSL ao se conectar, use `--ssl-mode=REQUIRED`. O usuário padrão é denominado "admin", que você usa como o nome do usuário no parâmetro `-u`. Depois de executar o comando, você será solicitado a inserir a senha do usuário administrativo, que é possível obter na seção de credenciais do painel *Informações de conexão*.

O Compose for MySQL tem o SSL ativado por padrão, mas ao se conectar, é necessário tomar precauções extras usando a opção `--ssl-mode=REQUIRED` na linha de comandos. Isso para o fallback do MySQL, por qualquer motivo, para uma conexão não criptografada.

Se preferir, é possível usar o certificado autoassinado para verificar. Mude o parâmetro `--ssl-mode` para `--ssl-mode=VERIFY_CA` e inclua `--ssl-ca` com o caminho e nome de seu arquivo .pem:

```shell
mysql -u [username] -p --host aws-us-east-1-portal.5.dblayer.com --port 16967 --ssl-mode=VERIFY_CA --ssl-ca=<your_file>.pem
```

## Conectando seu aplicativo

Seu aplicativo se conectará ao Compose for MySQL usando a sequência de conexões de sua implementação. Este guia de conexão rápida cobre os drivers de conexão e fornece amostras de código para JavaScript, Go, Python, Java e Ruby.

## Conectando-se ao JavaScript e Node.js

O driver de liderança para o MySQL for Node.js é o [Driver node-mysql](https://github.com/mysqljs/mysql). Vamos percorrer a configuração de uma conexão simples do Node.js/MySQL aqui. Se você deseja seguir adiante, certifique-se de que o [Node.js](https://nodejs.org/) e o [npm](https://github.com/npm/npm) estejam instalados em seu sistema.

Após a inicialização de um novo projeto usando `npm init`, instale o pacote de drivers na pasta do projeto:

```shell
npm install mysql --save
```

O driver e suas dependências são instalados na pasta `node_modules` e o driver aparecerá em `dependences` no arquivo `package.json`.

É possível usar o código a seguir para se conectar ao MySQL.

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
- `SHOW DATABASES` é um comando MySQL que lista os bancos de dados para os quais um usuário tem privilégios.
- Todos os bancos de dados na implementação são exibidos porque o script usa o usuário _admin_.
- Os resultados da consulta são retornados como uma matriz de objetos.

## Conectando-se ao Go

O Go tem uma [interface genérica para bancos de dados SQL](https://golang.org/pkg/database/sql/) e usá-la com o [go-sql-driver](https://github.com/go-sql-driver/mysql) nos fornecerá várias opções para se conectar ao MySQL. O problema com o driver é que não podemos verificar o certificado autoassinado. A única opção TLS/SSL que temos com certificados autoassinados é `skip-verify`, que é menor que o ideal.

Para se conectar ao MySQL usando Go, primeiro instale o pacote _go-sql-driver_ em seu `$GOPATH`:

```shell
go get github.com/go-sql-driver/mysql
```

É possível usar o código a seguir para se conectar ao MySQL.

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

## Conectando-se ao Python

É possível se conectar ao MySQL com Python usando o [Conector Python oficial do MySQL](https://dev.mysql.com/doc/connector-python/en/connector-python-introduction.html).

Primeiro, instale o [pacote do conector](https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html). Depois de instalar o pacote, é possível se conectar ao nosso banco de dados usando o código a seguir:
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
- O exemplo importa o conector do MySQL e inclui quaisquer parâmetros de conexão dentro de um dicionário `config`. Uma conexão segura é inicializada usando o certificado autoassinado da implementação no dicionário de conexão.
- `ssl_verify_cert` requer a opção `ssl_ca`. Usar a opção de configuração `'ssl_verify_cert': True` assegura que o certificado do servidor e o certificado armazenado em `cert.pem` sejam os mesmos. Se houver um erro de certificado, um `ValueError` será retornado, indicando que os certificados não correspondem.
- Uma lista útil dos argumentos de conexão disponíveis pode ser localizada [aqui](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html).
- O conector do MySQL Python requer que um objeto `cursor` seja instanciado para executar consultas SQL. Nesta amostra de código, o método `cursor` do objeto de conexão aqui é designado à variável `cur` e a variável `query` é designada ao comando SQL, que instrui o MySQL a mostrar todos os bancos de dados da implementação.
- O método `execute` executa operações do banco de dados que convertem objetos do Python em comandos MySQL em uma conexão segura. Neste exemplo, o método de execução instrui o MySQL a mostrar todos os bancos de dados, iterando sobre eles, antes de registrar a saída no console e fechar a conexão.

## Conectando-se ao Java

Para se conectar com Java, primeiro faça download e instale o [Conector/Driver JDBC](https://dev.mysql.com/downloads/connector/j/) do MySQL.

É possível então se conectar a uma implementação usando o código a seguir:

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
- As informações básicas para configurar uma conexão estão dentro da sequência de conexões. Usamos isso com a API JDBC e armazenamos essa sequência na variável `URL`:
- O nome do usuário e a senha para a implementação são armazenados em variáveis separadas, que são usadas para estabelecer uma conexão com o método JDBC `DriverManager.getConnection()`.
- A sequência de conexões inclui o nome do host, a porta e o banco de dados; as opções de SSL são anexadas à sequência de conexões.
- A amostra estabelece uma conexão SSL, que é verificada usando o certificado autoassinado. É possível se conectar ao servidor sem essas opções, mas a conexão seria insegura e resultaria em um aviso do MySQL:
```text
"Não é recomendado estabelecer a conexão SSL sem a verificação de identidade do servidor. Segundo os requisitos do MySQL 5.5.45+, 5.6.26+ e 5.7.6+, a conexão SSL deve ser estabelecida por padrão..."
```
- Para permitir que o driver para processar o certificado, as credenciais são salvas em um arquivo chamado `cert.pem`. O certificado não pode ser usado diretamente. Em vez disso, crie um armazenamento confiável para reter as credenciais do certificado usando `keytool`. O comando a seguir importa o arquivo `cert.pem`, designa o alias `composeCert` e define o arquivo de saída como um keystore chamado `truststore`. Ele usa a senha `henrythedog` para desbloquear o keystore.
```shell
keytool -import --alias composeCert -file ./cert.pem -keystore ./truststore -storepass henrythedog
```
- O método `setProperty` em `javax.net.ssl.trustStore` e `javax.net.ssl.trustStorePassword` usa as informações do keystore. As propriedades de sistema devem ser configuradas na parte superior do programa para serem executadas mais cedo no tempo de execução; de preferência antes de a variável `Connection` ser configurada, para que elas sejam bloqueadas antes de iniciar uma conexão SSL.
- Depois de criar a conexão, um objeto Statement é retornado e a consulta é executada com relação ao objeto. Isso retorna um ResultSet que é usado para iterar e imprimir os nomes do banco de dados.

## Conectando-se ao Ruby

Há vários drivers MySQL para o Ruby. O código de conexão de amostra usa [MySQL2](https://github.com/brianmario/mysql2).

É possível se conectar ao MySQL instalando o MySQL2 de acordo com as instruções no repositório Github do driver e usando o código a seguir:
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
- O hash `config` contém todas as configurações de conexão, incluindo a configuração de uma conexão SSL. Para obter detalhes de todas as opções de configuração, veja o [Leia-me do MySQL2](https://github.com/brianmario/mysql2).
- Para configurar uma conexão segura usando o certificado autoassinado, `sslCA` e `sslverify` são configurados. `sslCA` é o caminho do arquivo `.pem` ou `.cert` que contém o certificado e `sslverify` é configurado para `true` para verificar um certificado válido.
-  O construtor `Mysql2::Client.new` inicializa uma nova variável de conexão, usando a configuração de conexão em `config`.
- `results` contém uma matriz de hashes, que são iterados e impressos no console.
