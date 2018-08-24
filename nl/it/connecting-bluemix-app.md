---

copyright:
  years: 2016,2018
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connessione a un'applicazione {{site.data.keyword.cloud_notm}}

Per collegare un'applicazione {{site.data.keyword.cloud}} al tuo servizio, utilizza le credenziali create quando è stato eseguito il provisioning del servizio. L'applicazione di esempio illustra come utilizzare Node.js per il collegamento utilizzando le credenziali fornite e come creare un database e leggere e scrivere su di esso.

## Collegamento utilizzando l'applicazione di esempio 'Hello World'

L'applicazione di esempio [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) illustra come utilizzare Node.js per il collegamento utilizzando le credenziali fornite. L'applicazione crea, legge da, e scrive su un database.

Scarica l'applicazione di esempio e segui le istruzioni nel file readme. In seguito, nella pagina dei dettagli della tua applicazione in {{site.data.keyword.cloud_notm}}, fai clic su **Visualizza applicazione** per visualizzare il contenuto della tabella *esempi*.

## Credenziali disponibili

Nome campo|Descrizione
----------|-----------
`db_type`|Il tipo di database offerto dal servizio, in questo caso `mysql`.
`name`|Il nome di distribuzione del database.
`uri_cli`|Una riga di comando shell `mysql` che esegue il collegamento all'istanza del database.
`ca_certificate_base64`|Un certificato auto-firmato che viene utilizzato per confermare che un'applicazione sia collegata al server corretto. Il certificato si basa su codifica base64.
`deployment_id`|Un identificativo interno per il servizio come creato in Compose.
`uri`|L'URI da utilizzare quando esegui il collegamento al servizio, include lo schema (`mysql:`), il nome utente e la password amministratore, il nome host del server e il numero di porta a cui collegarsi.
`uri_direct_1`|Un URI secondario che può essere utilizzato durante il collegamento al servizio. Formato come l'`uri`.
`uri_cli_1`|Una riga di comando shell `mysql` secondaria che esegue il collegamento all'istanza del database.
{: caption="Tabella 1. Credenziali di Compose for MySQL" caption-side="top"}

**Nota:** due portali `haproxy` forniscono l'accesso al servizio MySQL. Possono essere utilizzati sia `uri` che `uri_direct_1` per il collegamento. Nelle tue applicazioni, passa da `uri` a `uri_direct_1` per gestire le risposte agli errori di connessione.
