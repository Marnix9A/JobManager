# Distribution setup

The distribution setup give the end-users possibility to distribute documents from an entity to an entity based upon conditions. We provide two different solutions to distribute documents. It can be done with tagging context of entity to (same document with tags from both entities) or to copy documents and tagging context of entity to (= standalone documents). This form can be found via 9A Raptor DWH > Setup > Document management > Distribution setup.

* Tags: retrieve documents based upon predefined tags
* Description: free text for extra explanation
* Entity type from: from which entity should it distributed
* Entity type to: to which entity should it distributed
* Distribution type:
  * Add tag: same documents with tagging the context of entity to
  * Copy documents: standalone documents with tagging the context of entity to
* Copy tags: in case of copy documents as distribution type the tags from first column will tagged as well
* Copy document template: In case of copy documents as distribution type the document template of originally document will be copied to new document as well

Our 9A Raptor DWH provides a hybrid solution where you can upload documents to the standard D365FO document handling framework with a reference to 9A Raptor DWH. You need to create a document type with Attach file as class. For a location please select Document Warehouse as external storage.

With this functionality a reference is made between the document handling record and 9A Raptor DWH. You can open or remove the reference like other document handling records.

This chapter describes the necessary setup for a proper security integration with 9A Document Management. There is a security privilege that can be added to a custom duty/role for displaying the 9A Document Management dino icon.

Also  the next duties can be added for the user that is used in the 9A Raptor DWH synchronisation. This user is linked with the Azure Client Id via the Azure Active Directory applications in Dynamics 365 for Financials and Operations.

From the 10.2024.3.1 release we can validate our data management export project against the 9A Raptor DWH to Identify which entity configurations are missing In the 9A Raptor DWH. Therefore we need go to the menu 'Document Warehouse' for a specific export data management project.

Every missing data entity In 9A Raptor DWH will be displayed In the Infolog. Via this way any system administration can add missing data entities In 9A Raptor DWH and complete the Integration.&#x20;

#### **Distribution Setup Overview**

The **Distribution Setup** feature allows end-users to distribute documents between entities based on specific conditions. The 'distribution' means either adding new tags to the source document or making a copy of the document and adding new tags.

You can access the Distribution Setup form via:\
**9A Raptor DWH > Setup > Document Management > Distribution Setup**

Before setting up distribution rules, make sure Distribution is enabled, see [#distribution-setup](../9a-raptor-dwh-parameters/document-management.md#distribution-setup "mention").

***

#### **Key Terms and Options**

* **Tags**: Used to retrieve documents based on predefined identifiers.
* **Description**: Free-text field to describe your distribution.
* **Entity Type From**: The source entity for the distribution.
* **Entity Type To**: The target entity for the distribution.
* **Distribution Type**:
  * **Add Tag**: The same document is tagged with the context of the target entity.
  * **Copy Documents**: A new, standalone document is created and tagged with the context of the target entity.
  * **Copy Tags**: For "Copy Documents" distributions, the tags from the source document are applied to the new document.
  * **Copy Document Template**:  the document template (see Raptor templates: [templates.md](../../../raptor-document-warehouse/configuration/templates.md "mention")) from the original document is copied to the new document.
  * **Tags to Attach**: the tags that should be added during the distribution
  * **Document template**: the template that should be assigned during the distribution

**Example scenario**

<figure><img src="../../../.gitbook/assets/image (109).png" alt=""><figcaption></figcaption></figure>

In the example above, distribution setup is used to distribute documents tagged as 'Drawing' from the Released product to the Production order and Purchase order line. \
The distribution of product related documents to the purchase order level also makes them eligible as attachments for the purchase order emails, see  [#attachments](../output-management/#attachments "mention").

#### **Applying Distribution Rules**

You can define specific distribution rules for certain records based on the source entity. To do this, use the **Edit Query** menu item to create relationships between the source entity and other tables.

Examples:

* Distribute documents with specific tags for **released products** in a particular **item group**.
* Distribute documents for **released products** associated with a specific **primary vendor**.

#### **Available Distribution routes**

* From product to
  * Released product
* From released product to
  * Sales order line
  * Purchase order line
  * Sales quotation line
  * Sales agreement line
  * Purchase agreement line
  * Production order
  * Purchase requisition line
  * Request for quotation case line
* From sales order header to
  * Sales invoice journal
  * Sales confirmation journal
  * Sales packing slip journal
  * Load header
  * Shipment header
* From purchase order header to
  * Purchase order confirmation journal
  * Load header
  * Shipment header
* From sales order line to
  * Production order
  * Load line
* From sales quotation line to
  * Sales order line
* From sales agreement line to
  * Sales order line
* From purchase agreement line to
  * Purchase order line
* From sales quotation to
  * Customer quotation journal
* From customer free text invoice to
  * Customer invoice journal
* From purchase requisition line to
  * Purchase order line
  * Request for quotation case line
* From customer account to
  * Sales order header
* From customer invoice account to
  * Sales order header
* From vendor account to
  * Purchase order header
* From vendor invoice account to
  * Purchase order header
* From project invoice proposal to
  * Project invoice journal
* From sales agreement header to
  * Sales agreement confirmation header
* From purchase agreement header to
  * Purchase agreement confirmation header

## **Distribution Entity Type Setup**

With the **Distribution Entity Type Setup** you can set when the distribution of the documents should take place. For each target entity type (**Entity Type To**) a **Processing mode** can be selected.

You can access the Distribution Entity Type Setup form via:\
**9A Raptor DWH > Setup > Document Management > Distribution Entity Type Setup**

<div align="left"><figure><img src="../../../.gitbook/assets/image (720).png" alt="" width="352"><figcaption></figcaption></figure></div>

The processing mode options are:

* **Immediately (During posting)**: This option will distribute the documents at the same time as the target entity is created.
* **In batch (After posting)**: This option will distribute the documents at a later time after the target entity is created. A batch job is needed to be setup to process the distribution of these documents.&#x20;

The default option for most entities is **Immediately (During posting)**. It can be set to **In batch (After posting)** if&#x20;

* a lot of documents are to be distributed and the performance is impacted
* the distributed documents are not needed immediately after posting
* there is a chance of a transaction rollback after the document distribution. Once a document is distributed, a transaction rollback will not perform the rollback of the distribution.

For some entities the option **In batch (After posting)** is the default or even mandatory. It can be mandatory when there is a many-to-one/many relation between the source and the target entity.

When a target entity is created that has its **Processing mode** set to **In batch (After posting)**, a queue record will be created to process the document distribution later on.

Use the **Distribute queued documents** periodic task to schedule the processing of those queued document distributions.

You can access the Distribution Entity Type Setup form via:\
**9A Raptor DWH > Periodic tasks > Document Management > Distribute queued documents**
