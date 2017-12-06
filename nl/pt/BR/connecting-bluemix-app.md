---

Copyright:
  Years: 2016,2017
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conectando um aplicativo {{site.data.keyword.cloud_notm}}

Para conectar um aplicativo {{site.data.keyword.cloud}} a seu serviço, use as credenciais de serviço que são criadas quando o serviço é provisionado. O aplicativo de amostra demonstra como usar o Node.js para se conectar usando as credenciais fornecidas e como criar um banco de dados e ler e gravar no banco de dados.

## Conectando usando o aplicativo de amostra 'Hello World'

O aplicativo de amostra [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) demonstra como usar o Node.js para se conectar a seu serviço usando as credenciais fornecidas. O aplicativo cria, lê e grava em um banco de dados

Faça download do aplicativo de amostra e siga as instruções no arquivo leia-me. Em seguida, em sua página de detalhes do aplicativo no {{site.data.keyword.cloud_notm}}, clique em **Visualizar app** para visualizar os conteúdos da tabela *exemplos*.

## Credenciais disponíveis

Campo de nome|Descrição
----------|-----------
`db_type`|O tipo de banco de dados que é oferecido pelo serviço, nesse caso `mysql`.
`name`|O nome da implementação do banco de dados.
`uri_cli`|Uma linha de comandos shell `mysql` que se conecta à instância de banco de dados.
`ca_certificate_base64`|Um certificado autoassinado que é usado para confirmar se um aplicativo está se conectando ao servidor apropriado. O certificado é codificado em base64.
`deployment_id`|Um identificador interno para o serviço conforme criado no Compose.
`uri`|O URI que é usado ao se conectar ao serviço, que inclui o esquema (`mysql:`), o nome do usuário administrativo e a senha, o nome do host do servidor, o número da porta à qual se conectar e o nome do vhost.
{: caption="Tabela 1. Credenciais do Compose for MySQL" caption-side="top"}
