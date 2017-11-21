---

Copyright:
  Years: 2017
lastupdated: "2017-11-20"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Service Overview

The _Overview_ page shows you information about your {{site.data.keyword.cloud}} Compose database. The overview includes essential identifying information and current resource usage. You'll also find a section for connection strings that you can use with tools or make use of tools to connect to your database.

## Deployment Details

The _Deployment Details_ panel shows details of your service.

![Deployment Details](./images/mysql-deployment-details.png "A view of the Deployment Details panel")

### Type

The type of database that is offered by the service, and the database version that your service uses.

### Name

An internal identifier for the service.

### Usage

The size of your database and the amount of storage provided by your service plan.

## Current Jobs

Making administrative changes to your service (such as scaling, or taking a manual backup) starts a job. While a job is running, the _Current Jobs_ panel appears on the _Overview_ page, showing the job name and a progress bar. When the job is complete, the _Current Jobs_ panel no longer appears on the _Overview_ page.

## Connection Strings

Connection Strings can be used by some client libraries and contain all the information needed for other libraries to connect. You can find out how to use a Connection String to connect to your service in [Connecting an external application](./connecting-external.html).

You'll find each Connection String for your service in a different tab in the _Connection Strings_ panel.

### Connection String

The **Connection String** can be used by some client libraries and contains all the information needed for other libraries to connect. You can find out how to use the Connection String to connect in [Connecting an external application](./connecting-external.html).

### Command Line

The **Command Line** is a preformatted command you can use to connect to MySQL. To do so, you have to install MySQL on your local machine. You can find out about how to use it in [Connecting an external application](./connecting-external.html).

### SSL Certificate

Your Compose {{site.data.keyword.cloud_notm}} service provides you with an SSL certificate that you can use to connect to your database.


## Instance Administration API

You can manage your {{site.data.keyword.composeForMySQL}} service through the {{site.data.keyword.cloud_notm}} Compose API.

### Foundation Endpoint

The foundation endpoint is composed of the region the service resides in and the service instance id. It will be at the start of every endpoint.

### Deployment ID

The deployment ID is necessary for most calls, and identifies the specific deployment instance.

### Reference

For more documentation and reference for using the {{site.data.keyword.cloud_notm}} Compose API, across all {{site.data.keyword.cloud_notm}} Compose services, read [The {{site.data.keyword.cloud_notm}} Compose API](https://www.compose.com/articles/the-ibm-cloud-compose-api/).
