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

# {{site.data.keyword.cloud_notm}}-Anwendung verbinden

Verbinden Sie eine {{site.data.keyword.cloud}}-Anwendung mit Ihrem Service mithilfe der Berechtigungsnachweise dieses Service, die bei dessen Bereitstellung erstellt werden. Die Beispielapp veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mithilfe der bereitgestellten Berechtigungsnachweise und die Vorgehensweise zur Erstellung einer Datenbank sowie Lese- und Schreibvorgänge in dieser Datenbank.

## Verbindung mithilfe der Beispielapp 'Hello World' herstellen

Die Beispielapp [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) veranschaulicht die Verwendung von Node.js zur Herstellung einer Verbindung mit Ihrem Service mithilfe der bereitgestellten Berechtigungsnachweise. Die Anwendung erstellt eine Datenbank, liest daraus und schreibt darin.

Laden Sie die Beispielapp herunter und befolgen Sie die Anweisungen in der Readme-Datei. Anschließend klicken Sie auf der Detailseite für die Anwendung in {{site.data.keyword.cloud_notm}} auf **App anzeigen**, um den Inhalt der Tabelle *examples* anzuzeigen.

## Verfügbare Berechtigungsnachweise

Feldname|Beschreibung
----------|-----------
`db_type`|Der Datenbanktyp, der vom Service angeboten wird, in diesem Fall `mysql`.
`name`|Der Name der Datenbankimplementierung.
`uri_cli`|Eine `mysql`-Shellbefehlszeile, die eine Verbindung zur Datenbankinstanz herstellt.
`ca_certificate_base64`|Ein selbst signiertes Zertifikat, mit dem bestätigt wird, dass eine Anwendung eine Verbindung zum geeigneten Server herstellt. Das Zertifikat ist base64-codiert.
`deployment_id`|Eine interne ID für den Service entsprechend der Erstellung in Compose.
`uri`|Der bei der Herstellung einer Verbindung zum Service verwendete URI, der Folgendes enthält: Schema (`mysql:`), Benutzername und Kennwort des Administrators, Hostname des Servers sowie die Nummer des Ports, zu dem die Verbindung hergestellt werden soll, und der vhost-Name.
{: caption="Tabelle 1. Compose for MySQL - Berechtigungsnachweise" caption-side="top"}
