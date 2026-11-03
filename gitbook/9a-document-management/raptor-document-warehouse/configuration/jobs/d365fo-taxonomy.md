# D365FO Taxonomy

The D365FO Taxonomy job retrieves masterdata from Dynamics 365 F\&O using an export project in it's [Data Management functionality](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/data-entities/data-entities-data-packages). Raptor will retrieve the export created by F\&O and generate tags from it using the [entity-configuration.md](../entity-configuration.md "mention").\
Taxonomy jobs are useful to proactively create tags that might be useful for Raptor users.

{% hint style="info" %}
In most cases, Raptor integrations are capable of making tags ad-hoc, whenever they are needed. Taxonomy jobs are therefore not essential for a working production environment. Their primary purpose is to make tags available for manual search in Raptor.
{% endhint %}

D365FO Taxonomy jobs use a Source service connection to a Dynamics 365 F\&O environment (see [#service-connections](./#service-connections "mention")) and use the Default delta packager.

## Delta Fetch settings

To create a D365F\&O Taxonomy job, an Export project must be available in your Dynamics 365 F\&O environment. The export project can contains the list of entities that you wish to create tags for in Raptor. Be sure to choose 'XML-element' as source data format for each entity.

<figure><img src="../../../.gitbook/assets/image (188).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Set the default refresh type for each entity to 'Incremental push only' to prevent unnecessary load on your F\&O environment and Raptor tenant.  Incremental push requires activating [change tracking](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/dev-itpro/data-entities/entity-change-track) on the entity.
{% endhint %}

{% hint style="info" %}
Note that tags will not be created for an entity if there is no [entity-configuration.md](../entity-configuration.md "mention") set up for it.
{% endhint %}

**Uri**: the URL of your F\&O environment (e.g. https://finopsaos.cloudax.dynamics.com).

**Definition Group Id**: Group name of the export project

**Package name**: the name given to the created exports

**Legal Entity**: the legal entity in F\&O which the export should be made for

**Retention Days**: amount of days that the export should remain available

