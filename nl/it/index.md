---

copyright:
  years: 2016,2018
lastupdated: "2018-03-26"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informazioni su {{site.data.keyword.composeForMySQL}}
{: #about-compose-for-mysql}

Con un'ampia serie secondaria di ANSI SQL 99 e una vasta gamma delle relative estensioni, inclusi il documento JSON, la ricerca di testo completo e le viste aggiornabili, MySQL offre una ricca tavolozza per gli sviluppatori per progettare le loro applicazioni. Gli amministratori possono inoltre trovare un'ampia selezione di strumenti di gestione del database che possono utilizzare con MySQL. {{site.data.keyword.composeForMySQL_full}} estende le funzionalità di MySQL gestendole al tuo posto, offrendo un sistema di distribuzione con ridimensionamento automatico facile da utilizzare che distribuisce l'elevata disponibilità e la ridondanza e i backup automatizzati.
{:shortdesc}

## Creazione di una istanza del servizio {{site.data.keyword.composeForMySQL}}

Puoi creare un servizio {{site.data.keyword.composeForMySQL}} dalla pagina [{{site.data.keyword.composeForMySQL}}](https://console.{DomainName}/catalog/services/compose-for-mysql/) nel catalogo {{site.data.keyword.cloud_notm}}.

Scegli un nome del servizio, una regione, un'organizzazione e uno spazio in cui eseguire il provisioning del servizio. Puoi utilizzare il campo **Select a database version** per scegliere tra le versioni del database disponibili.

Quando esegui il provisioning della tua istanza {{site.data.keyword.composeForMySQL}} puoi scegliere i piani *Standard* o *Enterprise*. Con il piano *Enterprise*, puoi eseguire il provisioning della tua istanza {{site.data.keyword.composeForMySQL}} in un cluster {{site.data.keyword.composeEnterprise}} disponibile. {{site.data.keyword.composeEnterprise}} fornisce la sicurezza e l'isolamento necessari per la conformità aziendale e utilizza la rete dedicata per garantire le prestazioni dei database distribuiti. Per ulteriori dettagli, consulta la [Documentazione aziendale Compose](../ComposeEnterprise/index.html).

## Gestione di {{site.data.keyword.composeForMySQL}}

Puoi gestire il tuo servizio dal dashboard del servizio. Qui puoi trovare le informazioni sul tuo database {{site.data.keyword.cloud}} Compose e su come collegarti ad esso. Puoi anche:
- gestire i tuoi backup
- assegnare ulteriori risorse al tuo servizio
- modificare la password del servizio
- utilizzare le whitelist per limitare l'accesso ai tuoi database 

Per ulteriori informazioni, consulta [Impostazioni](./dashboard-settings.html).

{{site.data.keyword.composeForMySQL}} si basa sui ruoli Cloud Foundry per gestire l'accesso al servizio. Solo gli utenti con il ruolo di sviluppatore possono visualizzare o utilizzare il dashboard del servizio. Per ulteriori informazioni sui ruoli Cloud Foundry, consulta le pagine [Cloud Foundry access](https://console.bluemix.net/docs/iam/cfaccess.html#cfaccess) e [Managing Cloud Foundry access](https://console.bluemix.net/docs/iam/mngcf.html#mngcf).
{: .tip}

## Connessione a {{site.data.keyword.composeForMySQL}}

Puoi collegarti al tuo servizio utilizzando le credenziali create insieme al servizio o con le stringhe di connessione e la riga di comando forniti nella scheda *Overview* nel tuo dashboard del servizio.

## Connessione di un'applicazione {{site.data.keyword.cloud_notm}} a {{site.data.keyword.composeForMySQL}}

Per collegare un'applicazione {{site.data.keyword.cloud_notm}} al tuo servizio, utilizza le credenziali create insieme al servizio. Puoi trovare le informazioni su come collegare un'applicazione {{site.data.keyword.cloud_notm}} al tuo servizio in [Connessione a un'applicazione {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Connessione a {{site.data.keyword.composeForMySQL}} dall'esterno di {{site.data.keyword.cloud_notm}}

Se desideri collegarti al tuo servizio dall'esterno di {{site.data.keyword.cloud_notm}}, puoi utilizzare la riga di comando o le stringhe di connessione fornite. Puoi trovare le informazioni su come collegarti in [Connessione a un'applicazione esterna](./connecting-external.html).
