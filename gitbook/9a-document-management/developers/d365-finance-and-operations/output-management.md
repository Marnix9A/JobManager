---
description: >-
  This document provides an overview how to integrate custom reports with the
  Output Management solution.
---

# Output Management

## 1.    Custom reports development

### 1.1.    Supported reports

Hereby an overview of which reports are supported within our Output management solution.

* Reports without report contract
  * **Unsupported**
* Reports with report contract, without report data provider (DP class). In other words reports with a Query as data source.
  * **Supported (= starting from release 10.2023.9.1)**
* Reports with report contract, with report data provider in combination with a journal & transaction structure. In other words as is the case for commercial documents such as sales order confirmation, sales invoice, purchase order confirmation and so on.
  * ReportDataProviderBase (tables of type InMemory)
    * **Supported**
  * ReportDataProviderPreProcess (tables of type Normal)
    * **Supported**
  * ReportDataProviderTempDB (tables type TempDB)
    * **Supported**
* Reports with report contract, with report data provider, without a journal & transaction structure. This is the case for many non-commercial documents that are not related to any posting: HR reports, production reports and so on. But there are some limitations as no automatic archiving, no document title / proforma information are available. If you want to use these advantages, then you can check chapter 3.2.
  * ReportDataProviderBase (tables of type InMemory)
    * **Supported**
  * ReportDataProviderPreProcess (tables of type Normal)
    * **Supported**
  * ReportDataProviderTempDB (tables type TempDB)
    * **Supported**

### 1.2.    Delegates

#### 1.2.1    How to pass the document title and the record Id information?

* Create a data contract with as DataContractAttribute as attribute
* Make sure two parm methods exists in your data contract
  * parmRecordId
  * parmDocumentTitle
* Create an event handler (or copy the original method from EXAPrintReportRecordSelector class – method getFromContractDelegate)

```
/// <summary>
/// To pass the values to the event and retrieve the record Id of the header and the document title but not necessary
/// </summary>
/// <param name="_dataContract">the current data contract</param>
/// <param name="_result"> Object of type EventHandlerResult with a container with a RecId and a documentTitle values</param>
[SubscribesTo(classStr(EXAPrintReportRecordSelector), delegateStr(EXAPrintReportRecordSelector, getFromContractDelegate))]
public static void EXAPrintReportRecordSelector_getFromContractDelegate(Object _dataContract, EventHandlerResult _result)
{
RecId           recId;
        str             documentTitle;
        ;
        if(_dataContract is EXAReportExampleDataContract)
        {
            EXAReportExampleDataContract dataContract = _dataContract;
            recId           =   dataContract.parmRecordId();
            documentTitle   =   dataContract.parmDocumentTitle();
        }

        if(_result.hasResult() == false
           && (documentTitle != '' || recId != 0))
        {
           _result.result([recId, documentTitle]);
        }
}
```

#### 1.2.2    How to pass the proforma information?&#x20;

You need to validate if the common object can be converted to your table. \
Via this function, you can decide if it’s a proforma or an effective posting.

```
/// <summary>
/// To pass proforma information from your custom report datasource to Ex Arte Raptor Output Management
/// </summary>
/// <param name="_common">the linked record</param>
/// <param name="_result">Object of type EventHandlerResult with a boolean as result</param>
[SubscribesTo(classStr(EXAPrintReportRecordSelector), delegateStr(EXAPrintReportRecordSelector, getProformaFromRecord))]
public static void EXAPrintReportRecordSelector_getProformaFromRecord(Common _common, EventHandlerResult _result)
{
        // Do something with the _common object and convert to your table
        // Pass the proforma information to the object _result of type EventHandlerResult
        // We expect a boolean as result value, make sure to verify if this is filled in another event already or not.

        boolean setupFound, isJournalProforma;

        switch(_common.TableId)
        {
           //In this example, we make sure to pass proforma information for WHSLoadTable
            case tableNum(WHSLoadTable):
                setupFound = true;
                isJournalProforma = false;
                break;
        }

        if(_result.hasResult() == false && setupFound == true)
        {
            _result.result([isJournalProforma]);
        }
}
```

## 2.    Business event integration

The Output management solution has one business event that can be triggered when an Ex Arte print destination is chosen during generation of a document. Please keep In mind the current schema can be extended with extra fields If possible but It's Important the payload should be small.

The current schema include these fields for the integration:

* Filename: generated filename of the document
* DocumentTemplate: table EXAReportSetup – field DocumentTemplate
* TableNamePrimary: table EXAReportSetup – field PrimaryTableName
* ReportSetupId: table EXAReportSetup – field ReportSetupId
* ReportName: table EXAReportSetup – field ReportName
* ReportRefLegalEntity: table EXAReportSetup – field RefCompanyId
* ReportProvider: table EXAReportSetup - field Provider\
  (enum symbol – SSRS, dox42, SmartFlows, Electronic Reporting)
* TableName: table name behind the linked record
* RecId:record Id behind the linked record
* PrintMediumType: selected print destination\
  (enum symbol – Ex Arte Archive, Ex Arte Screen, Ex Arte Printer, Ex Arte Email, Ex Arte Email interactive, Ex Arte E-Platform)
* LegalEntity: current legal entity where the report Is generated

## 3.    Email distribution framework

It's recommend to read the functional part before starting with this chapter. This chapter only includes technical instructions regarding how to extend the email distribution framework. Also, the Important enumerations are extensible as well.

### 3.1.    Data structure

#### 3.1.1    Events

* Base enumerations
  * Sender type: EXAEmailDistributionSenderType
  * Recipient type: EXAEmailDistributionRecipientType
  * Event type: EXAEmailDistributionEventType
* Table relations
  * Recipient relation: enforce It with a table relation In table extension

<figure><img src="../../.gitbook/assets/image (693).png" alt=""><figcaption></figcaption></figure>

#### 3.1.1.    Event groups

Create an event group In your table (CustTable, VendTable, SalesTable, …) based upon extended data type EXAEmailDistributionEventGroupId and create a foreign key relation to table EXAEmailDistributionEventGroup.

### 3.2.    Business logic

#### 3.2.1    Class based upon a new event type

This is a class based upon a new event type based upon attribute EXAEmailDistributionEventHandlerAttribute. Important is to mention the right event type that you've created earlier. Add new methods to execute extra logic if possible.

<figure><img src="../../.gitbook/assets/image (694).png" alt=""><figcaption></figcaption></figure>

#### 3.2.2    Code snippet to trigger a specific event type in combination with an event group

1. Create an object of type EXAEmailDistributionEventHandlerContract to provide a common record like SalesTable, an event type and a dirPartyRecid as optional parameter.
2. Call the event handler class with the created contract and trigger a specific event group.

<figure><img src="../../.gitbook/assets/image (695).png" alt=""><figcaption></figcaption></figure>
