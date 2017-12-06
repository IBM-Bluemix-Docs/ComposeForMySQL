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

# Compose for MySQL の概説
{: #getting-started-with-compose-for-mysql}

ANSI SQL 99 の広範囲なサブセット、および JSON ドキュメント、全文検索、更新可能なビューなどの独自の幅広い拡張機能セットによって、
MySQL は開発者がアプリケーションに構想を描くための便利なパレットを提供します。
また管理者は、MySQL で使用できるデータベース管理ツールを幅広い選択肢の中から見つけることもできます。
{{site.data.keyword.composeForMySQL_full}} は、MySQL をユーザーの代わりに管理して、MySQL の機能を拡張することにより、
高可用性、冗長度、自動バックアップを備えた、使いやすい自動スケーリング・デプロイメント・システムを提供します。
{:shortdesc}

## Compose for MySQL サービス・インスタンスの作成

[{{site.data.keyword.composeForMySQL}} インスタンスを作成します](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/)。

サービスのインスタンスを作成するときは、サービスの名前と資格情報名の両方を選択します。サービスをバインドしないでおきます。サービスをプロビジョンするときに指定される資格情報を使用して、アプリケーションをサービスに接続できます。「使用可能な資格情報」セクションには、各種の資格情報値がリストされています。

{{site.data.keyword.composeForMySQL}} インスタンスのプロビジョンでは、*標準*プランと*エンタープライズ*・プランのどちらかを選択できます。*エンタープライズ*・プランの場合は、{{site.data.keyword.composeForMySQL}} インスタンスを使用可能な {{site.data.keyword.composeEnterprise}} クラスターにプロビジョンできます。{{site.data.keyword.composeEnterprise}} は、企業コンプライアンスで要求されるセキュリティーと分離を提供し、専用ネットワーキングを使用してデプロイ済みデータベースのパフォーマンスを確保します。詳しくは、[Compose Enterprise 文書](../ComposeEnterprise/index.html)を参照してください。

## Compose for MySQL の管理

サービス・ダッシュボードからサービスを管理できます。ダッシュボードには {{site.data.keyword.cloud}} Compose データベースとそれへの接続方法に関する情報が示されます。また、以下の操作を行うこともできます。
- バックアップを管理する
- サービスに割り振るリソースを増やす
- サービス・パスワードを変更する
- ホワイトリストを使用してデータベースへのアクセスを制限する
詳しくは、[設定](./dashboard-settings.html)を参照してください。


## Compose for MySQL への接続

サービスに接続するには、サービスと一緒に作成された資格情報を使用するか、サービス・ダッシュボードの*「概要」*タブに表示される接続ストリングとコマンド・ラインを使用します。

## {{site.data.keyword.cloud_notm}} アプリケーションを Compose for MySQL に接続する場合

{{site.data.keyword.cloud_notm}} アプリケーションをサービスに接続するには、サービスと一緒に作成された資格情報を使用します。{{site.data.keyword.cloud_notm}} アプリケーションをサービスに接続する方法については、[{{site.data.keyword.cloud_notm}} アプリケーションの接続](./connecting-bluemix-app.html)を参照してください。

## {{site.data.keyword.cloud_notm}} の外部から Compose for MySQL に接続する場合

{{site.data.keyword.cloud_notm}} の外部からサービスに接続する場合は、用意されている接続ストリングやコマンド・ラインを使用できます。接続方法については、[外部アプリケーションの接続](./connecting-external.html)を参照してください。
