---

copyright:
  years: 2016,2017
lastupdated: "2017-06-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 連接 {{site.data.keyword.cloud_notm}} 應用程式

若要將 {{site.data.keyword.cloud}} 應用程式連接至您的服務，請使用您在佈建服務時所建立的服務認證。範例應用程式會示範如何使用 Node.js，利用所提供的認證進行連接，以及如何建立資料庫，然後從資料庫中讀取及寫入資料庫。

## 使用 'Hello World' 範例應用程式來連接

[compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) 範例應用程式會示範如何使用 Node.js，利用所提供的認證來連接至您的服務。應用程式會建立、讀取及寫入資料庫。

請下載範例應用程式，並遵循 Readme 檔中的指示。然後，在 {{site.data.keyword.cloud_notm}} 的應用程式詳細資料頁面中，按一下**檢視應用程式**來檢視*範例* 表格的內容。

## 可用的認證

欄位名稱|說明
----------|-----------
`db_type`|服務所提供的資料庫類型。在此情況下，為 `mysql`。
`name`|資料庫部署名稱。
`uri_cli`|連接至資料庫實例的 `mysql` Shell 指令行。
`ca_certificate_base64`|用來確認應用程式將連接至適當伺服器的自簽憑證。憑證是以 base64 的方式編碼。
`deployment_id`|Compose 內所建立之服務的內部 ID。
`uri`|連接至服務時使用的 URI，包括綱目 (`mysql:`)、管理使用者名稱和密碼、伺服器的主機名稱、要連接至的埠號，以及 vhost 名稱。
{: caption="表 1. Compose for MySQL 認證" caption-side="top"}
