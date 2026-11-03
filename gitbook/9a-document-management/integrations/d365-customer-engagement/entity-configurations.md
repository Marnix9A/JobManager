---
description: >-
  This article describes the Entity Configurations tab in the Raptor
  Configuration app.
---

# Entity Configurations

The Entity Configuration tab allows you to configure the Raptor Document Warehouse per entity.\
It allows you to:

* Make the Document Warehouse available via a button on your entity records
* Make the Document Warehouse available via a tab on your entity records
* Set up entity configuration to create tags
* Determine if note attachments and or emails added to the entity should be stored in Raptor

To create an Entity Configuration click the '+ New' button. \
A form will appear with the following parameters:

## General

**Entity Name**: choose your entity you wish to setup Raptor for from the dropdown.

**Entity Logical Name**: the logical name of your entity. This field will be automatically filled in.

**Entity Code**: the numeric code of your entity. This field will be automatically filled in.

**Delta Migration**: determines if records for this entity should be exported as a delta (= Yes) or as a full export (= No) when using the entity in a Data Sync Job.

### Note Configuration

**Transfer to Raptor**: determines if note attachments made on this entity should be automatically uploaded to Raptor.

**Delete Notes in CE**:

* No Delete in CE: Upload to Raptor but keep the document stored in Dataverse
* Delete Completely in CE (No Trace of the Annotation): Upload to Raptor and remove the annotation from the timeline
* Delete Only Data in CE (Keep Annotation Relation): Upload to Raptor and keep the annotation in the timeline

### E-mail/Appointment Attachment Configuration

**Transfer to Raptor:** determines if e-mails and appointments should be automatically uploaded to Raptor.

**Status of Emails to Transfer**: determines the status of e-mails that should trigger an upload to Raptor. Multiple statusses are possible (e.g. Received and Sent).

**Delete Attachments in CE (Only Inactive Records)**:

* No Delete in CE: Upload to Raptor but keep the email attachment stored in Dataverse
* Delete Completely in CE (No Trace of the Attachment): Upload to Raptor and remove the email attachment from the timeline
* Delete Only Data in CE (Keep Attachment Relation): Upload to Raptor and keep the email attachment in the timeline

**Supported Extensions ; separated (If empty = Everything)**

Optional, allows you to specify which attachment filetypes should be uploaded to Raptor. Filetypes not in this list will stay in Dataverse. If the field is left empty, all filetypes will be uploaded.

Example: pdf;docx;pptx;xlsx

**Minimum File Size in Bytes (If empty = everything)**

Optional, allows you to specify what the minimum size should be for an e-mail attachment to be uploaded to Raptor (specified in bytes). If the field is left empty, all sizes will be uploaded.

**Save E-mail as EML**: determines if emails should be stored in full as an EML file in Raptor.

* Do Not Save as EML: don't store the full email
* Received E-mails: store only received emails (inbound)
* Sent E-mails: store only sent emails (outbound)
* Received and Sent E-mails: store both received and sente mails (inbound + outbound)

## Attachment Manager Settings

**Parent Tag Ids for Tags Column (;separated)**: this field allows you to add extra columns to the Attachment Manager populated with Raptor tags. This can be done by specifying the parent tag ID's in a semicolon-separated way.&#x20;

**Extra Field Column**: allows you to add a Raptor field as a column to the Attachment Manager (value should be the field code).

**Columns to Hide** **(; separated)**: allows you to hide columns in the Attachment Manager by specifying their names in a semicolon separated way.

**Default Sort Column**: allows you to specify the name of the column which should be sorted on by default in the Attachment Manager

## Entity Forms

If the Development setting is enabled in the [environment-setup.md](environment-setup.md "mention"), this section will allow you to publish Raptor tabs to your forms. To add a tab to a form, change the 'Ex Arte Document List' value to 'Yes'.

## Entity Fields

The Entity Fields section allows you to define the fields that should be sent to Raptor to resolve tags using the Raptor Entity Configuration. See [entity-configuration.md](../../raptor-document-warehouse/configuration/entity-configuration.md "mention").

## Entity Foreign Fields

The Entity Fields section allows you to define the foreign fields to resolve tags using the Raptor Entity Configuration. See [entity-configuration.md](../../raptor-document-warehouse/configuration/entity-configuration.md "mention").





