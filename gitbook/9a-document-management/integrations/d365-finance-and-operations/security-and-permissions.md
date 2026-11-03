# Security & permissions

## Viewing the Raptor 'dinosaur' button

To be able to see the Raptor 'dino' icon on a page, the following privilege is required:\
_**To view Ex Arte Raptor document list**_

{% hint style="warning" %}
If a user with this privelege still does not see the 'dino' icon while other users do, verify if the setting 'Enable document handling' is turned on in the user's preferences (System administration > Users > Users > User options > Preferences).
{% endhint %}

## Required Security Roles for the Raptor Service Account

Raptor uses a dedicated service account, linked to a Microsoft Entra ID app registration, to export data from Dynamics 365 Finance & Operations (D365 F\&O).

### Minimum Required Duties

The service account must be assigned the following duties:

* **View Document Entity Data for Data Management**
* **View Document Entity for Data Management (Extension)**

> **Important:** These duties provide access to all standard D365 F\&O data entities.

If your integration uses custom data entities, the service account requires additional permissions:

* Assign the **View** privilege for each custom data entity that needs to be synchronized.
* If the integration (E-Platform) creates or updates records, also assign the **Maintain** privilege for the corresponding data entities.

If your implementation only requires a limited number of data entities (for example, when using the Kickstart solution), a standard duty is available that can be extended with project-specific data entities.

### Ex Arte Raptor Core Data Entities

The **Ex Arte Raptor Core Data Entities** duty grants access to the core entities required for document synchronization, including:

* Sales order packing slip headers
* Ledger journal headers
* Project invoice headers
* Vendor invoices, invoice lines, purchase links, and product receipt lines
* Customer transactions, including free-text invoices and quotation journals
* Production order attachments

### Ex Arte Raptor Data Entities

The **Ex Arte Raptor Data Entities** duty provides access to the business master data required for synchronization, including:

* Vendors, prospects, customers, and contact persons
* Projects
* Purchase order headers
* Sales order headers
* Products and released products
* Sales agreement headers
* Purchase agreement headers
* Production orders
* Return order headers
* System users
* Expenses

### Ex Arte Raptor Input Data Entities (View and Maintain)

The **Ex Arte Raptor Input Data Entities** duty provides both **View** and **Maintain** permissions for imported data entities, including:

* Ex Arte imported invoice headers
* Ex Arte imported invoice lines
* Ex Arte imported invoice header fields
* Ex Arte imported invoice line fields
* Ex Arte imported invoice purchase links

### Summary

Assign only the duties and privileges required for your implementation. Additional **View** and **Maintain** privileges should be granted only for the custom data entities used by your integration, ensuring both secure and efficient synchronization.
