---

copyright:
  years: 2016,2017
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Compose for MySQL
{: #getting-started-with-compose-for-mysql}

With a broad subset of ANSI SQL 99 and a wide set of its own extensions, including JSON document, full text search and updatable views, MySQL offers a rich palette for developers to draw on in their applications. Administrators can also find a wide selection of database management tools that can work with MySQL. {{site.data.keyword.composeForMySQL_full}} makes MySQL extends the capabilities of MySQL by managing it for you, offering an easy, auto-scaling deployment system that delivers high availability and redundancy, and automated backups.
{:shortdesc}

**Note:** {{site.data.keyword.composeForMySQL_full}} does not give access to the Compose UI. See [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) for more details.

## Creating a Compose for MySQL service instance

[Create a {{site.data.keyword.composeForMySQL}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

When you create an instance of the service, choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned.  The various credential values are listed in the "Available credentials" section.

When you provision your {{site.data.keyword.composeForMySQL}} instance you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForMySQL}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [Compose Enterprise documentation](../ComposeEnterprise/index.html) for more details.

## Managing Compose for MySQL

You can manage your service from the service dashboard. Here you can find information about your Bluemix Compose database and how to connect to it. You can also manage your backups from the dashboard and allocated more resources for your service. For more information, see [Service Overview](./dashboard-overview.html), [Backups](./dashboard-backups.html), and [Scaling Resources](./dashboard-scaling-resources.html).

## Connecting to Compose for MySQL

You can connect to your service using the credentials that are created along with the service, or with the connection strings and command line that are provided in the *Overview* tab of your service dashboard.

## Connecting a Bluemix application to Compose for MySQL

To connect a Bluemix application to your service, use the credentials that are created along with the service. You can find information on how to connect a Bluemix application to your service in [Connecting a Bluemix Application](./connecting-bluemix-app.html).

## Connecting to Compose for MySQL from outside Bluemix

If you want to connect to your service from outside Bluemix, you can use the provided connection strings or command line. You can find information on how to connect in [Connecting an external application](./connecting-external.html).