# Feature flags

Via the feature management within Finance and Operations the following features can be enabled.

* **9A Document Management - Use SVG Images for the Document Warehouse Icon**
  * When this feature Is activated, the Dino icon is replaced by an SVG image, making it more suitable for different screen sizes.
  * Turned on by default
* **9A Document Management - Invoice register enhancements**
  * **Recalculation of invoice totals:** invoice totals are automatically recalculated when purchase orders are linked to a registered _invoice register_ journal.
  * **Invoice status**&#x20;
    * **Posted**: the &#x69;_&#x6E;voice register_ journal has been posted.
    * **Registered**: The vendor transaction is available in the _invoice pool_ (ledger journal type = `VendInvoicePool`).
    * **Matched**: The vendor transaction has been added to a &#x6C;_&#x65;dger approval_ journal (ledger journal type = `Approval`).
  * **Visualization in form Invoice register journal:** invoice totals can be viewed within the form _Invoice register journal_.
  * **Button Invoice pool availability:** button **Invoice pool** becomes available in the _All Invoices_ form when an invoice of type _Invoice Register_ has been posted.
  * **Button Pending vendor invoice availability:** button **Pending Vendor Invoice** appears in the _All Invoices_ form when a pending vendor invoice is created based on an _Invoice Register_ journal.<br>
* **9A Document Management - Invoice totals enhancement**
  * Enhancements regarding calculation of invoice totals for an imported purchase invoice
* **9A Document Management - Email distribution framework**
  * Provides an event-based framework for sending emails (configured on request).

