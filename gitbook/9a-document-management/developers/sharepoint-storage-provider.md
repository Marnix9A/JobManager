# SharePoint Storage Provider

## About

The SharePoint integration links files in SharePoint and Raptor. This means that a file can exist in SharePoint, and visualized in Raptor.

Access to the document in Raptor is independent of access to the document in SharePoint; as far as Raptor is concerned the security roles in Raptor define who can see the file. There is however also a link to the document in SharePoint which will only work for SharePoint users that have actual acces to the file in SharePoint.

### Relations between files in Raptor and SharePoint:

Multiple documents in Raptor can point to the same file in SharePoint.\
But only 1 document in Raptor will be considered the "main" reference to the SharePoint file.

what does this mean?

* When you delete a file in SharePoint, the "main" document in Raptor that is linked to this file will be deleted as well.
* When you rename a file in SharePoint, the "main" document in Raptor will be renamed as well.
* The first time a SharePoint file is linked to a Raptor document, then that document becomes the main document. Even if this document was not created by the sync itself.\
  This can be used to "pre-upload" files when the SharePoint configuration has the status "registered", but not "active".

Extra "Raptor" documents can be created where the external source URL is set to the path to the SharePoint file. But those documents will not be deleted or renamed when SharePoint the file is deleted or renamed in SharePoint.

When you delete a file in Raptor, but not in SharePoint, the SharePoint sync may restore that document at any time. This can happen for example when the file is renamed.

## General Setup

The first thing to configure is which SharePoint we need to connect to. For this only a few steps are required

### In **Azure Entra ID**

Raptor uses the Graph API to connect to SharePoint, and authenticates using an Entra App ID. This means that our _SharePoint App_ must be accepted by an admin in the Azure tenant that is linked to the SharePoint.

{% hint style="info" %}
Accepting the app does yet give us any access to any files in SharePoint. A second step is required in SharePoint itself to give our app access to that specific SharePoint. And that is also where a user is linked to the app, and where specific security rules can be configured.
{% endhint %}

### In **SharePoint**

In SharePoint you need to white list our app. And you have to link it to a specific user account. Access rights are defined on this user, and also depend on the level at which you link the App.

For example: you can link our app on the root level, which would give us access to all the files in the entire SharePoint; or you can add it on each individual site. In the second case we only have access to documents that are in those sites.

Most customers use site specific access, but note that this means extra work in case there are dynamic sites that are created on the fly. For example project specific sites.

### In **Raptor**

In Raptor we need just 2 general parameters:&#x20;

1. The URL to the SharePoint site
2. The Directory ID (= Azure Tenant ID) of the tenant that hosts the SharePoint instance.

Once the above settings are completed, you can register or activate the SharePoint sync. Normally the first step is to register the SharePoint sync, which will allow for testing without actually creating documents in Raptor. And once activated, our sync will actually start processing all the files in SharePoint and start to create documents in Raptor.

<figure><img src="../.gitbook/assets/image (176).png" alt="Example of how the SharePoint General Config element looks like."><figcaption><p>General SharePoint Configuration</p></figcaption></figure>

Once the data is available you can _**Register**_, or _**Activate**_ the storage provider. Once the provider is registered it can start processing files that are manually uploaded and have the URL set to the SharePoint files. But in order to start the automatic sync for all the files in all the sites you will need to use _**Activate change tracking**_.

## Site Setup

Each site for which documents should be synced to Raptor should be listed here.\
When a site is added, all the document collections (drives) are included in the sync.

<figure><img src="../.gitbook/assets/image (175).png" alt="Example of what the site editor looks like."><figcaption><p>site editor</p></figcaption></figure>

You can only add sites that already exist, and that we have access to. Should you delete a site afterwards it will eventually be visualized in the UI as a greyed out record.

Once a site is added the sync will start, depending on the number of documents the sync should take several minutes to hours.

### Site specific tags

It is possible to configure tags that should be added to each document in a Site. However, this tag will only be assigned to the document when it is created by the sync.&#x20;

This means that if a document is added in Raptor (via a user, or an external flow), and pointing to a SharePoint site that has a specific tag assigned to it, this site tag will not be added to the document.\
This also means that you can remove the tag from the document, and this tag will not be re-added to the document.\
This also means that adding a new tag, or change the site specific tag will not have an impact on already existing documents in Raptor.

### Supported Sites

Only top level sites are supported, nested sites are not.\
The path to the site should look like this:

```
/sites/your_site_name
/teams/your_team_name
```

## Manual adding a document from SharePoint

(see [uploading-files.md](../raptor-document-warehouse/user-guide/uploading-files.md "mention"))

Go the the raptor web site and:

1. Click on the \[v] button next to the "upload" button, to open the upload menu
2. Click on the "Upload external document" button.
3. Enter the URL to the document in SharePoint, and add a file name.

{% hint style="warning" %}
When you add ad external document in Raptor that references a file in your SharePoint, make sure that it does not contain double slashes. This may cause trouble for the Storage provider to locate the document.

Bad: https://domain.sharepoint.com/sites/site1<mark style="color:red;">**//**</mark>documents/document1.docx

Good: https://domain.sharepoint.com/sites/site1<mark style="color:green;">**/**</mark>documents/document1.docx
{% endhint %}

Once this document is created the SharePoint integration will verify if it can access the file in SharePoint based on the provided URL, and if so, the file can be viewed and downloaded in Raptor.

{% hint style="info" %}
Note that .docx files may be downloaded instead of opened in a new tab depending on the configuration in your browser and SharePoint instance. To ensure that documents are opened in the browser, add “?web=1” add the end of the URL when manually adding an external document in Raptor.
{% endhint %}

## Automated Sync from SharePoint to Raptor

After activating the SharePoint storage provider, an automated sync will start which will create a document in Raptor for each file found in the sites that are stored in the Site Setup. No further action should be required.

This file sync uses an event driven system to identify which "document lists" have changes. After a change notification is received the system will as soon as possible process the changes and create, rename or delete the documents in Raptor.

To monitor changes in SharePoint we use the best practices as defined by Microsoft. This means that we create subscriptions on all the drives (aka document collections) in SharePoint, and then use delta links to get changes of the drive.

Note that SharePoint may delay change events up to several minutes, which means it may take a while before new files become available in SharePoint.

{% hint style="info" %}
Some operations in SharePoint may break our delta links, this could happen if changes are made to the configuration of a site, or to the underlying database and hardware that hosts the SharePoint environment. In such cases it is possible that we have to reprocess all the files in all the drives which are being monitored. Should such a situation occur, it may take several hours or in worst case even days before the system is back in sync.
{% endhint %}

## Sync from Raptor to SharePoint

In the specific situation when a document is already present in Raptor, and it needs to be uploaded in SharePoint in a site that is synced with Raptor we have a problem:

In this situation, there is a race condition, where the sync can pick up the new file in SharePoint, and will create a new document in Raptor, and where the existing document does not (yet) have a link to a SharePoint document for the simple reason that the file does not (yet) exists.

To solve this problem there is an endpoint available in our API that will upload the file, and make sure the link is created to the existing document in Raptor.

{% code fullWidth="false" %}
```http
HTTP POST ~/apigateway/api/storageproviders/sharepoint/file/upload-to-sharepoint
Authorization: Bearer XXXXXXX
Content-Type: application/json
Accept: application/json

{
  "configId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "siteConfigId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"     //optional
  "fileReferenceId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "driveId": "b!dxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "filePath": "/root folder/sub folder/file name.pdf"
}
```
{% endcode %}

<details>

<summary>Requirements</summary>

Requirements  & restrictions related to this call:

* The targeted site must be part of an existing site..
* There is no file in SharePoint with the same name.
* The file and path do not contain any characters that are illegal in SharePoint
* The document in Raptor may not yet be linked to another file in SharePoint.

</details>

<details>

<summary>Arguments / Parameters</summary>

To call the endpoint you must pass in following parameters:

* **configId** is the ID of the SharePoint Config object, as found in the Raptor UI.
* **siteConfigId** _\[optional]_ the ID of the site config in Raptor.
* **driveId** this is the driveId (Graph API) where you want to upload the file to.
* **path** this contains the desired full path of the file inside the document collection
* **fileReferenceId** the file reference id of the file in raptor. (not the document id)

Example of the path parameter:

```
/document.pdf
/folder/document.pdf     
/folder/                 
/
```

In case the path ends with a / the function assumes that it should use the filename as it is known in the File Reference object. In this case illegale characters will be removed from the filename before uploading. After uploading the file will be the "main" SharePoint file, meaning that the name in Raptor will be modified to the filename in SharePoint.

</details>

Result of the operation

{% hint style="success" %}
Result of the operation

* The existing document in Raptor will be the "main" link to the SharePoint file.
* If the filename in SharePoint is different then the original filename of the document in Raptor, then the Raptor document will be renamed to match the new name.
* The external source URL on the document will be set to point to the SharePoint file.
{% endhint %}

{% hint style="danger" %}
What is not part of this operation

* No tags are added to the document as part of this call.\
  As this document already existed, and already has tags, we decided not to add any.
* The default storage provider remains the existing storage provider.\
  Meaning that changing the file in SharePoint will not be reflected in our viewer, as the viewer will always show the file as it is in the primary storage provider.
{% endhint %}

### Error handling.

As this operation by definition depends on several network calls between several servers and databases, it is possible that any of those calls fail. This operation is not, and cannot be made 'atomic'. Instead we opted for a procedure that can recover from an error when it is run again. This means that in case of a problem, just retrying the same call with the same arguments should resolve the issue. (if it is resolvable)

Possible Response Status Codes

<details>

<summary>403 BAD REQUEST</summary>

This code is returned if we detect a problem that cannot be recovered automatically.

This code means that you should not retry the call.

The body of the message will contain extra information about the state of the procedure; and is intended to help debug the problem. The content and schema of the response body may change in the future, and should not be parsed for automated procedure.

After investigation, and having made some changes to either the request parameters, or some of the systems involved a retry can be considered.

</details>

<details>

<summary>500 INTERNAL SERVER ERROR</summary>

This error is returned if there is a problem that can likely be recovered from, and which probably is transient.

For example if the SharePoint server is down, or the operation took to long and a lock expired.

The call should be repeated with the exact same parameters.

Ideally the retry is delayed with an exponentially increasing time interval.

</details>

### Important information:

When uploading the file to SharePoint it will first get a different name, with a fixed prefix. This allows us to ignore the file in the change feed / delta link as long as the procedure is not yet completed. This is required because it is not possible to add additional meta data to the file that can link the file to the request in a way that can be discovered and recovered from in case anything would go wrong in the proceeding calls.

## Unlinking a document from SharePoint

Once a document is linked, the sync will remove the document in Raptor when it is deleted in SharePoint. But this may be undesired. In such a case the api provides an endpoint that can be called to unlink the document.

Before unlinking the document it will download the latest version from SharePoint and save it in the default Raptor storage. (unless if the local storage already has the document)

```http
HTTP POST ~/apigateway/api/storageproviders/sharepoint/file/detach
Authorization: Bearer XXXXXXX
Content-Type: application/json
Accept: application/json

{
  "azureDirectoryId": "string",
  "driveId": "string",
  "driveItemId": "string"
}
```

## Fetch the Raptor document matching a file in SharePoint

Sometimes you need to get the document in Raptor that is linked to the file in SharePoint. This can be done with following call:

```http
HTTP GET ~/apigateway/storageproviders/sharepoint/file/find-document?azureDirectoryId=xxxxx&driveId=xxxx&driveItemId=xxxxx
Authorization: Bearer XXXXXXX
Accept: application/json
```

{% hint style="info" %}
There may be a delay between the creation of a file in SharePoint and the time a synced file is available in Raptor. This call can be used to verify that the sync already processed the file.
{% endhint %}



