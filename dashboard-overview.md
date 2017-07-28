---

Copyright:
  Years: 2017
lastupdated: "2017-07-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Dashboard Overview

The service dashboard overview shows you information about your Bluemix Compose database. The overview includes essential identifying information and current resource usage. You'll also find a section for Connection Strings that you can use with tools or make use of tools to connect to your database.

## Deployment Details

The Deployment Details panel shows details of your service.

### Database

The type of database that is offered by the service; in this case `mysql`.

### Usage

Shows the size of your database and the amount of storage provided by your service plan.

## Connecting

There are two ways of connecting an external application to your database. You can either connect using a **Connection String** or with a **Command Line**. Both are provided on your service dashboard overview.

### Connection String

The **Connection String** can be used by some client libraries and contains all the information needed for other libraries to connect. You can find out how to use the Connection String to connect in [Connecting an external application](./connecting-external.html).

### Command Line

The **Command Line** is a preformatted command you can use to connect to MySQL. To do so, you have to install MySQL on your local machine. You can find out about how to use it in [Connecting an external application](./connecting-external.html).

### SSL Certificate

Your Compose Bluemix service provides you with an SSL certificate that you can use to connect to your database.