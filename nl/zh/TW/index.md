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

# 關於 {{site.data.keyword.composeForMySQL}}
{: #about-compose-for-mysql}

MySQL 具有廣泛的 ANSI SQL 99 子集和其自己的延伸集，包括 JSON 文件、全文檢索和可更新的視圖，並且提供豐富的選用區讓開發人員能在應用程式裡利用。管理者也可以找到廣泛的資料庫管理工具，可以搭配 MySQL 使用。{{site.data.keyword.composeForMySQL_full}} 延伸了 MySQL 的功能，因為它能替您管理、提供容易、自動擴充的部署系統，此系統能提供高可用性與備援，以及自動化備份。
{:shortdesc}

## 建立 {{site.data.keyword.composeForMySQL}} 服務實例

您可以從 {{site.data.keyword.cloud_notm}} 型錄中的 [{{site.data.keyword.composeForMySQL}} 頁面](https://console.{DomainName}/catalog/services/compose-for-mysql/)建立 {{site.data.keyword.composeForMySQL}} 服務。

選擇服務名稱、地區、組織，以及要在其中佈建服務的空間。您可以使用**選取資料庫版本**欄位，從可用的資料庫版本中進行選擇。

當您佈建 {{site.data.keyword.composeForMySQL}} 實例時，可以選擇*標準* 或*企業* 方案。使用*企業* 方案，您可以將 {{site.data.keyword.composeForMySQL}} 實例佈建到可用的 {{site.data.keyword.composeEnterprise}} 叢集。{{site.data.keyword.composeEnterprise}} 提供企業相符性所需的安全和隔離，並使用專用網路來確保已部署之資料庫的效能。如需詳細資料，請參閱 [Compose Enterprise 文件](../ComposeEnterprise/index.html)。

## 管理 {{site.data.keyword.composeForMySQL}}

您可以從服務儀表板來管理服務。在這裡，您可以找到 {{site.data.keyword.cloud}} Compose 資料庫的相關資訊，以及連接方式。您也可以：
- 管理備份
- 為您的服務配置更多資源
- 變更服務密碼
- 使用白名單來限制對資料庫的存取權。 

如需相關資訊，請參閱[設定](./dashboard-settings.html)。

{{site.data.keyword.composeForMySQL}} 根據 Cloud Foundry 角色來管理對服務的存取。只有具有「開發人員」角色的使用者才能看到或使用服務儀表板。如需 Cloud Foundry 角色的相關資訊，請參閱 [Cloud Foundry 存取](https://console.bluemix.net/docs/iam/cfaccess.html#cfaccess)及[管理 Cloud Foundry 存取](https://console.bluemix.net/docs/iam/mngcf.html#mngcf)頁面。
{: .tip}

## 連接至 {{site.data.keyword.composeForMySQL}}

您可以使用與服務一起建立的認證，或使用服務儀表板的*概觀* 標籤中所提供的連線字串及指令行，來連接至服務。

## 將 {{site.data.keyword.cloud_notm}} 應用程式連接至 {{site.data.keyword.composeForMySQL}}

若要將 {{site.data.keyword.cloud_notm}} 應用程式連接至服務，請使用與服務一起建立的認證。您可以在[連接 {{site.data.keyword.cloud_notm}} 應用程式](./connecting-bluemix-app.html)中，找到如何將 {{site.data.keyword.cloud_notm}} 應用程式連接至服務的資訊。

## 從 {{site.data.keyword.cloud_notm}} 之外連接至 {{site.data.keyword.composeForMySQL}}

如果您想要從 {{site.data.keyword.cloud_notm}} 之外連接至服務，則可以使用所提供的連線字串或指令行。您可以在[連接外部應用程式](./connecting-external.html)中，找到如何連接的相關資訊。
