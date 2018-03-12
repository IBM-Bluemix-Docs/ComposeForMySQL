---

copyright:
  years: 2016,2018
lastupdated: "2017-10-23"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre o {{site.data.keyword.composeForMySQL}}
{: #about-compose-for-mysql}

Com um subconjunto amplo de ANSI SQL 99 e um vasto conjunto de suas próprias extensões, incluindo o documento JSON, a procura de texto completa e as visualizações atualizáveis, o MySQL oferece uma paleta rica para desenvolvedores usarem em seus aplicativos. Os administradores também podem localizar uma ampla seleção de ferramentas de gerenciamento de banco de dados que podem funcionar com o MySQL. O {{site.data.keyword.composeForMySQL_full}} amplia os recursos de MySQL ao gerenciá-lo para você, oferecendo um sistema de implementação fácil de auto-scaling, que entrega alta disponibilidade e redundância, além de backups automatizados.
{:shortdesc}

## Criando uma instância de serviço do {{site.data.keyword.composeForMySQL}}

É possível criar um serviço do {{site.data.keyword.composeForMySQL}} por meio da página [{{site.data.keyword.composeForMySQL}}](https://console.{DomainName}/catalog/services/compose-for-mysql/) no catálogo do {{site.data.keyword.cloud_notm}}.

Escolha um nome do serviço e uma região, organização e espaço no qual provisionar o serviço. É possível usar o campo **Selecionar uma versão do banco de dados** para escolher nas versões do banco de dados disponíveis.

Quando você provisiona sua instância do {{site.data.keyword.composeForMySQL}}, é possível escolher os planos *Padrão* ou *Corporativo*. Com o plano *Corporativo*, é possível provisionar sua instância do {{site.data.keyword.composeForMySQL}} em um cluster disponível do {{site.data.keyword.composeEnterprise}}. O {{site.data.keyword.composeEnterprise}} fornece a segurança e o isolamento requeridos pela conformidade corporativa e usa rede dedicada para assegurar o desempenho dos bancos de dados implementados. Veja a [Documentação do Compose Enterprise](../ComposeEnterprise/index.html) para obter mais detalhes.

## Gerenciando {{site.data.keyword.composeForMySQL}}

É possível gerenciar seu serviço no painel de serviço. Aqui é possível localizar informações sobre o banco de dados do Compose do {{site.data.keyword.cloud}} e como conectar-se a ele. Também é possível:
- gerenciar seus backups
- alocar mais recursos para seu serviço
- mudar a senha do serviço
- use listas de desbloqueio para restringir o acesso a seus bancos de dados. 
Para obter mais informações, veja [Configurações](./dashboard-settings.html).


## Conectando-se ao {{site.data.keyword.composeForMySQL}}

É possível se conectar a seu serviço usando as credenciais que são criadas junto com o serviço ou com as sequências de conexões e linha de comandos que são fornecidas na guia *Visão geral* de seu painel de serviço.

## Conectando um aplicativo {{site.data.keyword.cloud_notm}} ao {{site.data.keyword.composeForMySQL}}

Para conectar um aplicativo {{site.data.keyword.cloud_notm}} a seu serviço, use as credenciais que são criadas com o serviço. É possível localizar informações sobre como conectar um aplicativo {{site.data.keyword.cloud_notm}} ao seu serviço em [Conectando um aplicativo {{site.data.keyword.cloud_notm}}](./connecting-bluemix-app.html).

## Conectando-se ao {{site.data.keyword.composeForMySQL}} de fora do {{site.data.keyword.cloud_notm}}

Se você deseja se conectar a seu serviço do {{site.data.keyword.cloud_notm}} externo, é possível usar as sequências de conexões fornecidas ou a linha de comandos. É possível localizar informações sobre como conectar-se em [Conectando um aplicativo externo](./connecting-external.html).
