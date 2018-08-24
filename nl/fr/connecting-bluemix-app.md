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

# Connexion d'une application {{site.data.keyword.cloud_notm}}

Pour connecter une application {{site.data.keyword.cloud}} à votre service, utilisez les données d'identification créées lors de la mise à disposition du service. Le modèle d'application montre comment utiliser Node.js pour établir une connexion à l'aide des données d'identification fournies et comment créer une base de données, lire dans cette base de données et y écrire.

## Connexion à l'aide du modèle d'application 'Hello World'

Le modèle d'application [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) montre comment utiliser Node.js pour établir une connexion à votre service à l'aide des données d'identification fournies. L'application crée une base de données, y lit et y écrit

Téléchargez le modèle d'application et suivez les instructions contenues dans le fichier Readme. Ensuite, sur la page des détails d'application d'{{site.data.keyword.cloud_notm}}, cliquez sur **Afficher l'application** pour afficher le contenu du tableau *Exemples*.

## Données d'identification disponibles

Nom de zone|Description
----------|-----------
`db_type`|Type de base de données fourni par le service, `mysql`, dans ce cas.
`name`|Nom du déploiement de base de données.
`uri_cli`|Ligne de commande shell `mysql` qui permet d'établir la connexion à l'instance de base de données.
`ca_certificate_base64`|Certificat autosigné utilisé pour confirmer qu'une application se connecte au serveur approprié. Le certificat est codé en base64.
`deployment_id`|Identificateur interne du service, créé dans Compose.
`uri`|Identificateur URI qui est utilisé pour la connexion au service et
qui comprend le schéma (`mysql:`), le nom et le mot de passe de
l'administrateur, le nom d'hôte du serveur, le numéro de port auquel se connecter et le nom vhost.
`uri_direct_1`|Second identificateur URI qui peut être utilisé lors de la connexion au service. Utilise le même format qu'`uri`.
`uri_cli_1`|Seconde ligne de commande shell `mysql` qui permet d'établir la connexion à l'instance de base de données.
{: caption="Tableau 1. Données d'identification Compose for MySQL" caption-side="top"}

**Remarque :** deux portails `haproxy` permettent d'accéder au service MySQL. Les zones `uri` et `uri_direct_1` peuvent toutes deux être utilisées pour établir la connexion. Dans vos applications, utilisez `uri` ou `uri_direct_1` pour gérer les réponses aux pannes de connexion.
