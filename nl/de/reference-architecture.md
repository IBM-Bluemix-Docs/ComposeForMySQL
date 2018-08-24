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

# Architektur 
{: #architecture}

## Replikation

Die Basiskonfiguration einer {{site.data.keyword.composeForMySQL_full}}-Bereitstellung umfasst drei Datenknoten in einem Cluster, die über die Verfügbarkeitszonen der Region verteilt sind. Die Daten werden auf allen drei Knoten repliziert. Wenn ein Datenelement (Member) im Cluster nicht mehr erreichbar sein sollte, setzt Ihr Cluster seinen Betrieb ordnungsgemäß fort. Der Cluster ist so konfiguriert, dass bei Ausfallen des im Cluster als Leader fungierenden Members der aktuelle Slave innerhalb von 60 Sekunden, nachdem der Leader nicht mehr erreichbar war, zum Leader hochgestuft wird. 

## Plattenverschlüsselung

Für alle {{site.data.keyword.composeForMySQL}}-Services erfolgt die Verschlüsselung im Ruhezustand. Ihre Daten befinden sich auf Servern, auf denen die Verschlüsselung auf Datenträgerebene aktiviert ist. 

Da es sich bei {{site.data.keyword.composeForMySQL}} um einen verwalteten Service handelt, sind Operatoren von Compose auf {{site.data.keyword.cloud}} in der Lage, Daten zu sehen. Zusätzlich zur Plattenverschlüsselung wird empfohlen, persönliche Informationen zu verschlüsseln, bevor sie in der Datenbank gespeichert werden, oder Erweiterungen bzw. Features zu verwenden, um die Verschlüsselung auf der Datenbank selbst zu ermöglichen. Obwohl diese Methoden den Bedienungskomfort oder die Leistung beeinträchtigen können, hat es sich bewährt, den Schutz persönlicher Informationen mit Verschlüsselung sicherzustellen.

## Automatische Skalierung

Die Ressourcen werden basierend auf der Gesamtplattenspeicherbelegung der MySQL-Datenbanken automatisch skaliert. Die Hauptspeicherbelegung basiert auf einem Faktor des bereitgestellten Speichers im Verhältnis von 1:10. Diese Ressourcen werden als Einheiten gebündelt.

Die automatische Skalierung ist so konzipiert, dass sie als Reaktion auf die kurz-bis mittelfristigen Trends Ihrer Datenbank erfolgt. Ihr Service wird in stündlichen Intervallen überprüft. Wenn der Plattenspeicherplatz für den Service knapp zu drohen wird, werden der Bereitstellung weitere Einheiten zugeordnet.

Bei der automatischen Skalierung wird kein Scale-down für Bereitstellungen durchgeführt, bei denen sich die Platten-/Speicherbelegung verringert hat. Die für Ihre Datenbanken bereitgestellten Ressourcen bleiben für zukünftige Anforderungen weiterhin bestehen, sofern Sie Ihre Bereitstellung nicht per Scale-down manuell nach unten skalieren.
{: .tip}
