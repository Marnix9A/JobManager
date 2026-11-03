# Storage providers

Storage providers are external data sources that can be synchronised with 9A Raptor DWH. By using a storage provider, external documents can be visualised in the 9A Raptor DWH tenant and used like any other 9A Raptor DWH document. The added benefit is that 9A Raptor DWH does not copy the external documents, but instead contacts the external datasource directly, saving storage cost.\
\
Currently the only supported data source is **SharePoint**.

![](<../../.gitbook/assets/image (346).png>)

A document synchronised from the storage provider will appear in 9A Raptor DWH as an external document. The linked SharePoint file can then be opened via the 'External source' button.

## Creating a storage provider

To create a storage provider, go to the tab ‘Storage providers’ and click the ‘+’ button. Insert a name of your choosing and hit ‘Save’.

After saving, you can further specify the settings:

<figure><img src="../../.gitbook/assets/image (322).png" alt=""><figcaption><p>demo on how a storage provider is configured</p></figcaption></figure>

{% hint style="info" %}
When you add ad external document in 9A Raptor DWH that references a file in your SharePoint, make sure that it does not contain double slashes. This may cause trouble for the Storage provider to locate the document.

Bad: https://domain.sharepoint.com/sites/site&#x31;**//**&#x64;ocuments/document1.docx

Good: https://domain.sharepoint.com/sites/site&#x31;**/**&#x64;ocuments/document1.docx
{% endhint %}

Hit 'Register' to activate the storage provider. This will allow 9A Raptor DWH to recognize documents for the SharePoint when an external document is manually added (see [uploading-files.md](../user-guide/uploading-files.md "mention")). When an external document is recognised, it will be possible to preview it in the 9A Raptor DWH viewer and download/print it through 9A Raptor DWH.

Storage providers were created to have a generic interface for external services that can access files and stream them to Raptor when needed.

First the storage provider has to register itself; this means that it has to inform Raptor on which URL it will be available for two way communications.

Next, every time a file is uploaded in Raptor and there is an external source URL set, raptor will contact all the known storage providers to verify if they have access to that file.

It is the task of the storage provider to reply yes or no to this question.

If a storage provider confirms that it has access to this file, Raptor will link the file to the storage provider, and if the file is needed at any time; Raptor will ask for the file.

This could happen when a user wants to visualize or download the file.

Note that .docx files may be downloaded instead of opened in a new tab depending on the configuration in your browser and SharePoint instance. To ensure that documents are opened in the browser, add “?web=1” add the end of the URL when manually adding an external document in 9A Raptor DWH.
