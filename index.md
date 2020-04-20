---

copyright:
  years: 2016,2018
lastupdated: "2018-03-26"

keywords: mysql, compose

subcollection: compose-for-mysql

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About {{site.data.keyword.composeForMySQL}}
{: #about}

With a broad subset of ANSI SQL 99 and a wide set of its own extensions, including JSON document, full text search and updatable views, MySQL offers a rich palette for developers to draw on in their applications. Administrators can also find a wide selection of database management tools that can work with MySQL. {{site.data.keyword.composeForMySQL_full}} extends the capabilities of MySQL by managing it for you, offering an easy, auto-scaling deployment system that delivers high availability and redundancy, and automated backups.
{:shortdesc}

## Creating a {{site.data.keyword.composeForMySQL}} service instance

You can create a {{site.data.keyword.composeForMySQL}} service from the [{{site.data.keyword.composeForMySQL}} page](https://{DomainName}/catalog/compose-for-mysql/) in the {{site.data.keyword.cloud_notm}} catalog.

Choose a service name, and a region, organization, and space to provision the service in. You can use the **Select a database version** field to choose from the available database versions.

When you provision your {{site.data.keyword.composeForMySQL}} instance, you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForMySQL}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation that is required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [{{site.data.keyword.composeEnterprise}} documentation](docs/ComposeEnterprise?topic=compose-enterprise-about) for more details.

## Managing {{site.data.keyword.composeForMySQL}}

You can manage your service from the service dashboard. Here you can find information about your {{site.data.keyword.cloud}} Compose database and how to connect to it. You can also:
- Manage your backups
- Allocate more resources for your service
- Change the service password
- Use whitelists to restrict access to your databases. 

For more information, see [Settings](/docs/ComposeForMySQL?topic=compose-for-mysql-dashboard-settings).

{{site.data.keyword.composeForMySQL}} relies on Cloud Foundry roles to manage access to the service. Only users with the Developer role can see or use the service dashboard. For more information on Cloud Foundry roles, see the [Cloud Foundry access](/docs/iam?topic=iam-cfaccess) and the [Managing Cloud Foundry access](/docs/iam?topic=iam-mngcf) pages.
{: tip}

## Connecting to {{site.data.keyword.composeForMySQL}}

You can connect to your service by using the credentials that are created along with the service, or with the connection strings and command line that are provided in the *Overview* tab of your service dashboard.

## Connecting an {{site.data.keyword.cloud_notm}} application to {{site.data.keyword.composeForMySQL}}

To connect an {{site.data.keyword.cloud_notm}} application to your service, use the credentials that are created along with the service. You can find information on how to connect an {{site.data.keyword.cloud_notm}} application to your service in [Connecting an {{site.data.keyword.cloud_notm}} Application](/docs/ComposeForMySQL?topic=compose-for-mysql-ibmcloud-cf-app).

## Connecting to {{site.data.keyword.composeForMySQL}} from outside {{site.data.keyword.cloud_notm}}

If you want to connect to your service from outside {{site.data.keyword.cloud_notm}}, you can use the provided connection strings or command line. You can find information on how to connect in [Connecting an external application](/docs/ComposeForMySQL?topic=compose-for-mysql-external-app).
