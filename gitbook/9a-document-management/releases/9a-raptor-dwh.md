---
hidden: true
---

# 9A Raptor DWH

{% hint style="info" %}
Release notes can now be found on the [9altitudes release notes website](https://releasenotes.9altitudes.com/9A%20Productivity%20Suite/9A%20Raptor%20Document%20Warehouse/CurrentSprint/)!
{% endhint %}

## July 2025

**16234**

* **Title**: External documents in 9A Raptor Document Warehouse are now copied correctly to the standard storage provider (Azure Blob Storage).
* **Type**: Bug
* **Notes**: By using the copy document function, via de 9A Raptor Document Warehouse API, for a external document it will copy now the external document and store it to the standard Azure Blob Storage account.

**15438**

* **Title**: New & improved email viewer for the 9A Raptor Document Warehouse.
* **Type**: User Story
* **Notes**: In the new email viewer the body of the document is now shown as html, as in Microsoft Outlook .

**16102**

* **Title**: Newly added documents are taken into account when sorting on documents after a keyword search.
* **Type**: Bug
* **Notes**: When sorting in the document list of the 9A Raptor Document Warehouse, after a keyword search, newly added documents are now correctly sorted.

**15844**

* **Title**: In the viewer of 9A Raptor Document Warehouse word documents containing table rows are now rendered correctly.
* **Type**: Bug
* **Notes**: Table rows in Word documents are now rendered correctly in the document viewer of the 9A Raptor Document Warehouse.

**14588**

* **Title**: As a key user you can now create advanced queries where you can select multiple tags in one expression.
* **Type**: User Story
* **Notes**: As a key user you are now able to create advanced queries where you can create a single expression containing multiple tags and decide if one, all or none of the containing tags should be set as a criteria. This feature significantly reduces the number of expressions you need to add in a advanced query to result to the same query result.

**16145**

* **Title**: For every external system, not only the first, all users are shown without the need to refresh the list.
* **Type**: Bug
* **Notes**: In the administration module, for every external system the list of users will be made available immediately .&#x20;

## May 2025

System maintenance/performance update

## March 2025

**15540**

* **Title**: \[Recurring] Improve documentation
* **Release**: 2025.0.0.640
* **Type**: User Story
* **Notes** Reworked D365 Finance & Operations Output management documentation<br>

**15675**

* **Title**: SharePoint sync - not all drive changes processed|
* **Release**: 2025.0.0.640
* **Type**: Bug
* **Notes** A bug fix to include the missing changes for documents stored in a synced SharePoint Online collection.

## January 2025

**15214**

* **Title**: A placeholder icon and descriptive text/button is used as visual for Zip files in the Document Warehouse.|
* **Release**: 2024.0.0.634
* **Type**: User Story
* **Notes** As an end user when you select a Zip file you would get a thumbnail with the message "No Thumbnail Available", this is replaced by the following visual: ![Image](https://releasenotes.9altitudes.com/9A%20Productivity%20Suite/9A%20Raptor%20Document%20Warehouse/images/6cdd3be0-1a08-4745-8a03-7b0221f1170c.png).   In the viewer itself the end-user will now see the text "no viewer available (unsupported file format)" and a button to download the zip instead of the error message.<br>

**15420**

* **Title**: “Move document 2 SPO” endpoint|
* **Release**: 2024.0.0.634
* **Type**: User Story
* **Notes** A new endpoint is created, called "Upload-to-SharePoint" in the API gateway.  This enpoint allows smooth & optimized upload of documents from Raptor towards SharePoint Online without the Raptor synchronisation automatically recreation the document in Raptor after upload to SharePoint Online.

**15423**

* **Title**: Documentation refresh of D365FO Input management|
* **Release**: 2024.0.0.634
* **Type**: User Story
* **Notes** Reworked D365 Finance & Operations Input management documentation

**15458**

* **Title**: Enable email attachments to be added to Raptor with drag & drop (new outlook client)|
* **Release**: 2024.0.0.634
* **Type**: User Story
* **Notes** While drag & drop from an email from the new Outlook client towards the 9A Raptor Document Warehouse was already possible, you are now also able to do drag & drop an email attachments directly from he new Outlook client to 9A Raptor Document Warehouse.&#x20;

**15496**

* **Title**: Option to download files “inline”|
* **Release**: 2024.0.0.634
* **Type**: User Story
* **Notes** Provided a new query parameter in the endpoint GET /api/meta/document/{id}/content to indicate that you wish a response with the header ‘Content-Disposition: inline’.

**14865**

* **Title**: Upgrade viewer component to latest version, including fix for conversions to PDF|
* **Release**: 2024.0.0.634
* **Type**: Bug
* **Notes** General update of viewer component to latest version, including fix for incorrect conversions of documents to PDF.

## December 2024

* For the Tungsten AP Essentials master data sync job in the Document Warehouse administration module, the input of the external entity name for D365 F\&O data entities is made case insensitive to prevent incorrect setup.
* The following topics on the Online Documentation are revised:
  * D365 F\&O 9A Raptor Document Warehouse integration
  * D365 CE 9A Raptor Document Warehouse technical installation
* The document viewer in the 9A Raptor Document Warehouse now supports visualisation of webp images.
* As an end user, you are now able to search in the list of available columns to find the columns you want to add to your document list section (screenshot).
* In the role section of the administration module, the list of available roles is now extended to show more than 100 roles, if available.

## October 2024

* A completely new email viewer ensures a better user experience for viewing emails stored in 9A Raptor Document Warehouse. The new viewer provides mail header information such as From, To, CC, BCC, Subject and Sent at the top of the viewer. All attachments that were part of the email will be listed under the header section allowing smooth switching between email body and any of the attachments.
* For customers using on prem AX2012 solutions, the AP Essentials master data service is updated to make it more resilient.
* When changing the name of a file in SharePoint Online, the name of the corresponding Raptor document will be updated as well.
* Documents that were originally stored in SharePoint Online can now be detached from SharePoint Online. This action causes the underlying storage provider to change for that document from SharePoint Online to the default 9A Raptor Document Warehouse storage provider (Azure Blob storage).
* In the last release we made it possible to drag & drop documents in the 9A Raptor Document Warehouse from the new Microsoft Outlook client. From this release on the context (metadata) will be saved together with the documents.

## September 2024

* Purchase invoice attachment handling: When purchase invoices are processed with Tungsten AP Essentials and the purchase invoices images/PDF’s are stored in 9A Raptor Document Warehouse, this new functionality enables the archiving of the email received in Tungsten AP Essentials together with the purchase invoices. This email will contain the purchase invoice and all original attachments that were send together with the purchase invoices for processing. To enable this functionality on a customer tenant some updates will need to be make by the Raptor team.
* In the new Microsoft outlook client, the drag & drop functionality of 9A Raptor Document Warehouse was not possible anymore. From this release on you will be able again to direct drag & drop from the new Outlook client to the 9A Raptor Document Warehouse as you could from the old Outlook client.\
  This may require a (one time) approval to grant the Raptor application access to the mail box.

## June 2024

* The HTML to PDF conversion is updated to the latest version. This feature is used to render mails in the Document Warehouse as mails are converted to PDF to be able to show them in the viewer.
* When creating new SharePoint Online sites, the subscription is created faster now, if the SharePoint Online sync is setup on your tenant.
* In the user sync from Dynamics 365 Finance & Operations disabled users are now synced as well.
* The location of the status badge ‘incomplete’ & ‘new” moved.
* Improved health checks for all scheduled sync jobs.
* The Copilot integration in the 9A Raptor Document Warehouse is now available in Preview mode. This feature allows you to search for documents using large language models. In this feature it facilitates the conversion of written sentences into advanced queries allowing users to find back documents in an intuitive way.

## May 2024

* We decommissioned the old rendering engine, which was used for the generation of thumbnails, annotations, document viewer & PDF merge in our production platform . Any customer still on the old rendering engine functionality will automatically be switched to the newest version.
* Existing barcode reader functionality is replaced by the new generation. Any customer on the old functionality will automatically be switched to the new barcode reader functionality.
* The main search bar will now clearly indicate that the search criteria is based on text string or tags.
* Users can now add tags to multiple documents at once. By using the bulk edit button on the command bar, you can add one or more tags on the selected documents in the document viewer.

## April 2024

* The D365 F\&O kickstart package is updated to split shared data entities and entity specific data entities and small updates are performed to limit the list of existing synced fields and the relations in the entity configuration.
* The subscription management for SharePoint Online sites, who are synced with Raptor Document Warehouse, is refactored .
* The delta processing for the SharePoint Online integration is refactored to reduce the memory consumption.
* Improved Raptor API responses, the response will be more descriptive and user-friendly.

## February 2024

* The Raptor API is extended to allow a copy-document that includes meta data like the template to be copied with it.
* In function of the SharePoint Online synchronisation, the registration and activation of a SharePoint site are decoupled.
* In function of the SharePoint Online synchronisation, a retry mechanism is built to store pending storage requests for external documents even for instance a SharePoint site is temporary unavailable.
* User language will be taken from D365 Finance & Operations at initial synchronisation & improved mapping from languages in D365 Finance & Operations to language codes in Raptor.
* fix: When typing in a tag field, and then switching to a new document the typed text could still be visible. Those fields are now cleared when switching to different documents.
* fix: In the configuration module, all fields will now be loaded when creating a new security rule.
* fix: Missing translation for dynamics dates have been added.

## January 2024

* SharePoint integration should now subscribe to new sharepoint sites immeadiatly after adding the site to the configuration. (used to be done as part of the next scheduled refresh which could take a few hours)
* Users can now create (advanced) search queries that use dynamic search options for date fields (such as today, yesterday, tomorrow, last/previous x number of months…).
* Refresh of cached document images stored in SharePoint Online is triggered upon document updates.
* Fix: Specific Microsoft Outlook files are rendered correctly in document viewer.
* The grouping mechanism is optimized in case the first-level grouping has empty values.

##

## December 2023

* In the document viewer, next to saving best width/best height, also save whether the user choses one of the (most common) zoom levels like 50%, 25%, ..
* The Raptor API now allows an "add or update" for fields. Previously you first had to try to add the field, followed by an update if the add failed.
* Users will be able to share saved advanced queries when the user has a security role assigned (by an administrator) which contains the permissions to share advanced queries.
* In the configuration section the save button is made more visible & intuitive to make sure an admin does not forget to save the changes.
* fix: Search on empty text fields in the advanced queries, will now result in a correct document list content.
* fix: In the configuration section when the first job is selected no job details were displayed.

## November 2023

* Facilitate Raptor integration to provide full context & action buttons to document list for Tulip.
* User can save table settings such as columns, sorting & grouping per device linked to the context provided by the external system such as D365FO, CE, BC or any other solution where Raptor is integrated in.
* Users can now reset all personal settings for the current tenant
* Thumbnail panel will remain visible after switching documents
* fix: searches can now contain a “-“ in the searched value and still result a complete & correct search outcome.
* fix: Deleting tags will now be recursive if cascading tag relations is active.

## October 2023

* When relation for certain tags have changed, related tags on relevant documents will be updated/removed automatically, this feature is also better known as cascading tag relations. Tags will have an indication if a tag was manually added or via a relation, however this functionality will need to be activated by a 9A consultant.  if not, no change in behavior will be noticed.
* Via API calls files in the document warehouse can be zipped to allow grouped downloads of documents.
* A feature that allows 9A administrators to prep a new environment with the latest versions of the kickstart for Business Central integration. Other integrations will follow soon.
* Third-party cookies were blocked, preventing thumbnail to load.

## September 2023

* In the administration module the Role pane has been refactored to allow full CRUDD security principle (key user) in combination with tags.
* An code revision has been done to optimize tag indexation to limit unnecessary load on the production platform.
* All security related option are now also available in the advanced search pane for any key users.
* The default viewer in the Raptor solution will be changed for all users to the advanced document viewer as a first step to decommission the standard document viewer.
* Certain MSG file with attachments could not be rendered correctly in the advanced document viewer.
* In the key user interface on the Audit pane the correct translations of labels are shown.
* In document viewer some pptx documents were visualized as XML’s instead of PowerPoints.
* When adding grouping functionality to the document list and selecting “Exclude ungrouped documents”, this functionality now also persistent on third level of grouping.



## July 2023

Most important new features & changes are:

* Searching in the top bar of the Document Warehouse screen will now show the tree view for each tag that has been found, giving the user a better insight on what tags are found (see image 1).
* Optimization of the group by functionality in the document list. The grouping feature was moved to a separate tab and now allows users to choose whether they want to see documents that do not belong to any of the selected “group by levels”. This allows for a more compact view of the grouped document list (see image 2).
* EMF files (emails) are now rendered correctly in the advanced document viewer.
* The Raptor sync with SharePoint Online can now act now a deletion & restore action in SharePoint Online.
* Extra database usage insights on tenant level will become available internally to give more in depth info related to CosmosDB usage.

## June 2023

Most important new features & changes are:

* First steps in the deployment of the Advanced Security functionality. In this release we added the functionality to allow administrators to predefine and re-use security conditions. Those conditions can be created in a similar fashion as an advanced search and already be used in the current security rules which can be composed in the role tab.
* Raptor users are now able to play MP4 recordings in the Document viewer.
* Per tenant, the default viewer can be set to migrate from standard viewer to advanced viewer (feature flag).

## May 2023

Most important new features & changes are:

* A new update of our Microsoft Teams integration is now available, allowing more context settings to fit the document viewer to the specific Teams channel (see screenshot).
* The document viewer will now use specific XML viewer instead of image viewer to render XML files.
* In the Document Warehouse, when an event is triggered next to the tag id’s the parent tag/hierarchy is now also included in the event to allow more efficient filtering on relevant documents to process.
* A new trigger is created in the Document Warehouse to launch an event when the location of a document is changed.
* The Convert2PDF function now supports also XLS files as base file.
* When selecting templates in a dropdown they will now be sorted alphabetically.

## April 2023

Most important new features & changes are:

* Update of “Cortex”, 9A Artificial intelligence solution:
  * Add queueing mechanism to analyse/classify documents;
  * Add field mapping for field recognition.
* Refactored render service, Document viewer and PDF manipulation tools:
  * Add new document viewer as alternative to existing viewer.
  * Add setting to switch between viewers on key user level(via preferences --> view ---> advanced viewer (Preview)).
  * As part of the new document viewer we have to functionality to search in a specific document on its content. This is a first phase toward a full-text-search functionality cross document.
  * Extra functionality to be activate on tenant level:
    * Replace existing convert office docs to PDF;
    * Replace existing digital stamp functionality;
    * Replace existing thumbnails creation.
* Update Kofax AP Essentials import service for AX2012 integration (Ex Arte V5):
  * Only import selected receipt lines;
  * Temporarily store XML files coming from Kofax AP Essentials.
* For the Kofax AP essentials integration to D365FO an update is done to round amounts to 2 characters (0.00).
* Update D9A kickstart with newest D365FO data entities.
* Update configuration section, delta storage fields are removed and delta packager field has become dropdown box instead of ID’s.
* e-platform service is updated to optimize memory usage.
* The Raptor standalone document warehouse is now available via [https://raptor.adultimagroup.com](https://raptor.adultimagroup.com/) as well as [https://raptor.9altitudes.com](https://raptor.9altitudes.com/).
* New documentation tool is created which includes developer’s pages which can be accessed through the help in the Raptor tenant or via following link: [https://docs.raptor.9altitudes.com/](https://docs.raptor.9altitudes.com/).

##

## December 2022

Most important new features & changes are:

* D365 Business Central Taxonomy synchronisation in Document Warehouse used basic authentication (only) to connect to D365BC, Oauth2 is now added as alternative. Oauth2 is a requirement for use with version as of BC21, lower version can still use basic authentication.
* When accessing the document list in plugin mode, an end user will be able to (un)lock the context of the document warehouse, allowing the end user to switch context in the external system (like D365FO, D365BC, D365CE….) without the context of the document list being updated .
* First version of Minimum Viable product “Cortex”, 9A Artificial Intelligence solution to classify and recognise documents, seamlessly integrated in the 9A Document Management framework.
* To allow large size messages to be send over the e-platform (for incoming as well as outgoing).
* New version including bug fixes to use filtered fields is made available for the SharePoint Document Management WebPart.

## November 2022

Most important new features & changes are:

* In this release the focus was on building the audit trail feature, which can be activated per customer tenant allowing the Document Warehouse to track, per document, actions such as
  * View, create, delete, download & print document
  * Add/remove tag/template
  * Update field

For each of these actions the date/time and username will be tracked. In the document list an extra tab “Audit” will be available which shows the full audit trail for the selected document. All users who have the rights to see the document in the Document Warehouse will be able to see the audit trail once activated (image 1).

The audit trail feature comes with a one-off activation fee, but once activated no recurring cost on top of the monthly subscription fee will be taken into account (for all subscriptions except the Light version).

* Currencies will be synced, as part of the kickstart solution, from D365FO to Kofax AP Essentials to limit the currencies that can be OCR & validated for a purchase invoice per buyer/legal entity.
* The swagger user interface is restructured into separated definitions (image 2).
* In the configuration section on the tab jobs, an administrator can now set a legal entity for a SQL Kofax Master data sync job. In this way an administrator can easily see what SQL Kofax Master data job concerns which legal entity.
* In the user interface in plugin mode, the plugin info was showing the source instead of the entity name and company.
* In the configuration section on the tab Users, a page refresh was needed to see changes.

<figure><img src="../.gitbook/assets/image (529).png" alt=""><figcaption><p>Audit trail feature</p></figcaption></figure>

## October 2022

**October 2022 release 9A Document Management!**

Most important changes & fixes:

* Fetching documents failed if user had too many roles assigned.
* For files which cannot be rendered, a download link becomes available in the document viewer screen.

<img src="../.gitbook/assets/image (537).png" alt="" data-size="original">

* \[D365FO integration] Fixed an issue where documents were not being tagged after document creation.
* Page load time has been improved (content is loaded dynamically).
* In plugin mode, the Document Warehouse can show useful information about the system in which it is embedded. This information can be viewed by clicking on the username in the top right corner and selecting ‘Plugin’.

![](<../.gitbook/assets/image (548).png>)

* Introduced a new feature flag which changes the Read-only role flag behaviour. In this new behaviour, a user will only be put in read-only mode if all assigned roles have Read-only enabled. In the current situation, the user will be in Read-only mode if one or more of the assigned roles have the setting enabled. The Read-only feature flag can be activated by a 9A Document Management consultant.
* Updated of how errors are displayed. A full history of the error logs is now also visible and logs can be removed.

![](<../.gitbook/assets/image (409).png>)

* Jobs are now being added in different queues based on their job type. Jobs that are essential for production processes will be prioritized.
* In the admin section, tag context can be set to a SharePoint site when performing a sync of a document from SharePoint to Document Warehouse.

![Image 4](<../.gitbook/assets/image (524).png>)



## September 2022

September 2022 release 9A Document Management

* In the administration module, configuration can be performed by admin for Business Central taxonomy sync jobs to Raptor.

![](<../.gitbook/assets/image (417).png>)

* In the administration module, configuration can be performed by admin for Dataverse taxonomy sync jobs to Raptor.

![](<../.gitbook/assets/image (569).png>)

* In the administration module, configuration can be performed by admin for SQL master data sync jobs to Kofax AP essentials.

![](<../.gitbook/assets/image (412).png>)

By setting exclude from search criteria in a taxonomy sync job a tag in the taxonomy tree can have the "exclude from" search field set to true/false.

![](<../.gitbook/assets/image (532).png>)

* The active tab (Detail/View) was no longer being persisted when using the Document Warehouse from an external system.
* When changing the context in an external system, the first document is now selected in the Document Warehouse at any time.
* When a key user uploads a document in a small window, the save button was pushed to the bottom of the screen.

![](<../.gitbook/assets/image (415).png>)

* Several UI regressions were fixed (including read only tags visualization & tag formatting).
* Tags can now be configured to be ignored during tag search and can be set up in the entity configuration by an administrator. This can be used to exclude obsolete or irrelevant tags from the tag lookup. In the administration module, configuration can be performed by admin for any taxonomy sync jobs to Raptor.

![](<../.gitbook/assets/image (527).png>)

Most important changes & fixes:

<br>

