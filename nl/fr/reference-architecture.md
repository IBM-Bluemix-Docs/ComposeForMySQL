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

# Architecture 
{: #architecture}

## Réplication

Un déploiement {{site.data.keyword.composeForMySQL_full}} commence avec trois noeuds de données dans un cluster, répartis dans les zones de disponibilité d'une région. Les données sont répliquées dans les trois noeuds, de sorte que si l'un des membres de données du cluster n'est plus accessible, le cluster continue à fonctionner normalement. Le cluster est configuré de sorte que si le membre leader du cluster échoue, le membre esclave est promu leader au bout de 60 secondes sans réponse du leader. 

## Chiffrement de disque

Tous les services {{site.data.keyword.composeForMySQL}} disposent du chiffrement au repos. Vos données résident sur des serveurs où le chiffrement au niveau volume est activé. 

Etant donné que {{site.data.keyword.composeForMySQL}} est un service géré, les opérateurs {{site.data.keyword.cloud}} Compose peuvent voir les données. Outre le chiffrement du disque, il est recommandé de chiffrer vos informations personnelles avant de les stocker dans la base de données ou d'utiliser des extensions ou des fonctions permettant d'activer le chiffrement sur la base de données elle-même. Même si ces méthodes risquent d'avoir un impact sur la facilité d'utilisation ou les performances, il est conseillé de s'assurer que les informations personnelles sont protégées par un chiffrement.

## Mise à l'échelle automatique

Les ressources sont automatiquement mises à l'échelle en fonction de l'utilisation totale du stockage sur disque des bases de données MySQL. L'utilisation de la mémoire est basée sur un rapport de stockage mis à disposition de 1 sur 10. Ces ressources sont intégrées en tant qu'unités.

La mise à l'échelle automatique est conçue pour répondre aux tendances à court et moyen termes de votre base de données. Votre service est contrôlé toutes les heures et, s'il est à court d'espace disque, des unités supplémentaires sont attribuées au déploiement.

Une mise à l'échelle automatique ne réduit pas la taille des déploiements où l'utilisation du disque/de la mémoire à diminué. Les ressources mises à disposition de vos bases de données sont conservées pour les besoins ultérieurs ou jusqu'à ce que vous réduisiez manuellement votre déploiement.
{: .tip}
