---
description: >-
  This article describes the Entity Configurations tab in the Raptor
  Configuration app.
---

# Data Sync Jobs

In the Data Sync Jobs tab, the user is able to define export packages for the D365CE Taxonomy job in Raptor. By defining a Taxonomy job, records from D365 CE can be automatically created as tags in the background. See [jobs](../../raptor-document-warehouse/configuration/jobs/ "mention") for more info.

To create a Data Sync Job click '+ New'.

Provide the following parameters:<br>

* Package Name: the name of your export

{% hint style="warning" %}
The following fields are obsolete and longer required:

* Cron Schedule
* AzureBlobContainerName
* AzureBlobStorageAccount
* AzureBlobStorageKey
{% endhint %}

* Entities

Choose the entities you wish to export. Only the entities made in [entity-configurations.md](entity-configurations.md "mention")will be available.
