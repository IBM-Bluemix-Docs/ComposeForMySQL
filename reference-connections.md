---
copyright:
  years: 2016,2018
lastupdated: "2018-06-11"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Connection Configuration
{: #connection-configuration}

{{site.data.keyword.composeForMySQL_full}} database connections are managed by 2 HAProxy portals. Each portal has 64MB of memory.

The two portals to allow for applications to maintain connectivity should one of the portals become unreachable. Failover at the client side is the responsibility of the application designer. Some MySQL drivers handle multiple connection strings and graceful failover automatically. Unless working with a driver which completely handles failover errors you should:

* Work with a driver that accepts multiple endpoints in its connection configuration.
* Ensure your applications calls to read or write to the database react to errors appropriately. Options include:
  + Logging the error and reconnecting.
  + Reconnecting and retrying the operation which caused the error.
  + Queuing the failed operation and scheduling reconnection.

## Encryption in Transit

All {{site.data.keyword.composeForMySQL}} HAProxy portals have TLS/SSL enabled and support TLS version 1.2. The certificates for the service are self-signed certificates. You may have to save a local copy of the certifcate for your serivce and provide it's location to your applications driver in order to make a secure connection.

## Connection Limits

Database connections have a connection limit of 95 connections per portal, with a maximum limit of 151 connections for the service.  Exceeding the connection limit will make your service unresponsive. You can manage connections from your application through your driver's connection pooling feature.

## Proxy Timeouts

The HAProxy portals manage the life cycle of connections between the server and client. We detail them here as a reference for driver writers and others who have an interest in the low-level activity of {{site.data.keyword.composeForMySQL}} database connections.

Setting | Value | Applies
----------|-----------|-----------
client | 1 day | When the client is expect to acknowledge or send data.
connect | 4s | When a connection is being made between the proxy and the server.
server | 30m | When the server is expected to acknowledge or send data.
tunnel | 1 day | When a bidirectional connection is established between a client and a server, and the connection remains inactive in both directions.
client-fin | 5m | When the client is expected to acknowledge or send data while one direction is already shut down.
check | 5s | As a secondary timeout check when a connection is being made between the proxy and the server.
{: caption="Table 1. MySQL HAProxy timeouts" caption-side="top"}
