---
hidden: true
---

# Ex Arte Raptor Setup (Table) List

If we open this table, we can see several tables and associated numbers. These are all the tables for which tags are created by the Taxonomy setup within [https://raptor.adultimagroup.com/configuration/jobs](https://raptor.adultimagroup.com/configuration/jobs). The sync job will edit existing tags if there was a change since the last sync. The job will also make new tags if they don’t exist. Following entities are predefined when setting up the Raptor product on the environment:&#x20;

<figure><img src="../../.gitbook/assets/image (328).png" alt=""><figcaption></figcaption></figure>

If you edit a table you can see the following screen:

<figure><img src="../../.gitbook/assets/image (534).png" alt=""><figcaption></figcaption></figure>

What we are doing here is listing all fields of a Customer Card in Business Central. These are ranked by number. In column 2, we find the name of the field within BC. In column 3, you enter a logical name of the field that you integrate with Raptor. If you fill in this third column, you can choose a name and use this in the Raptor Entity Configuration. This is mandatory otherwise this will not work. In this example, we use 2 fields: number and displayName. We are going to use this in our Entity Configuration.

\
See  below:

<figure><img src="../../.gitbook/assets/image (517).png" alt=""><figcaption></figcaption></figure>

Make sure you check the mark: Integrate with Ex Arte Raptor, if you want to use this field in the Entity Configuration. You should integrate all fields that you use in Raptor Entity Configuration.

<figure><img src="../../.gitbook/assets/image (540).png" alt=""><figcaption></figcaption></figure>

If you describe a field and don't use it in Entity Config, it will delete this data.

<figure><img src="../../.gitbook/assets/image (551).png" alt=""><figcaption></figcaption></figure>

More info on Document Template Management soon.
