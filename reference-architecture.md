---
copyright:
  years: 2016,2018
lastupdated: "2018-06-07"

subcollection: compose-for-mysql

---

{:shortdesc: .shortdesc}
{:tip: .tip}

# Architecture 
{: #architecture}

## Replication

An {{site.data.keyword.composeForMySQL_full}} deployment starts with three data nodes in a cluster, spread over the region's availability zones. Data is replicated across all three nodes; if one data member in the cluster becomes unreachable, your cluster continues to operate normally. The cluster is configured so that if the leader member in the cluster fails, the current slave is promoted to leader within 60 seconds of the leader becoming unresponsive. 

## Disk Encryption

All {{site.data.keyword.composeForMySQL}} services have encryption at rest. Your data resides on servers that have volume-level encryption enabled. 

Because {{site.data.keyword.composeForMySQL}} is a managed service, it is possible for {{site.data.keyword.cloud}} Compose operators to see data. In addition to the disk encryption, we recommend that you encrypt personal information before storing it in the database or use extensions or features to enable encryption on the database itself. While these methods might impact usability or performance, it is good practice to ensure that personal information is protected with encryption.

## Auto-scaling

Resources are scaled automatically based on the total disk storage use of the MySQL databases. Memory usage is based on a ratio of provisioned storage at a ratio of 1:10. These resources are bundled as units.

Auto-scaling is designed to respond to the short-to-medium term trends of your database. Every hour, your service is checked and if it is running short on disk space, more units are allocated to the deployment.

Auto-scaling does not scale down deployments where disk/memory usage has shrunk. The resources provisioned to your databases will remain for your future needs, or until you scale down your deployment manually.
{: tip}
