---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Arquitetura 
{: #architecture}

## Replicação

Uma implementação do {{site.data.keyword.composeForMySQL_full}} inicia com três nós de dados em um cluster, distribuídos pelas zonas de disponibilidade da região. Os dados são replicados nos três nós. Se um membro de dados no cluster se tornar inacessível, seu cluster continuará a operar normalmente. O cluster será configurado para que, se o membro líder no cluster falhar, o escravo atual seja promovido a líder no prazo de 60 segundos depois de o líder se tornar não responsivo. 

## Criptografia de Disco

Todos os serviços do {{site.data.keyword.composeForMySQL}} têm criptografia em repouso. Seus dados residem em servidores que possuem criptografia em nível de volume ativada. 

Como o {{site.data.keyword.composeForMySQL}} é um serviço gerenciado, é possível que os operadores do {{site.data.keyword.cloud}} Compose vejam dados. Além da criptografia de disco, recomendamos criptografar informações pessoais antes de armazená-las no banco de dados ou usar extensões ou recursos para ativar a criptografia no próprio banco de dados. Embora esses métodos possam afetar a usabilidade ou o desempenho, é uma boa prática assegurar-se de que as informações pessoais sejam protegidas com criptografia.

## Auto-scaling

Os recursos são escalados automaticamente com base no uso total de armazenamento em disco dos bancos de dados MySQL. O uso de memória baseia-se em uma razão de armazenamento provisionado em uma proporção de 1:10. Esses recursos são empacotados como unidades.

O Auto-scaling foi projetado para responder às tendências de curto a médio prazo de seu banco de dados. A cada hora, seu serviço é verificado e, se ele estiver sendo executado com pouco espaço em disco, mais unidades serão alocadas para a implementação.

O Auto-scaling não reduz a capacidade de implementações em que o uso de disco/memória foi reduzido. Os recursos provisionados para seus bancos de dados permanecerão para suas necessidades futuras ou até você reduzir a capacidade de sua implementação manualmente.
{: .tip}
