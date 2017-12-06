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

# 开始使用 Compose for MySQL
{: #getting-started-with-compose-for-mysql}

借助大量 ANSI SQL 99 子集及其自己的广泛扩展集，包括 JSON 文档、全文搜索和可更新视图，MySQL 为开发者提供了内容丰富的选用板，供其在自己的应用程序中使用。此外，还为管理员提供了诸多数据库管理工具，可选择用于处理 MySQL。通过 {{site.data.keyword.composeForMySQL_full}}，MySQL 的功能得到扩展，不仅可以为您管理 MySQL，还提供了易于使用、自动扩展的部署系统，能交付高可用性、冗余性和自动备份功能。
{:shortdesc}

## 创建 Compose for MySQL 服务实例

[创建 {{site.data.keyword.composeForMySQL}} 实例](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/)。

当您创建服务实例时，请选择服务的名称和凭证名称。保持服务处于未绑定状态；您可以稍后使用供应服务时提供的凭证，将应用程序连接到您的服务。“可用凭证”一节列出了各种凭证值。

供应 {{site.data.keyword.composeForMySQL}} 实例时，可以选择*标准*或*企业*套餐。使用*企业*套餐，您可以将 {{site.data.keyword.composeForMySQL}} 实例供应到可用的 {{site.data.keyword.composeEnterprise}} 集群中。{{site.data.keyword.composeEnterprise}} 提供企业合规性所需的安全性和隔离，并使用专用网络来确保已部署的数据库的性能。有关更多详细信息，请参阅 [Compose Enterprise 文档](../ComposeEnterprise/index.html)。

## 管理 Compose for MySQL

您可以从服务仪表板管理服务。您可以在此找到有关 {{site.data.keyword.cloud}} Compose 数据库以及如何连接到该数据库的信息。您还可以：
- 管理备份
- 为服务分配更多资源
- 更改服务密码
- 使用白名单来限制对数据库的访问。
有关更多信息，请参阅[设置](./dashboard-settings.html)。


## 连接到 Compose for MySQL

您可以使用随服务一起创建的凭证，或者使用服务仪表板*概述*选项卡中提供的连接字符串和命令行，来连接到服务。

## 将 {{site.data.keyword.cloud_notm}} 应用程序连接到 Compose for MySQL

要将 {{site.data.keyword.cloud_notm}} 应用程序连接到服务，请使用随服务一起创建的凭证。您可以在[连接 {{site.data.keyword.cloud_notm}} 应用程序](./connecting-bluemix-app.html)中查找有关如何将 {{site.data.keyword.cloud_notm}} 应用程序连接到服务的信息。

## 从外部 {{site.data.keyword.cloud_notm}} 连接到 Compose for MySQL

如果要从外部 {{site.data.keyword.cloud_notm}} 连接到服务，可以使用提供的连接字符串或命令行。您可以在[连接外部应用程序](./connecting-external.html)中找到有关如何连接的信息。
