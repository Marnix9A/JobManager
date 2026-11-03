# Invoice tag methods

Starting with release 10.2022.9.1, it is now possible to add additional tags to an imported invoice in Document Warehouse when it is posted. This is a fully generic solution that allows you to define tag methods based on the `VendInvoiceJour` table.

To implement this feature, consult a technical consultant to determine which methods are available and what type of return values should be used. It is important to note that the entities corresponding to the returned records must be included in the entity configuration within Document Warehouse.

<figure><img src="../../../.gitbook/assets/image (101).png" alt=""><figcaption></figcaption></figure>

***

There are two possible return types for tag methods:

1. **Record:**\
   The method returns a single record as an object. This is useful for retrieving the linked vendor transaction associated with your posted vendor invoice.
2. **Query:**\
   The method returns a query as an object. This is useful for retrieving multiple linked purchase orders associated with your posted vendor invoice.

Below is a list of the available table methods. Additionally, custom methods can be created to return other records for tagging in your imported invoice.

#### Root Table: VendInvoiceJour&#x20;

**1. vendTrans**

* **Purpose:** Returns the vendor transaction voucher.
* **Return Type:** Record (records from the `VendTrans` table).
* **Requirement:** The entity for the `VendTrans` table must be configured in Document Warehouse (e.g. EXAVENDTRANSENTITY).

**2. exaQueryVendInvoicePurchLink**

* **Purpose:** Returns linked purchase orders. This allows you tag posted invoices with their linked purchase orders.
* **Return Type:** Query (records from the `VendInvoicePurchLink` table).
  * **Requirement 1:** The entity for the `PurchTable` table must be configured in the [entity-configuration.md](../../../raptor-document-warehouse/configuration/entity-configuration.md "mention") (e.g. PURCHPURCHASEORDERHEADERV2ENTITY).
  *   **Requirement 2:** A [#relation-setup](../document-management/#relation-setup "mention") must be configured to link the PurchTable with the VendInvoicePurchLink table:\
      <br>

      <figure><img src="../../../.gitbook/assets/image (189).png" alt=""><figcaption></figcaption></figure>
