# Invoice setup

#### **Purpose**

The **Invoice Setup Rule Engine** offers a wide range of possibilities. Through this engine, you can create specific rules for individual vendors, for all vendors within a specific vendor group, for all vendors based on a buyer group, and more. It’s also possible to create a generic rule engine that applies to all vendors in general.

Additionally, you can combine one or more rule headers for a single invoice. This means you could have one rule header for invoice processing, another for process management with **AgilePoint NX**, or for sending business events to **Microsoft Power Automate** for automation. Alternatively, you can use the **Stop Further Processing** functionality after the first rule header to ensure that subsequent rule headers are not applied to the invoice.

Rule headers can also be created as templates by disabling the **Enabled** checkbox. With templates, you can easily copy them for specific vendors.

***

### **Key Components**

**1. Rule Engine Header**

A rule engine header organizes multiple rule lines. Key functionalities include:

* Applying rules to a specific vendor
* Applying rules based on a query (see: Edit query)
* Enabling or disabling specific rule headers
* Stop processing after a specific header
* Reordering headers based on priority

<figure><img src="../../../.gitbook/assets/image (97).png" alt=""><figcaption></figcaption></figure>

**2. Rule Engine Lines**

Each rule header contains lines, each with a specific action or condition. You can optionally use queries to refine their execution. We recommend using queries to improve accuracy and relevance.

<figure><img src="../../../.gitbook/assets/image (98).png" alt=""><figcaption></figcaption></figure>



***

### **Rule types**

**Pre-actions**

Executed **before** creating ERP transactions.

* **Set invoice type:** define the type (e.g., Invoice Journal, Invoice Register). Saves type in the imported invoice header.
* **Set journal name:** assign ledger journal names in case of Invoice Journal or Invoice Register. You can use queries to detect which journal name can be chosen, the selected value is saved in the imported invoice header.
* **Set approver:** specify the invoice approver.
* **Set approved:** mark invoices as approved for payment
* **Set invoice payment release:** automatically populate today’s date, which can be manually overridden later.
* **Set voucher template:** define an existing voucher template. This way you can have predefined offset ledger accounts and distribution of the invoice total amount over all voucher template lines.
* **Set values from invoice default setup:** retrieve values from the invoice default setup from linked vendor or from general setup

**Actions**

Executed **during** transaction creation.

* **Set invoice data:** create ledger journal or vendor invoice headers using data from external sources and pre-actions.

**Post-actions**

Executed **after** ERP transactions are created.

* **Set business event:** trigger business event with data from imported invoice header
* **Set purchase order strategy:** define strategies for purchase orders or product receipts in case the invoice type is Pending Invoice. The selected value is saved in the imported invoice header. This logic will be applied during import of the purchase order references.
* **Check duplicates:** detect based upon setup and mark original invoice and duplicated invoices as duplicated.
* **Set purchase invoice workflow**: submit imported invoice in D365FO workflow.
* **Only in combination with Process Management**
  * **Set process template:** assign a process template from AgilePoint NX.
  * **Start process instance:** submit imported invoice in workflow from the Process Management parameters.
