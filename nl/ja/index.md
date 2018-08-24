---

copyright:
  years: 2016,2018
lastupdated: "2018-03-26"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.composeForMySQL}} の概要
{: #about-compose-for-mysql}

ANSI SQL 99 の広範囲なサブセット、および JSON ドキュメント、全文検索、更新可能なビューなどの独自の幅広い拡張機能セットによって、
MySQL は開発者がアプリケーションに構想を描くための便利なパレットを提供します。 また管理者は、MySQL で使用できるデータベース管理ツールを幅広い選択肢の中から見つけることもできます。 {{site.data.keyword.composeForMySQL_full}} は、自動管理機能によって MySQL を拡張し、高可用性、冗長性、自動バックアップ機能を備えた使いやすい自動スケーリング・デプロイメント・システムを提供します。
{:shortdesc}

## {{site.data.keyword.composeForMySQL}} サービス・インスタンスの作成

{{site.data.keyword.composeForMySQL}} サービスは、{{site.data.keyword.cloud_notm}} カタログの [{{site.data.keyword.composeForMySQL}} ページ](https://console.{DomainName}/catalog/services/compose-for-mysql/)から作成できます。

サービス名、およびサービスをプロビジョンする地域、組織、スペースを選択します。 **「データベースのバージョンの選択 (Select a database version)」**フィールドを使用して、データベースの使用できるバージョンを選択できます。

{{site.data.keyword.composeForMySQL}} インスタンスのプロビジョンでは、*標準*プランと*エンタープライズ*・プランのどちらかを選択できます。 *エンタープライズ*・プランの場合は、{{site.data.keyword.composeForMySQL}} インスタンスを使用可能な {{site.data.keyword.composeEnterprise}} クラスターにプロビジョンできます。 {{site.data.keyword.composeEnterprise}} は、企業コンプライアンスで要求されるセキュリティーと分離を提供し、専用ネットワーキングを使用してデプロイ済みデータベースのパフォーマンスを確保します。 詳しくは、[{{site.data.keyword.composeEnterprise}} 文書](/docs/services/ComposeEnterprise/index.html)を参照してください。

## {{site.data.keyword.composeForMySQL}} の管理

サービス・ダッシュボードからサービスを管理できます。 ダッシュボードには {{site.data.keyword.cloud}} Compose データベースとそれへの接続方法に関する情報が示されます。 また、以下の操作を行うこともできます。
- バックアップを管理する
- サービスに割り振るリソースを増やす
- サービス・パスワードを変更する
- ホワイトリストを使用してデータベースへのアクセスを制限する。 

詳しくは、[設定](./dashboard-settings.html)を参照してください。

{{site.data.keyword.composeForMySQL}} は、Cloud Foundry の役割を利用して、サービスへのアクセスを管理します。 開発者役割を持つユーザーのみが、サービス・ダッシュボードを表示または使用できます。 Cloud Foundry の役割について詳しくは、『[Cloud Foundry アクセス権限](https://console.{DomainName}/docs/iam/cfaccess.html#cfaccess)』および 『[Cloud Foundry のアクセス権限の管理](https://console.{DomainName}/docs/iam/mngcf.html#mngcf)』のページを参照してください。
{: .tip}

## {{site.data.keyword.composeForMySQL}} への接続

サービスに接続するには、サービスと一緒に作成された資格情報を使用するか、サービス・ダッシュボードの*「概要」*タブに表示される接続ストリングとコマンド・ラインを使用します。

## {{site.data.keyword.composeForMySQL}} への {{site.data.keyword.cloud_notm}} アプリケーションの接続

{{site.data.keyword.cloud_notm}} アプリケーションをサービスに接続するには、サービスと一緒に作成された資格情報を使用します。 {{site.data.keyword.cloud_notm}} アプリケーションをサービスに接続する方法については、[{{site.data.keyword.cloud_notm}} アプリケーションの接続](./connecting-bluemix-app.html)を参照してください。

## {{site.data.keyword.cloud_notm}} 外からの {{site.data.keyword.composeForMySQL}} への接続

{{site.data.keyword.cloud_notm}} の外部からサービスに接続する場合は、用意されている接続ストリングやコマンド・ラインを使用できます。 接続方法については、[外部アプリケーションの接続](./connecting-external.html)を参照してください。
