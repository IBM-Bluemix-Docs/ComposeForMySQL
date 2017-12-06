---

copyright:
  years: 2016,2017
lastupdated: "2017-10-23"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Con un'ampia serie secondaria di ANSI SQL 99 e una vasta gamma delle relative estensioni, inclusi il documento JSON, la ricerca di test ocompleto e le viste aggiornabili, MySQL offre una ricca tavolozza per gli sviluppatori per progettare le loro applicazioni. Gli amministratori possono inoltre trovare un'ampia selezione di strumenti di gestione del database che possono utilizzare con MySQL. {{site.data.keyword.composeForMySQL_full}} permette a MySQL di estendere le funzionalità di MySQL a gestirle al tuo posto, offrendo un sistema di distribuzione con ridimensionamento automatico facile da utilizzare che distribuisce l'elevata disponibilità e la ridondanza e i backup automatizzati.
{:shortdesc}

## Creazione di un'istanza del servizio Compose per MySQL

[Crea un'istanza {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

Quando crei un'istanza del servizio, scegli un nome per il tuo servizio e un nome per la credenziale. Lascia il servizio senza bind; puoi collegare un'applicazione al tuo servizio successivamente utilizzando le credenziali fornite quando è stato eseguito il provisioning del servizio.  I vari valori delle credenziali sono elencati nella sezione "Credenziali disponibili".

Quando esegui il provisioning della tua istanza {{site.data.keyword.composeForMySQL}} puoi scegliere i piani *Standard* o *Enterprise*. Con il piano *Enterprise*, puoi eseguire il provisioning della tua istanza {{site.data.keyword.composeForMySQL}} in un cluster {{site.data.keyword.composeEnterprise}} disponibile. {{site.data.keyword.composeEnterprise}} fornisce la sicurezza e l'isolamento necessari per la conformità aziendale e utilizza la rete dedicata per garantire le prestazioni dei database distribuiti. Per ulteriori dettagli, consulta la [Documentazione aziendale Compose](../ComposeEnterprise/index.html).

## Gestione di Compose for MySQL

Puoi gestire il tuo servizio dal dashboard del servizio. Qui puoi trovare le informazioni sul tuo database {{site.data.keyword.cloud}} Compose e su come collegarti ad esso. Puoi anche:
- gestire i tuoi backup
- assegnare ulteriori risorse al tuo servizio
- modificare la password del servizio
- utilizzare le whitelist per limitare l'accesso ai tuoi database 
Per ulteriori informazioni, consulta [Impostazioni](./dashboard-settings.html).


## Connessione a Compose for MySQL

Puoi collegarti al tuo servizio utilizzando le credenziali create insieme al servizio o con le stringhe di connessione e la riga di comando forniti nella scheda *Overview* nel tuo dashboard del servizio.

## Connessione di un'applicazione {{site.data.keyword.cloud_notm}} a Compose for MySQL

Per collegare un'applicazione {{site.data.keyword.cloud_notm}} al tuo servizio, utilizza le credenziali create insieme al servizio. Puoi trovare le informazioni su come collegare un'applicazione {{site.data.keyword.cloud_notm}} al tuo servizio in [Connessione a un'applicazione {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Connessione a Compose for MySQL dall'esterno di {{site.data.keyword.cloud_notm}}

Se desideri collegarti al tuo servizio dall'esterno di {{site.data.keyword.cloud_notm}}, puoi utilizzare la riga di comando o le stringhe di connessione fornite. Puoi trovare le informazioni su come collegarti in [Connessione a un'applicazione esterna](./connecting-external.html).
