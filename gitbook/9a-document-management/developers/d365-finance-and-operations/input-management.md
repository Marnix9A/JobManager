---
description: >-
  This document provides a technical overview regarding the Input Management
  solution.With this documentation it should be possible to create new rules and
  how to integrate the module with other externa
---

# Input Management

## 1.    Invoice setup rule engine

### 1.1.    Base objects

All base objects will be described in this chapter to give you an idea which objects should be changed or extended for custom rules.

* Base enum **EXAPurchInvoiceActionStrategy** (is extensible)
* Class **EXAPurchInvoiceStrategyField** : to handle UI actions like lookup in the Invoice Setup form
* Class **EXAPurchInvoiceStrategy** : to execute custom logic based upon the defined strategy

It’s important that every rule have two classes for the UI actions and executing custom logic.

### 1.2.    Use EXAPurchInvoiceStrategyField

The base object EXAPurchInvoiceStrategyField is a way to handle the UI actions in the Invoice Setup form. With this class you can bind a field from the table EXAPurchInvoiceImported with a specific class. You can find a list with all possibilities below.

* Bind a field from table EXAPurchInvoiceImported
* Bind the field with a base extended data type (if you want use standard lookup)
* Define which value should be displayed in the Invoice setup form
* Decide or the value can be edited
* Decide or the selected value should be validated
* Use custom lookup

Every child of this base class have an attribute of type EXAPurchInvoiceStrategyFieldAttribute. You can define an enum value in this attribute. Via this way we can bind the enum values with the used classes.

```
[EXAPurchInvoiceStrategyFieldAttribute(EXAPurchInvoiceActionStrategy::SetInvoicePaymentRelease)]
public class EXAPurchInvoiceStrategyField_SetInvoicePaymentRelease extends EXAPurchInvoiceStrategyField
{

}
```

Please look to the existing implementations to give you an idea how to implement this class.

* Custom lookups : **EXAPurchInvoiceStrategyField\_SetJournalName**
* Standard lookups : **EXAPurchInvoiceStrategyField\_SetApprover / EXAPurchInvoiceStrategyField\_SetInvoiceType**
* Empty classes – no specific UI actions : **EXAPurchInvoiceStrategyField\_SetInvoiceData**

### 1.3.    Use EXAPurchInvoiceStrategy

This base object EXAPurchInvoiceStrategy is a way to execute custom logic during the import of invoices. It’s possible to update one field in the table EXAPurchInvoiceImported as pre-action so this field can be used to update a LedgerJournalTable record or a VendInvoiceInfoTable record. Also you can write code to have a post-action like as trigger a business event.

```
[EXAPurchInvoiceStrategyAttribute(EXAPurchInvoiceActionStrategy::SetJournalName)]
public class EXAPurchInvoiceStrategy_SetJournalName extends EXAPurchInvoiceStrategy
{

}

```

Please look to the existing implementations to give you an idea how to implement this class.

* Update a field based upon the strategy field : **EXAPurchInvoiceStrategy\_SetApprover**
* Execute custom logic : **EXAPurchInvoiceStrategy\_SetBusinessEvent**

### 1.4.    How to start with development

1. Create an extension based upon base enum EXAPurchInvoiceActionStrategy
2. Create a new class based upon EXAPurchInvoiceStrategyField
3. Create a new class based upon EXAPurchInvoiceStrategy
4. To be sure, refresh the AOT elements with class EXAPurchInvoiceFlushAOD

## 2.    Public endpoints

The existing data entity EXAPurchInvoiceImportedEntity – imported invoice headers entity include public endpoints for external OData integration with external systems. You need to select an existing imported invoice before calling these public endpoints.

Method **approvePayment**

* 2 parameters
  * parameter **transDate**
  * parameter **userId** (existing userId / if it’s blank the current user will be used)
* purpose: to approve the payment for the existing imported invoice

Method **approvePaymentV2** (same principle as approvePayment but with a personnel number)

* 2 parameters
  * parameter **transDate**
  * parameter **personnelNumberId**
* purpose: to approve the payment for the existing imported invoice with a personnel number instead of userId

Method **getUrl**

* no parameters
* purpose: get the URL so we can navigate to the existing invoice from external system

Method **finishImport**

* no parameters
* purpose: calling it from the E-Platform and let D365FO know that the whole import of an imported invoice is finished

Method **checkIfMatchedStatus**

* no parameters
* purpose: to validate or the pending vendor invoice is matched based upon standard D365FO parameters. It will return a true if the whole pending vendor invoice is matched.

Method **postInvoice**

* no parameters
* purpose: to post the existing Imported Invoice
* returns a true as boolean when the Invoice Is posted

Example: [https://_d365fo-environment_.cloudax.dynamics.com/data/PurchInvoiceImporteds(DocNo=’XXX’,dataAreaId=’XXX’)/Microsoft.Dynamics.DataEntities.approvePayment](https://d365fo-environment.cloudax.dynamics.com/data/PurchInvoiceImporteds\(DocNo=%E2%80%99XXX%E2%80%99,dataAreaId=%E2%80%99XXX%E2%80%99\)/Microsoft.Dynamics.DataEntities.approvePayment)

These public endpoints are available only in combination with the Process Management solution:

Method **cancelProcess**

* no parameters
* purpose: to cancel current process of the linked invoice

## 3. Custom fields

For the imported invoice header and imported invoice lines we have custom fields. Via this way we can save extra values from Ephesoft/Kofax/E-Platform in D365FO without developing extra fields.

Used data entities:

* EXAPurchInvoiceImportedFieldsEntity – imported invoice fields headers entity
  * DocNo
  * FieldName
  * FieldValue
* EXAPurchInvoiceLineImportedFieldsEntity – imported invoice fields lines entity
  * DocNo
  * LineNum
  * FieldName
  * FieldValue

At this moment we have three supported custom fields for the imported invoice header:

* STRUCTURED\_PAYMENT
  * Payment Id for the ledger journal transaction lines
  * Payment Id for the pending vendor invoices
* TRANSACTION\_TXT
  * Transaction text for the ledger journal transaction lines
  * Invoice description for the pending vendor invoices
* BUYER\_VAT\_NUMBER
  * Buyer VAT number from Kofax
  * Used to execute specific actions In the Invoice rule setup

## 4.    Business event integration

The Input Management solution has one business event that can be triggered from the rule engine. For a functional overview regarding the rule engine – you can read the functional documentation about the Input Management solution.

The current schema include these fields for the integration:

* VendorAccount: table EXAPurchInvoiceImported – field VendAccount
* DocumentNumber: table EXAPurchInvoiceImported – field DocNo
* InvoiceAmount: table EXAPurchInvoiceImported – field InvoiceAmount
* CurrencyCode: table EXAPurchInvoiceImported – field CurrencyCode
* InvoiceType: table EXAPurchInvoiceImported – field InvoiceType\
  (enum symbol – None, InvoiceJournal, InvoiceRegister, PendingInvoice)
* DebitCredit: table EXAPurchInvoiceImported – field DebitCredit\
  (enum symbol – Debit, Credit)
* InvoiceStatus: table EXAPurchInvoiceImported – field InvoiceStatus\
  (enum symbol – Imported, Posted, Finished, Registered, Matched, Canceled)
* InvoiceId: table EXAPurchInvoiceImported – field InvoiceId
* JournalNum: table LedgerJournalTable – field JournalNum (relation between imported invoice and ledger journal)
* TableRefId: table VendInvoiceInfoTable – field TableRefId (relation between imported invoice and pending vendor invoice)
* LegalEntity: table EXAPurchInvoiceImported – field DataAreaId

## 5.    Power Automate integration

The Input Management solution provide new data entities for the integration between imported invoices and pending vendor invoices. The public collection names are listed in the list below.

### 5.1.    Public collection names:

* EXAVendInvoiceInfoTables: pending vendor invoice header
* EXAVendInvoiceInfoSubTables: linked purchase orders for a pending vendor invoice
* EXAVendInvoiceInfoLines: lines of a pending vendor invoice
* EXAVendInvoiceInfoSubLines: linked product receipt info for a pending vendor invoice line

### 5.2.    How to execute it with Power Automate?

Get pending vendor invoice

* https://URL/data/EXAVendInvoiceInfoTables?$filter=TableRefId eq '010691'\&dataAreaId eq 'frrt'\&cross-company=true

Get purchase orders of a pending vendor invoice

* https://URL/data/EXAVendInvoiceInfoSubTables?$filter=TableRefId eq '010691'\&dataAreaId eq 'frrt'\&cross-company=true

Get lines of a pending vendor invoice

* https://URL/data/EXAVendInvoiceInfoLines?$filter=TableRefId eq '010691'\&dataAreaId eq 'frrt'\&cross-company=true

Get product receipt info of all lines for a pending vendor invoice

* https://URL/data/EXAVendInvoiceInfoSubLines?$filter=TableRefId eq '010691'\&dataAreaId eq 'frrt'\&cross-company=true

The value TableRefId can retrieved on two different ways:

* Get the value TableRefId from the entity EXAPurchInvoiceImporteds (imported invoice headers)
* Get the value TableRefId from the business event contract (chapter 6)

General advice:

Use keyword select so only used fields are retrieved instead of the whole record

* https://URL/data/EXAVendInvoiceInfoTables?$select=TableRefId&$filter=TableRefId eq '010691'\&dataAreaId eq 'frrt'\&cross-company=true

## 6.    Process management integration

For the AgilePoint NX integration – we will send a list of custom attributes to AgilePoint. Via this way AgilePoint NX can take actions based upon the custom attributes.

Hereby a fixed list with all existing custom attributes:

* ErpUrl: root URL of your D365FO environment
* EntityName: entityname of the current record
* PublicEntityName: public entityname of the current record
* PublicCollectionName:  public collection name of the current record
* TableName: tablename of the current record
* RecId: recId value of the current record
* RaptorResolveContextJSON: resolve context object for Document Warehouse
* ErpUrlEntity: whole URL where you can navigate to the current record
