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

# 体系结构 
{: #architecture}

## 复制

{{site.data.keyword.composeForMySQL_full}} 部署从具有三个数据节点的集群开始，三个节点分布在区域的可用性专区中。数据会在所有三个节点之间进行复制；如果集群中的一个数据成员变为不可访问，集群仍会继续正常运行。集群配置为集群中的领导成员发生故障时，如果领导在 60 秒内无响应，那么当前从属成员将升级为领导。 

## 磁盘加密

所有 {{site.data.keyword.composeForMySQL}} 服务都具有静态加密。数据位于启用了卷级别加密的服务器上。 

由于 {{site.data.keyword.composeForMySQL}} 是受管服务，因此 {{site.data.keyword.cloud}} Compose 操作员可以查看数据。除了磁盘加密外，还建议您在数据库中存储个人信息之前，对这些信息加密，或者使用扩展或功能启用对数据库本身的加密。虽然这些方法可能会影响可用性或性能，但确保个人信息受到加密保护是比较好的做法。

## 自动扩展

资源将根据 MySQL 数据库的磁盘存储总使用量自动进行扩展。内存使用量基于按 1:10 比率供应的存储量。这些资源会捆绑为单元。

自动扩展旨在响应数据库的中短期趋势。系统每小时会检查一次服务，如果服务的磁盘空间不足，那么会向部署分配更多单元。

自动扩展不会向下扩展部署，即减少磁盘/内存使用量。向数据库供应的资源将保留以满足您的未来需求，或者直到您手动向下扩展部署为止。
{: .tip}
