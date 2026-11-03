---
hidden: true
---

# Output Management

## Prerequisites

* Business Central Integration Addon installed (RaptorBC)
* Installation of app BC Output Management.

In Current solution there are some functionalities that overlap the new ones so for now is necessary to deactivate the initial so there is not duplication in some distribution.&#x20;

<figure><img src="../../.gitbook/assets/image (599).png" alt=""><figcaption></figcaption></figure>

In 9altitudes Setup, the **Expand Post and Send** should be False (Do not know if RaptorBC should deprecate this functionality in the future)

<figure><img src="../../.gitbook/assets/image (474).png" alt=""><figcaption></figcaption></figure>

Also is necessary to deactivate the functionality “Save Document on Post to Raptor”, as this will do the same without any setup from BC Output Management. So this was also some Output Management being done in RaptorBC standard solution (Do not know if RaptorBC should deprecate this functionality in the future)



## Setup

The central point for the output management setup. Per record you can define what document to generate and when/how. All setup Is predefined when setting up Raptor on the environment.

When setting up additional entities, some technical knowledge surrounding the table ID Is necessary. Keep In mind the possibility of extra development when allowing documents to be generated from a certain table with the additional requirement of storing It In the Raptor archive.

<figure><img src="../../.gitbook/assets/image (440).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (489).png" alt=""><figcaption></figcaption></figure>

1. Table ID
2. Document type; multiple document types can be defined per table ID (each time with a new setup card)
3. Linked table ID
4. Report ID: The report we want to generate when executing the process we are setting up In this card.
5. Report caption; Caption of the above ID.
6. Default E-mail setup: link the e-mail setup we defined in the previous chapter to certain output cases. Use the default e-mail setup "Code Klanten" when generating Sales orders
7. Type of output: Defines how we want to distribute our report
8. Usage; define which kind of document this is.
9. Used; always on.
10. Generate documents on distribute: Distribute the document manually, only available for certain documents, when the distribute button Is available (Posted Sales Invoice,It w Posted Sales Credit Memo, Posted Purchase Invoice, Posted Purchase Credit memo)
11. Generate document on release; If the release action on a page Is selected with this parameter active, the document generation process will Initialise on this action.
12. Multiple unposted document; If Raptor only needs to save 1 (the most recent version of a certain document - will delete previous versions and re-upload the current document), this setup Is only possible for tables 36 &38 (Sales orders & Purchase orders)

<figure><img src="../../.gitbook/assets/image (423).png" alt=""><figcaption></figcaption></figure>

1. Print: It will send the generated document to Raptor archive and print as well
2. Print & E-mail; It will send the document to Raptor, print and e-mail If the base setup Is done
3. E-mail; It will send the document to Raptor and e-mail If the base setup Is done
4. No output; no document will be generated and distributed

In Generate Output Management Setup is possible to setup the tables that should send the documents to Raptor as well to distribute.

On this Page is possible to setup for unposted documents (from table 36 and 38) if is supposed to maintain only 1 version or is suppose to upload each time a document is released.

<figure><img src="../../.gitbook/assets/image (434).png" alt=""><figcaption></figcaption></figure>

It’s only available to this kind of documents.

To posted documents the documents are uploaded to system if they were not uploaded at posting / manual distributing / running batch.

To posted documents only 1 version is stored at Raptor, if the file is deleted from Raptor making a manual distribution is possible to resend the posted document to Raptor.

The supported documents are:

**Posted Documents:**

* Posted Sales Invoice, Posted Sales Credit Memo, Posted Purchase Invoice, Posted Purchase Credit memo,

**Unposted/Temporary Documents:**

* Proforma Invoice.
* As the base RaptorBC also supports the iframes to these documents, so if the base does not support this will also not support other kind of documents.

**Type of Outputs supported:**

* Print – It will send the document to Raptor and print.
* Print and Email – Will send the document to Raptor, print and email having the base setup done.
* Email– Will send the document to Raptor and email having the base setup done.

In Customers and Vendors we have the setup to choose the distribution list with output Management:

<figure><img src="../../.gitbook/assets/image (445).png" alt=""><figcaption></figcaption></figure>

From Sales Invoices is possible to release the document to distribute the proforma invoice with that process.

Batch Run

* The Codeunit 2057802 "EXA Raptor Output Man. Batch” can be used to activate the distribution by batch.

Document still not supported

* Blanket Orders, Return Orders, Confirmation Orders, because the RaptorBC base application does not have the iframes ready to those kinds of documents, is necessary to change the base application to then add them to distribution. Any other posted or unposted kind of documents supported in V5 version not mentioned in the supported documents.

Not supported:

* EDI
* Print outside documents via BC
* Template Identification on Uploading documents.
