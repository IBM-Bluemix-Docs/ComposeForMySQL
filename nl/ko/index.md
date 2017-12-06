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

# Compose for MySQL 시작하기
{: #getting-started-with-compose-for-mysql}

ANSI SQL 99의 광범위한 서브세트와 다양한 고유 확장기능 세트(예: JSON 문서, 전체 텍스트 검색 및 업데이트 가능 보기)를 사용하여 MySQL에서는 개발자가 애플리케이션에서 이용할 수 있는 풍부한 팔레트를 제공합니다. 관리자가 MySQL과 함께 작동할 수 있는 다양한 데이터베이스 관리 도구도 찾을 수 있습니다. {{site.data.keyword.composeForMySQL_full}}에서는 MySQL의 기능을 확장하여 ScyllaDB를 관리하고 고가용성 및 중복성 외에도 자동화된 백업을 제공하는 사용하기 쉬운 자동 확장 배치 시스템을 제공합니다.
{:shortdesc}

## Compose for MySQL 서비스 인스턴스 작성

[{{site.data.keyword.composeForMySQL}} 인스턴스를 작성하십시오.](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/)

서비스의 인스턴스를 작성하는 경우 서비스의 이름과 신임 정보 이름을 모두 선택하십시오. 서비스를 바인딩되지 않은 상태로 두십시오. 서비스가 프로비저닝될 때 제공되는 신임 정보를 사용하여 나중에 애플리케이션을 서비스에 연결할 수 있습니다. 다양한 신임 정보 값이 "사용 가능한 신임 정보" 섹션에 나열됩니다.

{{site.data.keyword.composeForMySQL}} 인스턴스를 프로비저닝할 때 *표준* 또는 *엔터프라이즈* 플랜을 선택할 수 있습니다. *엔터프라이즈* 플랜을 사용하면 {{site.data.keyword.composeForMySQL}} 인스턴스를 사용 가능한 {{site.data.keyword.composeEnterprise}} 클러스터에 프로비저닝할 수 있습니다. {{site.data.keyword.composeEnterprise}}는 엔터프라이즈 준수에 필요한 보안 및 격리를 제공하며 전용 네트워킹을 사용하여 배치된 데이터베이스의 성능을 보장합니다. 세부사항은 [Compose Enterprise 문서](../ComposeEnterprise/index.html)를 참조하십시오.

## Compose for MySQL 관리

서비스 대시보드에서 서비스를 관리할 수 있습니다. 여기서 {{site.data.keyword.cloud}} Compose 데이터베이스 및 연결 방법에 대한 정보를 찾을 수 있습니다. 또한 다음을 수행할 수 있습니다.
- 백업 관리
- 서비스에 대한 추가 리소스 할당
- 서비스 비밀번호 변경
- 화이트리스트를 사용하여 데이터베이스에 대한 액세스 제한.
자세한 정보는 [설정](./dashboard-settings.html)을 참조하십시오.


## Compose for MySQL에 연결

서비스와 함께 작성된 신임 정보를 사용하거나 서비스 대시보드의 *개요* 탭에서 제공되는 연결 문자열 및 명령행을 사용하여 서비스에 연결할 수 있습니다.

## {{site.data.keyword.cloud_notm}} 애플리케이션을 Compose for MySQL에 연결

{{site.data.keyword.cloud_notm}} 애플리케이션을 서비스에 연결하려면 서비스와 함께 작성되는 신임 정보를 사용하십시오. [{{site.data.keyword.cloud_notm}} 애플리케이션 연결](./connecting-bluemix-app.html)에서 {{site.data.keyword.cloud_notm}} 애플리케이션을 서비스에 연결하는 방법에 대한 정보를 찾을 수 있습니다.

## {{site.data.keyword.cloud_notm}} 외부에서 Compose for MySQL에 연결

{{site.data.keyword.cloud_notm}} 외부에서 서비스에 연결하려는 경우 제공된 연결 문자열 또는 명령행을 사용할 수 있습니다. [외부 애플리케이션 연결](./connecting-external.html)에서 연결 방법에 대한 정보를 찾을 수 있습니다.
