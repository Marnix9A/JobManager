# Imported invoices

## **Imported Invoices Features**

### **Actions**

* **Reinitialize Invoice:** Remove the ledger journal/pending vendor invoice and reapply the invoice setup rules - if the status is "Imported."
* **Change Invoice Type:** Create a new ledger journal/pending vendor invoice without reapplying rules for "Imported" invoices. You may need fill in extra required fields based on the selected invoice type.
* **Cancel Invoice:** Delete an invoice and its associated records.
* **Select Product Receipts**: Users can select product receipts for non-captured purchase orders, filtered by vendor accounts designated as Invoice accounts. Additionally, users can deselect product receipts if they are already linked to another invoice, for example. Only product receipts with line items matching the currency code of the associated imported invoice can be selected.
* **Post Invoice:** Quickly post invoices without navigating through linked journals.
* **Approve for Payment**: This functionality allows users to approve an invoice for payment if payment approval is not applied to the ledger journal or pending vendor invoice. However, this functionality is disabled when a process template is defined, provided the Process Management solution is in use.

Additionally, you can navigate to the linked ledger journal or pending vendor invoice, where you can create, edit, and delete invoice lines. However, posting the invoice is only possible if the totals are matched.

<figure><img src="../../../.gitbook/assets/image (99).png" alt=""><figcaption></figcaption></figure>



**Enhancements 10.2022.5.1 Release**

In the 10.2022.5.1 release, three new enhancements have been introduced for Vendor Invoice Journals:

1. **Merge Financial Dimensions:**\
   The financial dimensions of the vendor can now be merged with the financial dimensions of the main accounts. Previously, this was only possible for the offset account in standard FO, but it is now supported for the account itself.
2. **Account Type Default to Ledger:**\
   When adding new lines in the Invoice Journal, the account type is automatically set to "Ledger." It's important to note that the first line must be of type "Ledger" before you can create additional lines.
3. **Filter Default Main Accounts:**\
   The dropdown menu for main accounts is now filtered based on the selected vendor. While this functionality already existed in standard FO for the offset account, it is now available for the account as well. The filtered dropdown identifies the first account of type "Vendor" to list all applicable default accounts

### Info parts <a href="#info-parts" id="info-parts"></a>

**Purchase Invoice Totals:**\
This section validates the matching between an imported invoice and the corresponding ledger journal or pending vendor invoice. Posting an imported invoice is only possible if there are no discrepancies.

* If the invoice has not been posted, the amounts displayed come from the ledger journal or pending vendor invoice.
* Once the invoice is posted, the amounts are sourced from the Vendor Invoice Journal.



<figure><img src="https://docs.raptor.9altitudes.com/~gitbook/image?url=https%3A%2F%2F3857075213-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FKfypi8e8luNHtfjQhy6p%252Fuploads%252FwnQgssfn4TSeUPojjGCP%252Fimage.png%3Falt%3Dmedia%26token%3Da817f3cc-f506-4190-a808-6d528ae7400c&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=feba68ca&#x26;sv=2" alt=""><figcaption></figcaption></figure>

**Purchase Invoice References:**\
Displays all linked purchase orders associated with an imported invoice.

<figure><img src="https://docs.raptor.9altitudes.com/~gitbook/image?url=https%3A%2F%2F3857075213-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FKfypi8e8luNHtfjQhy6p%252Fuploads%252FP3zDCBsl8HliqXgGYS7z%252Fimage.png%3Falt%3Dmedia%26token%3D15c15491-7c20-4178-800e-ec4e38a8ed47&#x26;width=300&#x26;dpr=4&#x26;quality=100&#x26;sign=797103ad&#x26;sv=2" alt=""><figcaption></figcaption></figure>

***

## **Purchase Orders**

There are two fields that should be populated from the E-Platform, where integration with purchase orders is possible:

1. **Is a Purchase Order (EXAPurchInvoiceImported.IsPurchaseOrder):**\
   This field is used to execute specific rules when the imported invoice is linked to a purchase order. It is automatically set to _true_ by Ephesoft, Kofax, or the E-Platform.
2. **Is a Prepayment Invoice (EXAPurchInvoiceImported.IsPrepaymentInvoice):**\
   This field enables the execution of specific rules when the imported invoice is linked to a prepayment for a particular purchase order. Like the previous field, it is also set to _true_ by Ephesoft, Kofax, or the E-Platform.
