# D365 Finance & Operations

{% hint style="info" %}
Newer release notes can now be found on the [9altitudes release notes website](https://releasenotes.9altitudes.com/9A%20Productivity%20Suite/9A%20Raptor%20Document%20Warehouse/D365-Finance-Operations/)!
{% endhint %}

## January 2026 (10.2026.2.1)

* Core
  * Improvements of helper functions for the mentioned features below
* Document management
  * Document distribution from Product to Released Product
  * Get Raptor context via the workflow work Item Improvements
  * Ability to delete a tag from a document with a record In code
  * Ability to delete a tag from a document with a tag object In code
* Input management
  * Populate list code In ledger journals from vendor when Transfer purchases Is activated In Foreign trade parameters
  * A checkbox 'E-Invoice only' Is foreseen on vendors to make a distinct between vendors who are using Peppol
  * Support for Tax Calculation Service for Imported Invoices In combination with purchase orders
  * Extension points for classes
    * EXAPurchInvoiceWorkflowParticipantProvider
    * EXAPurchInvoiceWorkflowHelper
* Output management
  * Provide ability to archive a report based upon checkbox 'Archive' in the report setup to archive the document always regardless the checkbox 'Archive In 9A Raptor DWH' In the print management settings. Please be aware with using this function because your report will archived every time!
  * (Preview) ability to generate HTML content with dox42 and use It for 9A Email and 9A Email Interactive with field Email template Setup Id In the report setup.
  * Change CacheLookup property from EntireTable to Found for table EXAReportSetup



## November 2025 (10.2025.11.1)

* Core
  * Change configuration key from 'Ex Arte Raptor' to '9A Raptor DWH'
* Document management
  * Get sales/purchase agreement history as context from the agreement history journals
  * Document distribution framework extensions
    * Add a custom document template Instead of copy current document template
    * Add custom document tags Instead of copy current document tags
  * Show dino Icon only If the record behind a workflow work Item Is used In 9A Raptor Document Warehouse
  * Possibility to validate connection between D365FO and 9A Raptor Document Warehouse. If the validation Is passed, you will receive a Infolog with the tenant and the external system details.
  * Ability to get a specific document from 9A Raptor DWH for Electronic Reporting framework
    * Function GetDocumentFromRaptorWithParms
    * Example: GetDocumentFromRaptorWithParms("CustInvoiceJour", "InvoiceId", "InvoiceIdNumber", GetCurrentCompany(), "pdf", "DocumentTypes\SalesInvoice")
    * Function GetDocumentFromRaptorWithParmsAndWithoutRecord
    * Example:GetDocumentFromRaptorWithParmsAndWithoutRecord(GetCurrentCompany(), "txt","DocumentTypes\GeneralConditions","en-us")
  * Ability to get multiple documents from 9A Raptor DWH for Electronic Reporting framework
    * Class EXADocuERDocumentAttachmentHelper
    * Function getDocumentsWithParmsAsArrayList with same parameters as above
    * Function getDocumentsWithParmsAndWithoutRecordAsArrayList with same parameters as above
  * Extension of document distribution framework for next entities as alternative of the existing feature 'Tag documents outside FO'
    * Project Invoice proposal to project Invoice journal
    * Sales order header to sales Invoice journal
    * Purchase order header to purchase order confirmation journal
    * Sales order header to sales confirmation journal
    * Sales order header to sales packing slip journal
* Input management
  * Bugfix regarding Invoice duplicate check If the rule Is processed without setup behind duplicate check
  * Activation of fields 'Created by' and 'Modified by' for table EXAPurchInvoiceImported
  * Extension points for class EXAPurchInvoiceAttachmentArchiveService
* Output management
  * Change label 'Read certificate' to 'Validate certificate' for dox42

## October 2025 (10.2025.10.1)

* Core
  * Increase password/secret fields to 100 chars
  * Ability to run a batchjob for cleanup of HTTP logging records. However It Is still recommend to disable the HTTP logging feature If It's not necessary. This feature Is Introduced to Investigate Issues In HTTP communication between D365FO and external Integrations.
* Document management
  * Increase password/secret fields to 100 chars
  * Extension of document distribution framework for next entities
    * Customer account to sales order header
    * Customer Invoice account to sales order header
    * Vendor account to purchase order header
    * Vendor Invoice account to purchase order header
* Input management
  * Improvements for Invoice Capture Integration
  * Invoice type as new field In the Invoice default setup overview
  * No/Yes dialog Is foreseen when an end-user want to cancel an invoice In the user Interface
  * Vendor responsible field Is foreseen for the Imported Invoices. This field Is populated with Employee responsible from your vendor. Also a migration script Is foreseen and automatically executed to fill It for existing Imported Invoices.
  * Introduction of new feature 'Invoice check duplicate setup' to mark Imported Invoices as duplicates based upon setup. This feature Is triggered with Invoice rule 'Check duplicates'
  * Improvements In performance for reinitialize Invoices In combination with purchase orders
  * Improvements for D365FO purchase Invoice workflow
    * Posting of an Imported Invoice as workflow automated task
    * Functions as conditions - Pending vendor Invoice - has purchase order - Pending vendor invoice - has purchaser - Pending vendor Invoice - has requester - Has vendor responsible
    * VendTable as additional datasource
    * New Invoice rule to trigger a workflow during Import of an Invoice
* Output management
  * Increase password/secret fields to 100 chars
  * Skip HTML encoding for email subject during email generation to avoid encoding problems with special symbols
* Process management
  * Increase password/secret fields to 100 chars



## June 2025 (10.2025.5.2)

* Core - 10.2025.5.1
  * Provide helper functions for SharePoint / MS Graph Integration
  * Provide helper functions for Import & read certificates (pfx)
* Document management - 10.2025.5.2
  * Introduce a function for Electronic Reporting to get documents from 9A Raptor Document Warehouse and embed It In outbound Electronic Reporting documents.
* Input management - 10.2025.5.2
  * Improvements for Invoice Capture Integration regarding attachments
  * Correction for field Remark to make It editable In every situation
* Output management - 10.2025.5.2
  * Support client certificate authentication for dox42 Integration

## May 2025 (10.2025.5.2)

This release is important for every customer who use dox42 for report generation due deprecation of service accounts with MFA authentication.

* Core - 10.2025.5.1
  * Provide helper functions for SharePoint / MS Graph Integration
  * Provide helper functions for Import & read certificates (pfx)
* Document management - 10.2025.5.2
  * Introduce a function for Electronic Reporting to get documents from 9A Raptor Document Warehouse and embed It In outbound Electronic Reporting documents.
* Input management - 10.2025.5.2
  * Improvements for Invoice Capture Integration regarding attachments
  * Correction for field Remark to make It editable In every situation
* Output management - 10.2025.5.2
  * Support client certificate authentication for dox42 Integration&#x20;

## May 2025 (10.2025.5.1)

* Document management
  * Improvements regarding purchase Invoice attachments upload to 9A Raptor Document Warehouse
* Input management
  * A feature with ability to populate purchase Invoice attachments In a table where the attachments are uploaded to 9A Raptor Document Warehouse with a batch job (to support 9A Smart Connect, Invoice Capture,…)
  * Add EXAPurchInvoiceWorkflowResubmit menu Item to privilege EXAPurchInvoiceWorkflowAction
  * Keep the old voucher template If the voucher template dialog Is canceled
  * Get the purchase strategy value from the dialog when Change Invoice type dialog Is opened (Peeters)
  * A new field Remarks Is added to the purchase Invoice header and the form All Imported Invoices (several customers)
  * Correction for Invoice totals calculation when cash discount Is used for Invoice journals and Invoice registers
  * Activation of Allow Row Version Change Tracking for tables
    * EXAPurchInvoiceImported
    * EXAPurchInvoiceImportedFields
    * EXAPurchInvoiceLineImported
    * EXAPurchInvoiceLineImportedFields
    * EXAPurchInvoiceImportedPurchLink
* Output management
  * No HTML encoding for generated filenames based upon placeholders
  * Disable std D365FO email body editor when print destination 9A Email or 9A Email Interactive Is selected

## February 2025 Hotfix (10.2025.2.2)

A regression issue was found regarding email adresses validation in our Output management solution. This issue is identified, fixed and available via the known channels. An upgrade to 10.2025.2.2 is only if you have installed the version 10.2025.2.1. No actions are required for older versions.

## February 2025 (10.2025.2.1)

* Document management
  * Feature 'Use SVG images for the Document Warehouse icon' is enabled by default
* Input management
  * Ability go to the right invoice from the assigned workflow work items
  * Include Project as offset account type for calculation of invoice totals with feature 'Invoice totals ehnancement'
  * Define a default voucher template in invoice default setup
  * Extend query LedgerJournalWFApprovals with field EXADocNo to get documents via the workflow form when std D365FO workflow is used for ledger journals&#x20;
* Output management
  * Get the first record from a query based report and use in combination with placeholders
  * Split agreement confirmation for purchase and sales agreements and get placeholders based upon proforma and posted agreement confirmations
  * Move validation for wrong email adresses as prestep when 9A Email or 9A Email Interactive is used as print destination
  * Foresee an extension point with ability to assign extra tags as customization for the archived document when a generated document is archived in Raptor Document Warehouse

## October 2024 (10.2024.10.1)

* General
  * Rebranding of our solution in the user interface
    * ‘Ex Arte’ is replaced by ‘9A’ for print destinations
    * ‘9A Document Management’ is replaced by ‘9A Raptor DWH’
  * Provide a data entity for outbound and inbound load headers (WHSLoadTable)
  * Provide a data entity for customer collection letter journals (CustCollectionLetterJour)
* Document management
  * Possibility to copy a selection of values for a selected document in Raptor Document Warehouse if Raptor Document Warehouse is opened inside D365FO
  * Auto update of connection URL from raptor.adultimagroup.com to raptor.9altitudes.com. This is applied automatically during the database synchronization. No further actions are required.
* Input management
  * Force to create a VendInvoiceInfoSubTable if no purchase order lines or product receipt lines are found
  * Extend query VendInvoiceDocument with field EXADocNo to get documents via the workflow form when std D365FO workflow is used for pending vendor invoices
  * Changes in the sales tax calculation for voucher templates
  * No push of tax amounts anymore from Kofax to ledger journals
  * Only reinitialize invoice if a changed field is part of field group EditableFields
  * Introduction of invoice default invoice setup
    * Via this way we can setup default values in general
    * Also we can override default values for a specific vendor
    * This step can be triggered with rule ‘Set values from invoice default setup’. This step should be done before call rule ‘Set invoice data’.

## July 2024 (10.2024.7.1)

* General
  * License report usage - it will report license usage and information to a database in 9altitudes tenant. The batchjob will start by it self and is required to run. No sensitive or user information is reported only counts, license name and license serial number.
* Document management
  * Availability of PdfMerge endpoint where we can merge different PDF documents into one PDF document
* Input management
  * Autofill purchase order number in the pending vendor invoice if no purchase order lines or product receipt lines are found
  * Add field 'Document No' in the listpage overview of pending vendor invoices
* Output management
  * Possibility to choose for PDF or Word as output generation in case of dox42 is used as report provider
  * Label correction 'Opschonen' within NL as label file

## May 2024 (hotfix)

* Input management
  * It was not possible to edit or to save an Imported Invoice since the VendTrans datasource was added to the EXAPurchInvoiceImported form
* Output management
  * hotfix - for XperiDo as report provider

## May 2024 (10.2024.5.1)

* Document management
  * Includes API endpoints to get user Info and or to execute query based upon user Info from Raptor Document Warehouse
  * Extension of distribution setup to copy documents from released product to a purchase requisition line.
* Input management
  * Add table VendTrans as read-only outerjoin In form All imported invoices. Via this way you can add fields from table VendTrans via personalized views In the mentioned form.
  * Introduction of D365FO workflow for the imported invoices. Via this way you can approve invoices for payment with the workflow. To use this feature the configuration key Purchase Invoice workflow should be activated. If you want to use this feature then the module Process management shouldn’t be Installed.
  * To allow delete pending vendor Invoices that are created via an Imported Invoice with Invoice type Invoice Register. Delete pending vendor Invoices with Invoice type Pending Vendor Invoice can’t be deleted.
  * Bugfix where the fixed asset amounts weren't applied In the Invoice totals overview.
* Output management
  * Introduction of XperiDo as new report provider. To use this feature the configuration key XperiDo should be activated.
  * Bugfix for Electronic reporting as report provider In combination with new reports as customization.

## March 2024 (10.2024.3.1)

* General
  * Throw a clear error message If no token Is generated for ROPC flows
* Document management
  * Use the dino icon to get documents for a linked context via a workflow work Item
  * Copy the document template when documents are copied via the distribution framework
  * Possibility to validate the entity configuration In Raptor Document Warehouse from D365FO
* Input management
  * Selection of products receipts for a specific vendor account. This feature give you as end-user a possibility to select product receipts of other non-captured purchase orders.
  * Invoice totals calculation - force to calculate tax amounts for Imported ledger journal lines via Excel to avoid to post a ledger journal without tax amounts.
* Output management
  * Throw error If no OAuth 2.0 token Is generated for dox42 flows (see section General)
  * Support for Business Documents with TempDB tables (Customer statement report as example)
  * Include print destination (PrintMediumType) In the general Info node during XML generation

## January 2024 (10.2024.1.1)

* Document management
  * Provide a query to get all purchase orders based upon a posted vendor Invoice
  * Change behavior of the tag selector dialog so an end user has a possibility to fill a tag code manually without to use the dialog
  * Improvements for embedded Document Warehouse In standard D365FO document viewer
    * Support for filenames with spaces and without spaces
    * Visualization of Images (PNG, JPG, JPEG,…)
* Input management
  * New way of calculation of Invoice totals for Invoice journals and Invoice registers - this can be done with activation of feature ' 9A Document Management - Invoice totals enhancement' In standard D365FO feature management
  * Add extra validations to avoid purchase Invoice totals calculation If a pending vendor Invoice Is created without a link to our Input management
  * Bugfix regarding creation of different pending vendor Invoices based upon one product receipt
* Output management
  * Remove double enters during generation of emails based upon predefined email templates
  * Fixed a bug during XML generation for E-Platform when no document template Is defined

## &#x20;November 2023 (hotfix)

* Output management
  * Hotfix for report providers SSRS and Electronic reporting where it's stuck during document generation

## November 2023

* General
  * Provide a data entity for purchase RFQ headers
* Document management
  * Support for Danish translations
  * Embed Document Warehouse In standard D365FO document viewer
    * Useful for scenarios like viewing Instructions In Manufacturing Execution Integration
    * Useful to view documents In standard D365FO DocuRef form
  * Distribution setup for Purchase RFQ lines
  * Distribution functionality from Purchase requisition lines to purchase RFQ lines
  * Distribution functionality from Purchase requisition lines to purchase order lines
  * Distribution functionality from Purchase RFQ lines to purchase order lines
  * Fix regarding distribution on InventTrans level in combination with planned orders
  * Support for Enterprise Asset Management to open Document Warehouse regarding asset objects
* Input management
  * Support Change Invoice type for all Invoice types
* Output management
  * Support for EMF generation If dox42 Is used as report provider\
    (DISCLAIMER - the dox42 backend per tenant should be upgraded to latest version)

## September 2023

* General
  * Provide a data entity for production order attachments
* Document management
  * Add field 'EXADocumentId' In the standard FO data entity DocuRefEntity
* Input management
  * Fix regarding cash discount amounts for Invoice journals and Invoice register journals
  * Visualization of Invoice totals In Invoice journal form as factbox
  * Invoice register enhancements - this can be done with activation of feature In the feature management
    * Visualization of Invoice totals In Invoice register journal form as factbox
    * Fix regarding Invoice status Posted when an Invoice Is posted from the Invoice pool
    * Matching of Invoice totals when an Invoice of type Invoice Register Is registered and It's linked to a purchase order
    * Visualization of button Invoice pool In the All Invoices form
* Output management
  * Support for query based SSRS reports next data providers In our report setup
  * Introduction of Advanced email distribution framework - this can be done with activation of feature In the feature management
  * Fix regarding using archived document as baseline for triggering tag methods

## June 2023

* Document management
  * Distribution framework - category can be empty for distribution of purchase order lines, sales order lines, agreement lines and sales quotation lines.
  * Replacement of legacy Document Warehouse - FO plugin by Document Warehouse Generic plugin
  * Distribution framework - Include Integration from Released product to Production order
  * New API endpoints to support fields In the Document Warehouse
  * Replacement of old PNG Images by SVG Images for the dino Icon - this can be done with activation of feature In the feature management
* Input management
  * Fix regarding cash discount date Initialization - use the Invoice date Instead of date of today&#x20;
  * Fix regarding calculation of actual sales tax amounts If an Invoice template Is used
  * Move logic for add tag methods for Imported purchase Invoices during posting from the central screen to the corresponding forms (Invoice journals, register journals and pending vendor Invoices)
* Output management
  * Change logic in the attachments logic so no attachments are retrieved if the linked record is not found as context in the Document Warehouse (specific for proforma situations)
  * dox42 Integration - give any exception if the generated document is not a valid document&#x20;
  * Dummy SSRS reports for sales and purchase agreements since std FO have one report for both types
* Process management
  * Fix regarding table relations for process history and actors

## March 2023

* Document management
  * Fix regarding sending context to Document Warehouse when you are hovering over a form part.
  * Provide a menu item to open Document Warehouse on purchase requisition lines
* Input management
  * New custom field 'BUYER\_VAT\_NUMBER' is introduced where the buyer VAT number is populated from Kofax. This can be used as condition in the invoice setup rules. If you want to use it for existing customer, please ask the Raptor team to execute changes in the E-Platform routes.&#x20;
  * Change logic regarding calculation from your imported invoice if it's a credit note with a reversed tax amount.&#x20;
  * Validate currency code between imported invoice and purchase orders if a purchase order with another currency code is selected afterwards.&#x20;
* Output management
  * Field Format mapping is available in the Ex Arte Report setup data entity.

## February 2023

* Document management
  * Fix regarding sending context to Document Warehouse when you are hovering over a form part.
  * Provide a menu item to open Document Warehouse on purchase requisition lines
* Input management
  * New custom field 'BUYER\_VAT\_NUMBER' is introduced where the buyer VAT number is populated from Kofax. This can be used as condition in the invoice setup rules. If you want to use it for existing customer, please ask the Raptor team to execute changes in the E-Platform routes.&#x20;
  * Change logic regarding calculation from your imported invoice if it's a credit note with a reversed tax amount.&#x20;
  * Validate currency code between imported invoice and purchase orders if a purchase order with another currency code is selected afterwards.&#x20;
* Output management
  * Field Format mapping is available in the Ex Arte Report setup data entity

## November 2022

* General
  * Availability of table CustTrans as data entity
  * Availability of table CustInvoiceTable as data entity
  * Availability of table CustQuotationJour as data entity
* Document management
  * Fix regarding sending context to Document Warehouse when you are hovering over a customer or vendor account number
  * Distribution framework for sales quotations to customer quotation journals
  * Distribution framework for customer free text invoices to customer invoice journals
  * \[Technical] method parmDocumentTemplate in class EXADocumentAttachment will be deprecated and is replaced by method parmTemplate
* Input management
  * A button for opening Document Warehouse to display the imported invoice. Via this way the end-user has an ability to view the same imported invoice across whole D365FO application without automatic link
  * Get invoice date, invoice number and description from previous line when a new line is created in the ledger journals that are created from our solution
* Output management
  * Fix regarding outgoing emails when print destination 'Ex Arte E-mail' is used in combination with 'Activate tracking' is enabled in the report setup
  * \[Technical] Refactoring logic for Ex Arte print destinations selection in the print destination settings form. This allow us to combine our solution with other ISV solutions who rely on custom print destinations.

## September 2022

* General
  * Rebranding to 9A Document Management / Document Warehouse
* Document management
  * Include support for query expressions In the endpoint between D365FO and Document Warehouse
  * Rename 'Environment' to 'External system' In the 9A Document management parameters form - parameter tab Document Management
* Input management
  * Improvements for rule Set voucher template
  * Generic solution to add additional tags when an imported Invoice is posted from our imported invoices central screen
  * Label corrections In general
* Output management
  * Fixed filename Is not applied when primary table name Is not defined In the report setup
  * Generic solution to add additional tags when the generated document Is archived In Document Warehouse
  * Business event trigger when an Ex Arte print destination Is executed
* Process management
  * Improvements regarding refresh process history or process actors when switching from an imported invoice to other imported invoices\
    \
    &#x20;

<br>
