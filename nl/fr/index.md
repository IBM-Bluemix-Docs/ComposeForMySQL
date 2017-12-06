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

# Initiation à Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Avec un vaste sous-ensemble ANSI SQL 99 et un large ensemble de ses propres extensions, dont un document JSON, une recherche en texte intégral et des vues qu'il est possible de mettre à jour, MySQL offre une riche palette de fonctions à laquelle les développeurs peuvent faire appel dans leurs applications. Les administrateurs bénéficient aussi d'une grande sélection d'outils de gestion de base de données compatibles avec MySQL. Par le biais d'{{site.data.keyword.composeForMySQL_full}}, MySQL étend ses propres fonctionnalités en les gérant à votre place, vous offrant un système de déploiement à dimensionnement automatique facile à utiliser qui fournit des fonctions de haute disponibilité et de redondance et des sauvegardes automatisées.
{:shortdesc}

## Création d'une instance de service Compose for MySQL

[Créez une instance {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

Quand vous créez une instance du service, choisissez un nom pour votre service et un nom de données d'identification. Laissez le service non lié ; vous pourrez connecter une application à votre service ultérieurement en utilisant les données d'identification fournies lors de la mise à disposition du service.  La section "Données d'identification disponibles" répertorie les différentes valeurs de données d'identification.

Lorsque vous mettez votre instance {{site.data.keyword.composeForMySQL}} à disposition, vous avez le choix entre le plan *Standard* et le plan *Entreprise*. Avec le plan *Entreprise*, vous pouvez mettre votre instance {{site.data.keyword.composeForMySQL}} à disposition dans un cluster {{site.data.keyword.composeEnterprise}} disponible. {{site.data.keyword.composeEnterprise}} fournit la sécurité et l'isolement requis par les normes de conformité des entreprises et utilise un réseau dédié pour garantir les performances des bases de données déployées. Pour plus d'informations, voir la [documentation Compose - Entreprise](../ComposeEnterprise/index.html).

## Gestion de Compose for MySQL

Vous pouvez gérer votre service depuis son tableau de bord. Vous y trouverez des informations concernant la base de données Compose d'{{site.data.keyword.cloud}} et la manière de vous y connecter. Vous pouvez également :
- gérer vos sauvegardes ;
- allouer plus de ressources à votre service ;
- modifier le mot de passe du service ;
- constituer des listes blanches pour limiter l'accès à vos bases de données.
Pour plus d'informations, voir [Paramètres](./dashboard-settings.html).


## Connexion à Compose for MySQL

Vous pouvez vous connecter à votre service avec les données d'identification créées en même temps que le service ou avec les chaînes de connexion et la ligne de commande fournies dans l'onglet *Vue d'ensemble* du tableau de bord de votre service.

## Connexion d'une application {{site.data.keyword.cloud_notm}} à Compose for MySQL

Pour connecter une application {{site.data.keyword.cloud_notm}} à votre service, utilisez les données d'identification créées en même temps que le service. Pour plus d'informations sur la connexion d'une application {{site.data.keyword.cloud_notm}} à votre service, voir [Connexion d'une application {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Connexion à Compose for MySQL depuis l'extérieur d'{{site.data.keyword.cloud_notm}}

Pour vous connecter au service depuis l'extérieur d'{{site.data.keyword.cloud_notm}}, vous pouvez utiliser les chaînes de connexion ou la ligne de commande fournies. Pour plus d'informations sur ce type de connexion, voir [Connexion d'une application externe](./connecting-external.html).
