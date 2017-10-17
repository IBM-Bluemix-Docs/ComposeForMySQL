---

copyright:
  years: 2017
lastupdated: "2017-10-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Backups
{: #backups}

You can create and download backups from the *Manage* page of your service dashboard. Both scheduled and manual backups are available.

## Viewing existing backups

Daily backups of your database are automatically scheduled. To view your existing backups, navigate to the *Manage* page of your service dashboard. 

![Backups](./images/mysql-backups-show.png "A list of available backups")

Click on the corresponding row to expand the options for any available backup.

![Backup Options](./images/mysql-backups-options.png "Options for a backup.") 

## Creating a backup on demand

As well as scheduled backups you can create a backup manually. To create a manual backup, navigate to the *Manage* page of your service dashboard and click *Backup now*.

## Downloading a backup

To download a backup, navigate to the *Manage* page of your service dashboard and click *Download* in the corresponding row for the backup you wish to download.

## Restoring a backup

To restore a backup to a new service instance, follow the steps to view existing backups, then click in the corresponding row to expand the options for the backup you want to download. Click on the **Restore** button. A message is displayed to let you know that a resotre has been initiated. The new service instance will automatically be named "mysql-restore-[timestamp]", and appears on your dashboard when provisioning starts.