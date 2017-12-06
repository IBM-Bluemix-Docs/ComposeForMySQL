---

Copyright:
  Years: 2016,2017
lastupdated: "2017-10-23"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao Compose for MySQL
{: #getting-started-with-compose-for-mysql}

Com um subconjunto amplo de ANSI SQL 99 e um vasto conjunto de suas próprias extensões, incluindo o documento JSON, a procura de texto completa e as visualizações atualizáveis, o MySQL oferece uma paleta rica para desenvolvedores usarem em seus aplicativos. Os administradores também podem localizar uma ampla seleção de ferramentas de gerenciamento de banco de dados que podem funcionar com o MySQL. O {{site.data.keyword.composeForMySQL_full}} faz o MySQL ampliar os recursos de MySQL, gerenciando-o para você, oferecendo um sistema de implementação fácil e de escala automática que oferece alta
disponibilidade e redundância, além de backups automatizados.
{:shortdesc}

## Criando uma instância de serviço do Compose for MySQL

[Crie uma instância do {{site.data.keyword.composeForMySQL}}](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

Ao criar uma instância do serviço, escolha um nome para seu serviço e um nome de credencial. Deixe o serviço desvinculado; é possível conectar um
aplicativo ao seu serviço mais tarde usando as credenciais que são fornecidas quando o
serviço é provisionado.  Os vários valores de credencial são listados na seção "Credenciais disponíveis".

Quando você provisiona sua instância do {{site.data.keyword.composeForMySQL}}, é possível escolher os planos *Padrão* ou *Corporativo*. Com o plano *Corporativo*, é possível provisionar sua instância do {{site.data.keyword.composeForMySQL}} em um cluster disponível do {{site.data.keyword.composeEnterprise}}. O {{site.data.keyword.composeEnterprise}} fornece a segurança e o isolamento requeridos pela conformidade corporativa e usa rede dedicada para assegurar o desempenho dos bancos de dados implementados. Veja a [Documentação do Compose Enterprise](../ComposeEnterprise/index.html) para obter mais detalhes.

## Gerenciando o Compose for MySQL

É possível gerenciar seu serviço no painel de serviço. Aqui é possível localizar informações sobre o banco de dados do {{site.data.keyword.cloud}} Compose e como conectar-se a ele. Também é possível:
- gerenciar seus backups
- alocar mais recursos para seu serviço
- mudar a senha do serviço
- use listas de desbloqueio para restringir o acesso a seus bancos de dados. 
Para obter mais informações, veja [Configurações](./dashboard-settings.html).


## Conectando-se ao Compose for MySQL

É possível se conectar a seu serviço usando as credenciais que são criadas junto com o serviço ou com as sequências de conexões e linha de comandos que são fornecidas na guia *Visão geral* de seu painel de serviço.

## Conectando um aplicativo {{site.data.keyword.cloud_notm}} ao Compose for MySQL

Para conectar um aplicativo {{site.data.keyword.cloud_notm}} a seu serviço, use as credenciais que são criadas com o serviço. É possível localizar informações sobre como conectar um aplicativo {{site.data.keyword.cloud_notm}} ao seu serviço em [Conectando um aplicativo {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Conectando-se ao Compose for MySQL de fora do {{site.data.keyword.cloud_notm}}

Se você deseja se conectar a seu serviço do {{site.data.keyword.cloud_notm}} externo, é possível usar as sequências de conexões fornecidas ou a linha de comandos. É possível localizar informações sobre como conectar-se em [Conectando um aplicativo externo](./connecting-external.html).
