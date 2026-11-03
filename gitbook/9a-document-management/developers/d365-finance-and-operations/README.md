# D365 Finance & Operations

## Code snippets

### 1. Tag selector

With this code snippet, It Is possible to open the tag field selector dialog from a formdatasource extension.

```
[ExtensionOf(formDataSourceStr(form, formdatasource))]
public final class Form_FormDataSource_FDS_CustomerModel_Extension
{
    public void init()
    {
        EXADocuTagSelectorExtensionOverrides docuTagSelectorExtensionOverrides;
        ;
 
        next init();
        docuTagSelectorExtensionOverrides = EXADocuTagSelectorExtensionOverrides::construct();
        docuTagSelectorExtensionOverrides.common = this.cursor();
        docuTagSelectorExtensionOverrides.documentTagFieldId = fieldNum(Table, FieldTag);
 
        this.object(fieldNum(Table, FieldTag)).registerOverrideMethod(  methodstr(FormStringControl, lookup),                                                                        methodStr(EXADocuTagSelectorExtensionOverrides, documentTag_OnLookup),                                                                        
        docuTagSelectorExtensionOverrides);
    }
}
```





### 2. HTTP request - production order attachments

Here's an example on how to pass a documentId from the Document Warehouse to D365FO for a production order:

·        https://d365fo-environment.cloudax.dynamics.com/data/EXAProdTableAttachments

·        HTTP verb: POST

·        Body: JSON

&#x20;

Example JSON body

```
{
"dataAreaId": "FRRT", to find it in the tags of your document
"TypeId": "DOC_WAREHOUSE", // depends from customer to customer
"Name": "document.pdf",
"FileName": "document",
"FileType":"pdf",
"ProdId":"000006", // to find it in the tags of your document
"EXADocumentId": "d739d37a-77c9-44c7-b822-715a06f95752" // documentId of document in Document Warehouse
}
```
