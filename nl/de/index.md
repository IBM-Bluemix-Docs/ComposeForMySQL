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

# Informationen zu {{site.data.keyword.composeForMySQL}}
{: #about-compose-for-mysql}

Mit einem umfassenden ANSI SQL 99-Subset und einem umfangreichen Subset an eigenen Erweiterungen wie JSON-Dokument, Volltextsuche und aktualisierbaren Ansichten, bietet MySQL Anwendungsentwicklern eine breite Palette zur Nutzung ihrer Anwendungen. Administratoren steht außerdem eine breite Auswahl an Datenbank-Management-Tools zur Verfügung, die mit MySQL funktionieren. {{site.data.keyword.composeForMySQL_full}} erweitert die Funktionen von MySQL dahingehend, dass die Verwaltung für Sie übernommen wird und Sie ein einfaches Bereitstellungssystem zur automatischen Skalierung für eine hohe Verfügbarkeit und Redundanz sowie automatisierte Backups angeboten bekommen.
{:shortdesc}

## {{site.data.keyword.composeForMySQL}}-Serviceinstanz erstellen

Sie können einen {{site.data.keyword.composeForMySQL}}-Service über die [{{site.data.keyword.composeForMySQL}}-Seite](https://console.{DomainName}/catalog/services/compose-for-mysql/) im {{site.data.keyword.cloud_notm}}-Katalog erstellen.

Wählen Sie einen Servicenamen und eine Region, eine Organisation und einen Bereich zur Bereitstellung des Service aus. Im Feld **Datenbankversion auswählen** können Sie eine der verfügbaren Datenbankversionen auswählen.

Bei der Bereitstellung Ihrer {{site.data.keyword.composeForMySQL}}-Instanz können Sie den Plan *Standard* oder *Enterprise* auswählen. Mit dem Plan *Enterprise* können Sie Ihre {{site.data.keyword.composeForMySQL}}-Instanz in einem {{site.data.keyword.composeEnterprise}}-Cluster bereitstellen. {{site.data.keyword.composeEnterprise}} stellt die für die Konformität mit Enterprise erforderliche Sicherheit und Isolation bereit und stellt mithilfe eines dedizierten Netzbetriebs die Leistung der bereitgestellten Datenbanken sicher. Weitere Details finden Sie in der Dokumentation zu [{{site.data.keyword.composeEnterprise}}](/docs/services/ComposeEnterprise/index.html).

## {{site.data.keyword.composeForMySQL}} verwalten

Sie können Ihren Service über das Service-Dashboard verwalten. Hier finden Sie Informationen zu Ihrer {{site.data.keyword.cloud}} Compose-Datenbank und dazu, wie Sie eine Verbindung zu ihr herstellen. Außerdem können Sie:
- Ihre Sicherungen verwalten
- Ihrem Service mehr Ressourcen zuordnen
- Das Servicekennwort ändern
- Whitelists verwenden, um den Zugriff auf Ihre Datenbank zu beschränken. 

Weitere Informationen finden Sie im Abschnitt [Einstellungen](./dashboard-settings.html).

{{site.data.keyword.composeForMySQL}} nutzt Cloud Foundry-Rollen, um den Zugriff auf den Service zu verwalten. Nur Benutzer mit der Entwicklerrolle können das Service-Dashboard anzeigen oder verwenden. Weitere Informationen zu Cloud Foundry-Rollen finden Sie auf den Seiten [Cloud Foundry-Zugriff](https://console.{DomainName}/docs/iam/cfaccess.html#cfaccess) und [Cloud Foundry-Zugriff](https://console.{DomainName}/docs/iam/mngcf.html#mngcf) verwalten.
{: .tip}

## Verbindung zu {{site.data.keyword.composeForMySQL}} herstellen

Sie können mit den Berechtigungsnachweisen, die zusammen mit Ihrem Service erstellt werden, oder mithilfe der Verbindungszeichenfolgen und der Befehlszeile, die auf der Registerkarte *Übersicht* Ihres Service-Dashboards bereitgestellt werden, eine Verbindung zu dem Service herstellen.

## Verbindung von einer {{site.data.keyword.cloud_notm}}-Anwendung zu {{site.data.keyword.composeForMySQL}} herstellen

Um eine {{site.data.keyword.cloud_notm}}-Anwendung mit Ihrem Service zu verbinden, verwenden Sie die Berechtigungsnachweise, die zusammen mit dem Service erstellt wurden. Informationen zum Herstellen einer Verbindung von einer {{site.data.keyword.cloud_notm}}-Anwendung zu Ihrem Service finden Sie im Abschnitt [{{site.data.keyword.cloud_notm}}-Anwendung verbinden](./connecting-bluemix-app.html).

## Verbindung zu {{site.data.keyword.composeForMySQL}} außerhalb von {{site.data.keyword.cloud_notm}} herstellen

Wenn Sie außerhalb von {{site.data.keyword.cloud_notm}} eine Verbindung zu Ihrem Service herstellen wollen, können Sie dazu die bereitgestellten Verbindungszeichenfolgen oder die Befehlszeile verwenden. Informationen dazu, wie sich eine Verbindung herstellen lässt, finden Sie im Abschnitt [Externe Anwendung verbinden](./connecting-external.html).
