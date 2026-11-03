# Report setup

The report setup can be found through the following path:\
**9A Raptor DWH > Setup > Output Management > Report Setup**

Currently, the module supports various providers:

* SmartFlows
* SSRS
* Electronic Reporting
* Dox42
* Xperido

#### **SmartFlows**

* All print destinations are supported with **SmartFlows** reports.
* Before using **SmartFlows** as a provider, ensure that the **9A Kickstart templates** are imported into SmartFlows.

***

#### **SSRS**

* All print destinations are supported with **SSRS** reports.
* **Troubleshooting Tip**: Verify whether the document is generated correctly via standard **D365FO**.

***

#### **Electronic Reporting**

* All print destinations are supported with **Electronic Reporting** reports. However, only the **9A Printer** is supported when Word/Excel documents are converted to PDF.
* Before using **Electronic Reporting** as a provider, ensure that the necessary electronic reporting templates are imported into **D365FO**.
* **Troubleshooting Tip**: Verify whether the document is generated correctly via standard **D365FO**.
* **Key Difference**: With **Electronic Reporting**, you don’t need to set up format mapping in the general print management setup, or in the customer/vendor print management setup. Instead, leave it as standard and set up the required format mapping in the report setup. Additionally, you don’t need to define electronic reporting destinations (as in standard D365FO).

***

#### **dox42**

* All print destinations are supported with **dox42** reports.
* To use dox42 templates, link the SharePoint URL of the dox42 template in the **Flows** section.

***

#### **XperiDo**

* This is for existing **XperiDo** customers.
* Connection information can be found in the **Ex Arte V5 Foundation**.
* All print destinations are supported with **XperiDo** reports.

Some setup options are only available for certain providers. For example, template development is only available when **SmartFlows** or **Dox42** is selected as the provider. Format mapping is only available when **Electronic Reporting** is selected.

***

### **Settings**

The mandatory settings are explained below, detailing how to use them for your reports.

* **Report Setup ID**: A unique identifier for each report setup.
* **Provider**: Options include SSRS, SmartFlows, Electronic Reporting, Dox42, Xperido.
* **Report Name**: This should match the report name in Print Management. Be sure to remove the suffix `.report` (default in D365FO) or any custom suffix.
* **Format Mapping**: This option is only available when **Electronic Reporting** is selected as the provider.
* **Company**: Enter a company name if you want to use the report setup for a specific company. If not filled, the system will search for a default report setup without a company.
* **Primary Table Name**: Required if you want to archive the report in Document Warehouse. It only works with regular tables (e.g., journal tables) and not with temporary tables.

***

### **General Settings**

* **Download XSD**: This option is available if SmartFlows, Dox42, or XperiDo is selected as the provider.
* **Download XML**: Also available for SmartFlows, Dox42, or XperiDo as the provider.
* **Document Template**: Works with the Raptor Document Warehouse. Triggered when **Ex Arte Archive** is selected as the print destination.
* **Email ID**: Choose an email template for sending emails to customers and vendors. If no company is selected, ensure the Email ID exists in every company used. Email templates can also include placeholders.
* **Activate Tracking**: Select "Yes" to track emails. If "No", emails are sent immediately. When tracking is activated, emails are sent via the email batch job (standard in D365FO).
* **Convert to PDF**: Enable this option if you want to convert Excel or Word documents to PDF. Keep in mind that the Raptor Document Warehouse integration must be activated.
* **Output Generation**: This has two options: 'Default' and 'Word'. It is only available with **Dox42** as the provider and converts documents to Word. When this option is enabled, the "Convert to PDF" setting becomes available. This allows you to generate PDFs with adjustable tables.
* **Trigger Business Event**: Use this to trigger a business event with information about the print generation (note: XML or attachments are not included).
* **Print as EMF**: By default, this is enabled for **Dox42** as the report provider. This option allows the DRA client to run in Windows Service mode.
* **Output Generation**: Allows you to choose the format for the document (PDF or Word). For **Dox42**, you can select either PDF (default) or Word. For other providers, PDF is always the default.

***

### **E-Platform**

This setup is available when the **E-Platform** integration is activated in the **9A Raptor DWH** parameters.

* **Use Only for E-Platform**: Supports XML generation only, without attachments.
* **REST Endpoint URL**: Specify the destination for E-Platform. This can be overridden at the vendor or customer level.
* **Document Template**: Works in conjunction with the Raptor Document Warehouse solution. The generated XML file will be archived in the Document Warehouse.

***

### **Flows**

This setup is available when the **SmartFlows**, **Dox42**, or **XperiDo** integration is activated in the **Output Management** tab of the **9A Raptor DWH** parameters.

* **Flow**: Choose a flow from the dropdown when **SmartFlows** or **XperiDo** is selected as the report provider. For **Dox42**, manually input the SharePoint URL where the template is stored.
* **Language**: Optional. Leave blank if the flow is for all languages. The language can be retrieved from the sales or purchase order.

***

### **Filenames**

You can set custom filenames to archive documents in Document Warehouse or for email attachments. Filenames can be specified for different languages, and placeholders can be used.

* **Default Filename**: If no specific filename is set for a report setup, a generic filename will be used for every generated document.
* **Electronic Reporting**: When using **Electronic Reporting** as a provider, the filename defined in Electronic Reporting will be used if none is specified in the report setup.

### **Attachments**

This is available only when **9A Email** or **9A Email Interactive** is selected as the print destination. Extra attachments can be added to emails based on tag setup. Document Warehouse must be set up before using this feature.

* **Tags**: Enter one or more tags as conditions.
* **Linked to Record**: Include the record as a tag condition (e.g., sales invoice journal, sales confirmation journal).
* **Linked to Company**: Include the company as a tag condition.
* **Linked to Language**: Include the language from the linked record as a tag condition.

<figure><img src="../../../.gitbook/assets/image (153).png" alt=""><figcaption></figcaption></figure>

***

### **Tag Methods**

This feature is available when **9A Archive** is used, starting from release **10.2022.9.1**. It allows you to add additional tags to archived documents in Document Warehouse, without the need for customizations.

Tag methods start from the primary table configured in the Report setup, and retrieve additional data  via a linked record or a query. This data is then translated into tags using the [entity-configuration.md](../../../raptor-document-warehouse/configuration/entity-configuration.md "mention")and applied on the archived document.&#x20;

<div align="left"><figure><img src="../../../.gitbook/assets/image (154).png" alt=""><figcaption></figcaption></figure></div>

* **Record**: Returns one record as an object.
* **Query**: Returns a query as an object.

Below is a list of existing primary tables with their corresponding table methods:

**Customer Confirmations**

* **Table**: CustConfirmJour
* **Methods**:
  * **queryCustConfirmSalesLink**
* **Purpose**: To return multiple sales order numbers.
* **Return Type**: Query – Records from the **CustConfirmSalesLink** table.
* **Entity Configuration**: The entity behind the **SalesTable** should be configured in Document Warehouse.
* **D365FO Relations**: Use relations in D365FO to link **CustConfirmSalesLink** and **SalesTable** in the [#relation-setup](../document-management/#relation-setup "mention")

***

**Customer Packing Slips**

* **Table**: CustPackingSlipJour
* **Methods**:
  * **queryCustPackingSlipSalesLink**
* **Purpose**: To return multiple sales order numbers.
* **Return Type**: Query – Records from the **CustPackingSlipSalesLink** table.
* **Entity Configuration**: The entity behind the **SalesTable** should be configured in Document Warehouse.
* **D365FO Relations**: Use relations in D365FO to link **CustPackingSlipSalesLink** and **SalesTable** in the [#relation-setup](../document-management/#relation-setup "mention")

***

**Customer Invoices**

* **Table**: CustConfirmJour
* **Methods**:
  * **queryCustInvoiceSalesLink**
* **Purpose**: To return multiple sales order numbers.
* **Return Type**: Query – Records from the **CustInvoiceSalesLink** table.
* **Entity Configuration**: The entity behind the **SalesTable** should be configured in Document Warehouse.
* **D365FO Relations**: Use relations in D365FO to link **CustInvoiceSalesLink** and **SalesTable** in the [#relation-setup](../document-management/#relation-setup "mention")
* **Table**: CustTrans
* **Purpose**: To return the customer transaction voucher.
* **Return Type**: Record – Record from the **CustTrans** table.
* **Entity Configuration**: The **CustTrans** entity should be configured in Document Warehouse.

***

**Project Invoices**

* **Table**: ProjInvoiceJour
* **Methods**:
  * **exaQueryProjInvoiceLinesUnion**
* **Purpose**: To return multiple project numbers.
* **Return Type**: Query – Records from the **ProjInvoiceLinesUnion** view.
* **Entity Configuration**: The entity behind the **ProjTable** should be configured in Document Warehouse.
* **D365FO Relations**: Use relations in D365FO to link **ProjInvoiceLinesUnion** and **ProjTable** in the [#relation-setup](../document-management/#relation-setup "mention")

***

**Customer Quotation Journals**

* **Table**: CustQuotationJour
* **Methods**:
  * **queryCustQuotationSalesLink**
* **Purpose**: To return multiple sales quotation numbers.
* **Return Type**: Query – Records from the **CustQuotationSalesLink** table.
* **Entity Configuration**: The entity behind the **SalesQuotationTable** should be configured in Document Warehouse.
* **D365FO Relations**: Use relations in D365FO to link **CustQuotationSalesLink** and **SalesQuotationTable** in the [#relation-setup](../document-management/#relation-setup "mention")

### **Placeholders**

In the Placeholders section we can define placeholders and map them to a specific field or method from a particular table.&#x20;

Placeholders can be used in filenames or email templates. Remember to enclose each placeholder with percent symbols (`%`) as both a prefix and suffix.

For example, the **%customername%** placeholder can be mapped to the **DeliveryName** field from the **CustConfirmJour** table (Sales Confirmations) or the **InvoicingName** field from the **CustInvoiceJour** table (Sales Invoices).

<figure><img src="../../../.gitbook/assets/image (195).png" alt=""><figcaption></figcaption></figure>

Another example is mapping the %**DeliveryAddress%** placeholder to the **deliveryAddress** method from the **CustConfirmJour** table.

<figure><img src="../../../.gitbook/assets/image (194).png" alt=""><figcaption></figcaption></figure>
