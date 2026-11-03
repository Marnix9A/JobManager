---
description: >-
  Document Distribution Routes enable documents to be transferred/copied between
  entities, while preserving their history through tags.
---

# Document Distribution Routes

With document distribution routes, you can link entities to each other, ensuring that documents from one entity are automatically copied on to another (including template and extra fields).

When you copy a document for the first time, a new version (the copy) is created and enriched with additional tags associated with the entity where it originated. As you continue to copy this document to other entities, the same copy is retained, and new tags are added to reflect its links to the related documents. This ensures that the original document stays untouched.&#x20;

For example: linking item to sales order&#x20;

* When you add an item to a sales order line, and that item has documents attached to it in Raptor, a copy of those documents are automatically added to the sales order (and to the item).

## Setup in Business Central&#x20;

### 1. 9A Raptor Document Distribution Setup

Set up the routes that specify from and to where documents will be copied.

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

* From Entity: entity where you want to copy the documents from&#x20;
* To Entity: entity where you want to copy the documents to&#x20;
* Distribution Tags: this determines what documents you copy. Only documents with the document-tag that you specify here will be copied. **It is important that you provide a distribution tag, otherwise the copying won't work.**&#x20;
  *

      <figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>
  * These tags need to be created in Raptor (see Setup in Raptor: taxonomy > 1. File Tags)
  * Make sure to add these tags to your original document.
    *

        <figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>


* Action: Copy Selected Routes: you can copy the parameters (e.g. distribution tags) from this entity to another entity
  *

      <figure><img src="../../.gitbook/assets/image (196).png" alt=""><figcaption></figcaption></figure>

### 2. List of possible distribution routes

Only combinations of routes that make sense will work. The following list shows all the 13 available routes you can use.

<table><thead><tr><th width="218">From entity</th><th>To entity</th></tr></thead><tbody><tr><td>Customer</td><td>Sales Quote Header</td></tr><tr><td></td><td>Sales Order Header</td></tr><tr><td></td><td>Sales Invoice Header</td></tr><tr><td></td><td>Sales Return Order Header</td></tr><tr><td></td><td>Sales Credit Memo Header</td></tr><tr><td></td><td>Job</td></tr><tr><td>Vendor</td><td>Purchase Quote Header</td></tr><tr><td></td><td>Purchase Order Header</td></tr><tr><td></td><td>Purchase Invoice Header</td></tr><tr><td></td><td>Purchase Return Order Header</td></tr><tr><td></td><td>Purchase Credit Memo Header</td></tr><tr><td>Item</td><td>Sales/Purchase Quote Line</td></tr><tr><td></td><td>Sales/Purchase Invoice Line</td></tr><tr><td></td><td>Sales/Purchase Credit Memo Line</td></tr></tbody></table>

Posted documents (posted invoice, posted shipment/receipt) will follow the route from the unposted. Once you set up the right routes for the unposted files. Configuring this route ensures that linked documents are also transferred to the posted documents.

## Setup in Raptor: taxonomy

### 1. Document type&#x20;

In order for the distribution routes to work, you need to link Distribution Tags to the entities. These Distribution Tags need to be created in Raptor first.&#x20;

Create the distribution tags under the root tag 'Document Type' in the taxonomy tree. In this example we created 'Drawing' and 'Contract', but you are free to create other tags and link them to certain entities.&#x20;

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## Functionality

### 1. Document distribution: original and copies

When a document is added to an entity **for the first time**, a new document (the copy) is created with some additional tags. You can find this copy on both entities.&#x20;

When you distribute the document to other entities **after** that, these tags are added to the same initial copy. This way, there is an original document and **a single copy** that shows all the tags indicating where the document has been distributed.&#x20;

**Entity where you copy FROM:**&#x20;

On the entity where you copy from (customer, vendor, item), you will have the original document and the copy when the document is used in another linked entity.&#x20;

Original Document:&#x20;

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

Copy:&#x20;

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

* The copy has the following tags to indicate that it is a copy of the original
  * CreatedBySystem
  * Extra information about the entity where it is copied to. In this example the document was copied to a sales order line
    * Sales order line - sales order - customer linked to that sales order

**Entity where you copy TO:**&#x20;

On the entity where you copy to, you will only see the copy with all the&#x20;

### 2. Original documents on 9A viewer

At first glance, it is not clear what document is the original document and what are the copies.&#x20;

Because the copies of the document get the 'CreatedBySystem'-tag, you can filter the view to only show the original documents with the following query:&#x20;

<figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

* It is easier to save this query (step 3). For example under a name such as 'Original Documents'. That way, you can easily select the query and filter the documents
* This filter is available for all 9A viewers, so you can use it on other entities as well
*

    <figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

### 3. Example flow: item > sales order&#x20;

Document distribution setup:&#x20;

*   From item to sales order&#x20;

    <figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>
*   Distribution tag = FileType\Drawing

    <figure><img src="../../.gitbook/assets/image (198).png" alt=""><figcaption></figcaption></figure>

**1) Add a document to the item**&#x20;

On the item, add a document with the drawing distribution tag

*

    <figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

**2) Create a sales order with this item as a sales order line**

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

When you send the sales order to raptor, two documents are made in this case:&#x20;

* 1\) The standard sales order document
* 2\) A copy of the document from the item, with the following additional tags:&#x20;
  * &#x20;CreatedBySystem - sales order line - sales order - customer from the sales order
  *

      <figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

