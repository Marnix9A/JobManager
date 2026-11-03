---
description: >-
  This document provides an overview on how to extend the most Important
  components of Document Management.
---

# Document Management

## 1.    Extending document distribution as customization with custom entities

### 1.1.    Extend enum EXADocuEntityType with the custom entities

Start by adding the entities you want to add as a type in an extension of the 'EXADocuEntityType' base enum. As an example, an entity called 'NewEntity' was added to the enum, make sure your naming makes sense for your entity (see the other standard examples).

<figure><img src="../../.gitbook/assets/image (321).png" alt=""><figcaption></figcaption></figure>

### 1.2.    Extend table EXADocuDistributionTable

Here we extend the 'EXADocuDistributionTable' table. This Is so we can map the D365 FO tables to the entity type we added in the previous section.

```
[ExtensionOf(tableStr(EXADocuDistributionTable))]
internal final class EXADocuDistributionTable_Table_ADU_Extension
{
    public static EXADocuEntityType convertCommonToEntityType(Common        _common)
    {
        EXADocuEntityType       entityType;
        ;

        entityType = next convertCommonToEntityType(_common);

        if(entityType == EXADocuEntityType::None)
        {
            switch(_common.TableId)
            {
                case tableNum(NewEntityTable)
                    entityType = EXADocuEntityType::NewEntity;
                    break;
            }
        }
    }

    public static RefTableId convertEntityTypeToTableId(EXADocuEntityType _docuEntityType)
    {
        RefTableId      refTableId;
        ;

        refTableId = next convertEntityTypeToTableId(_docuEntityType);
        if(!RefTableId)
        {
            switch(_docuEntityType)
            {
                case EXADocuEntityType::NewEntity
                    refTableId = tableNum(NewEntityTable);
                    break;
            }
        }
    }
}

```

### 1.3.    Implementation of the distribution

In this next step, we will add the actual distribution of the documents to the pieces of code where we want them to get distributed. Usually it will be a piece of code that you need to call when you insert new records, like with the creation of for example a purchase order line.

As an example, we'll have a look at how to copy documents from an item to your newly made purchase order line. You need to call the class 'EXADocuDistributionManager' with 2 parameters; your 'From' record (in this example the table 'InventTable'), and your 'To' record (in this example the table 'Purchline')

```
[ExtensionOf(classStr(PurchLineType))]
public final class PurchLineType_Class_EXADocu_Extension
{
    public void inserted()
    {
        ;

        next inserted();

        this.exaDistributeDocuments();
    }
    /// <summary>
    /// Distribute documents from released product entity to purchase order line entity
    /// </summary>
    public void exaDistributeDocuments()
    {
        Common      commonFrom;
        ;

If(isConfigurationKeyEnabled(configurationKeyNum(EXARaptorDocuMgmt)) == true && EXADocuDistributionManager::canDistributeOnPurchLine(this.parmPurchLine()) == true)
       {
       	    commonFrom = this.parmPurchline().inventTable();

	    if(commonFrom.RecId != 0 && this.parmPurchLine().RecId != 0)
	    {
EXADocuDistributionManager::distributeFromEntityToEntity(commonFrom, this.parmPurchLine());
    }
       }
    }
}

```

## 2. Code snippets

### 1. Get a tag based on a record

This method allows you to get the tag that's based on the given record.

```
EXARaptorTagModelDC tagModelDC = EXADocuHelper::findOrCreateTag(_commonRecord);
```

### 2. Get all documents based on a query setup (tags + document template)

This code allows you to get all documents based on a query setup, filtering by tags and document template:

```
public List getListOfDocuments(common _commonRecord,
                                EXARaptorTemplateModelDC _templateModelDC)
{
    List listTagsAsString = EXADocuHelper::findOrCreateTagAsList(_commonRecord);
    EXARaptorMetaQueryExpressionDC metaQueryExpressionDC = EXADocuHelper::getQueryExpressionForDocumentTemplate(_templateModelDC.parmId());

    return EXADocuHelper::getListOfDocuments(listTagsAsString, metaQueryExpressionDC);
}
```

### 3. Get all physical documents from tags or documents

This code shows how to get a list of physical documents based on a list of tags (type EXARaptorTagModelDC).

```
/// <summary>
/// Get all attachments based upon tags
/// </summary>
/// <param name = "_listTags">A list of object EXARaptorTagModelDC with all tags</param>
/// <returns>A list of object EXADocumentAttachment with all attachments (filename + extension / byte array) </returns>
protected List initAttachmentsFromTags(List _listTags)
{        
    List listTagAsString, listTagDocuments, listTagAttachments;

    listTagAsString     =   EXADocuHelper::convertTag2Str(_listTags);
    listTagDocuments    =   EXADocuHelper::getListOfDocuments(listTagAsString);             // get all documentIds based upon tagIds
    listTagAttachments  =   EXADocuHelper::getListOfPhysicalDocuments(listTagDocuments);    // get all physical documents based upon documentIds

    return listTagAttachments;
}
```

If you already have a list of documents (type EXARaptorDocumentDC), you can instead immediately call the method like so:

```
/// <summary>
/// Get all attachments based upon documents
/// </summary>
/// <param name = "_listDocuments">A list of object EXARaptorDocumentDC with all documents</param>
/// <returns>A list of object EXADocumentAttachment with all attachments (filename + extension / byte array) </returns>
protected List initAttachmentsFromDocuments(List _listDocuments)
{        
    List listTagAttachments;
    
    listTagAttachments  =   EXADocuHelper::getListOfPhysicalDocuments(_listDocuments);    // get all physical documents based upon documentIds

    return listTagAttachments;
}
```

### 4. Tag all documents with additional tags

This method will tag all of the documents that are tagged with the commonFrom record tag and add the commonTo record tag to it, for example adding the tag of a sales order to all documents that are already tagged by a purchase order.

```
EXADocuHelper::addTagsFromToDocuments(_commonFrom, _commonTo);
```

### 5. Archive a document

This method will allow you to archive a document, which means uploading it to the document warehouse, resolving the tags and attaching the tags and template (if applicable) to the uploaded document. If successful, it will return true, if not false.

```
EXADocuHelper::archiveDocument(_common, _documentAttachment, _documentTemplateId);
```

Another method you can use to archive is the following:

```
EXADocuHelper::ArchiveDocumentReturn(_common, _documentAttachment);
```

This method will return the document (type EXARaptorDocumentDC) instead of true/false, regardless of whether the tagging with tags or template succeeded. Warnings will of course still be thrown to show that the tagging failed.

### 6. Full process of making a tag, retrieving all documents and tagging them with the new tag

```
/// <summary>
/// Way of working to add CommonTo record tag to the corresponding documents where it's marked with CommonFrom record tag
/// </summary>
/// <param name = "_commonFrom">Common record like SalesTable record</param>
/// <param name = "_commonTo">Common record like CustConfirmJour record, CustInvoiceJour record,...</param>
public static void addTagsFromToDocuments(  Common          _commonFrom,
                                            Common          _commonTo)
{
    EXARaptorTagModelDC         tagModelFrom, tagModelTo;
    List                        listTags;

    tagModelFrom    =   EXADocuHelper::findOrCreateTag(_commonFrom);
    tagModelTo      =   EXADocuHelper::findOrCreateTag(_commonTo);

    if(tagModelFrom                 !=  null 
        &&  tagModelTo              !=  null
        &&  tagModelFrom.parmId()   !=  '' 
        &&  tagModelTo.parmId()     !=  ''
        &&  tagModelFrom.parmId()   !=  tagModelTo.parmId())
    {   
        listTags = new List(Types::Class);
        listTags.addEnd(tagModelFrom);

        List listTagAsString    =   EXADocuHelper::convertTag2Str(listTags);
        List listTagDocuments   =   EXADocuHelper::getListOfDocuments(listTagAsString);
        ListEnumerator listEnumerator = listTagDocuments.getEnumerator();

        while(listEnumerator.moveNext())
        {
            EXARaptorDocumentDC raptorDocument = listEnumerator.current();

            if(raptorDocument.parmId() != null)
            {
                EXADocuHelper::tagDocumentByTag(tagModelTo, raptorDocument.parmId());
            }
        }
    }
}
```
