---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Architettura 
{: #architecture}

## Replica

Una distribuzione {{site.data.keyword.composeForMySQL_full}} inizia con tre nodi di dati in un cluster, distribuiti nelle zone di disponibilità della regione. I dati vengono replicati tra tutti e tre i nodi; se un membro di dati nel cluster diventa irraggiungibile, il tuo cluster continua a funzionare normalmente. Il cluster viene configurato in modo che, se si verifica un malfunzionamento del membro leader nel cluster, lo slave corrente viene promosso a leader entro 60 secondi da quando il leader smette di rispondere. 

## Crittografia del disco

Tutti i servizi {{site.data.keyword.composeForMySQL}} hanno la crittografia dei dati inattivi. I tuoi dati si trovano su server che hanno la crittografia a livello di volume abilitata. 

Poiché {{site.data.keyword.composeForMySQL}} è un servizio gestito, gli operatori di {{site.data.keyword.cloud}} Compose possono visualizzare i dati. Oltre alla crittografia del disco, ti consigliamo di crittografare le informazioni personali prima di archiviarle nel database o di usare delle estensioni o delle funzioni per abilitare la crittografia sul database stesso. Anche se questi metodi possono influire sull'usabilità o sulle prestazioni, è buona norma assicurarsi che le informazioni personali siano protette con la crittografia.

## Ridimensionamento automatico

Le risorse vengono ridimensionate automaticamente in base all'utilizzo di archiviazione disco totale dei database MySQL. L'utilizzo della memoria è basato su una proporzione di archiviazione di cui viene eseguito il provisioning a un rapporto di 1:10. Queste risorse sono raccolte in bundle come unità.

Il ridimensionamento automatico è progettato per rispondere alle tendenze a medio e a lungo termine del tuo database. Il tuo servizio viene controllato ogni ora e, se sta esaurendo lo spazio su disco, delle ulteriori unità vengono assegnate alla distribuzione.

Il ridimensionamento automatico non riduce le distribuzioni in cui l'utilizzo di disco/memoria si è ridotto. Le risorse di cui è stato eseguito il provisioning ai tuoi database rimarranno per le tue future esigenze oppure finché non riduci manualmente la tua distribuzione.
{: .tip}
