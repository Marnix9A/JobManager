# Dox42

9A provides its own Dox42 connector for Dynamics 365 Customer Engagement, which seamlessly integrates with the Raptor Document Warehouse. Below is a complete guide on how to link Dox42 templates in CE and map them to Raptor tags and templates.

## Technical Configuration

Open the dox42 app:

![](<../../.gitbook/assets/image (255).png>)\
There you will find the following site map items:

<div align="left"><figure><img src="../../.gitbook/assets/image (200).png" alt=""><figcaption></figcaption></figure></div>

**1.        Service Connections**\
Defines the connection to the SharePoint location where the templates are stored.

**2.        Template Configuration**\
Contains the templates that users can select from when generating a document for a record in D365 CE.

**3.        Languages**\
Allows you to define the languages supported by your dox42 configuration.

**4.        Text Blocks**\
Predefined text components that can be reused across documents. You can also create custom, record-dependent text blocks.

**5.        Text Block Types**\
Lets you categorize text blocks, making it easier to select them in templates or generate them automatically via a flow.

**6.        Translation**\
Used to translate specific records (e.g., product names). It can also serve as a standalone multilingual text block, not necessarily tied to a record.

**7.        Signature Email Messages**\
If you want to integrate document signing, this entity allows you to define email content used in flows to Signicat, DocuSign, etc.

**8.        Signers**\
Specifies the individuals who are required to sign the document.

**9.        Parameters**\
Contains all the necessary settings for dox42 to function, such as API URLs and configuration values.

**10.   Users**\
You can configure a default queue for each user. This queue is automatically selected when sending emails to customers.

**11.   dox42 Admin Configuration**\
Opens the administration configuration interface provided by dox42.

**12.   dox42 Resources**\
Provides access to all available dox42 resources and documentation.

**13.   dox42 Downloads**\
Before you can create or configure templates, a dox42 add-in must be installed. This section contains the necessary downloads.

### Service connections

Here you can define the location where the dox42 templates are stored. Note that you can configure multiple locations if needed.

<figure><img src="../../.gitbook/assets/image (201).png" alt=""><figcaption></figcaption></figure>

·        Name: The name of your service connection.

·        Server URL: The URL provided by the dox42 team. This will be used to generate the documents.

·        Template Base URL: The SharePoint location where the templates are stored.



### Languages

This allows your documents to support multiple languages. Before doing so, you need to define the available Languages:<br>

<figure><img src="../../.gitbook/assets/image (256).png" alt=""><figcaption></figcaption></figure>

·        Name: The display name users will see when selecting a specific language.

·        Code: The internal _dox42_ language code used in the document generation process.

·        CE Code: Allows you to map the _D365 CE_ language(s) to a specific _dox42_ language. For example, if your ERP sends multiple variations of Dutch (e.g., nl-BE, nl-NL), you can link them all to a single "NL" dox42 language.

·        Raptor Tag: If Raptor is enabled, this field lets you automatically associate the correct language with your uploaded document.

Note: The language code will also be passed into the generated document and may be used in the template file naming. More on this in the _Template Configuration_ section.

### Text Blocks

These are predefined blocks of text that can be used within your templates. Text blocks can also be linked to specific records and are typically created via Power Automate flows:

<figure><img src="../../.gitbook/assets/image (203).png" alt=""><figcaption></figcaption></figure>

&#x20;

·        Name: The name of the text block.

·        Code: A unique identifier for the text block. For example, if you're working with multiple languages, you can append the dox42 language code (e.g., \_en-us).

·        Text Block Type: Used to categorize your text blocks for easier management and retrieval.

·        Language: Select from the configured _dox42 Languages_.

·        Sort Order: Controls the ordering of text blocks in the selection list, making it easier to locate specific blocks.

·        Is Template: Indicates whether the text block is a reusable template (used in flows) or a record-specific block.

·        Primary Entity: Specifies the Dataverse entity to which this block is linked.

·        Auto-Add: If set to "Yes", this text block will be automatically added when the related record is created via a flow.

·        Regarding _(Hidden)_: Stores the reference to the related record.

·        Parent Text Block _(Hidden)_: Allows linking text blocks hierarchically.

·        Description: An HTML editor where you define the content that will appear in the generated document.

### Text Block Types

Text block types are used exclusively to categorize text blocks.

<figure><img src="../../.gitbook/assets/image (204).png" alt=""><figcaption></figcaption></figure>

·        Name: The name of the Text Block Type.

·        Code: A code used to easily identify the Text Block Type.

·        Value: An optional description or label for the type. This field is rarely used or populated.

### Translations

Used to translate specific records (e.g., product names). It can also serve as a standalone multilingual text block, not necessarily tied to a record:

<figure><img src="../../.gitbook/assets/image (205).png" alt=""><figcaption></figcaption></figure>

·        Language: Specifies the language for which the translation is intended.

·        Regarding (Optional): Indicates the record to which the translation is linked. This is a _polymorphic lookup_, meaning it can reference multiple record types. If you need to add a custom entity (e.g., alongside “Price List” or “Product”), your technical colleague will need to add it to the lookup control using tools like the _XRM Toolbox – Polymorphic Lookup Manager_.

·        Translation Code: A technical identifier that allows you to easily reference the translation in templates.

·        Translation: A short text string representing the translated value.

·        Translation Long Text: An HTML editor field where you can enter rich-text translations, including fonts, formatting, and colors.

·        Translation Long Text (No HTML): A plain text version of the translation, without any HTML formatting.

### Signature Email Messages

This is a custom activity entity designed to help users easily prepare a message before sending it to the customer. When creating a template, you can choose to enable document signing. If enabled, this screen will open, allowing you to add multiple documents for signing and configure the signing options.

All settings and callback URLs must be defined in the [#template-configuration](dox42.md#template-configuration "mention").

<figure><img src="../../.gitbook/assets/image (206).png" alt=""><figcaption></figcaption></figure>

·        Subject: The subject line of the email.

·        From: Can be a queue or a user. This can be selected in the template chooser or entered manually.

·        Sender Name: The display name of the sender.

·        Sender Email: The email address from which the message will be sent.

·        Recipient Name: The name of the recipient.

·        Alternative Recipient Email: The email address to which the message will be sent.

·        Extra Recipients _(not yet functional)_: Allows defining additional recipients (feature pending).

·        Regarding: The record to which this email is related.

·        Attachments: Documents that will be included in the signing request. Note: the filename must contain "TOBESIGNED" for the document to be included as required for signing.

·        Send to Sign: A custom button that triggers the Power Automate flow to send the sign request to the configured recipients.

### Signers (Inactive – Under Development)

This feature is currently under development and not yet in use. It is intended to define who needs to sign a document, the number of required signers, and the signing order.

<figure><img src="../../.gitbook/assets/image (207).png" alt=""><figcaption></figcaption></figure>

·        Signer: The customer or contact who is required to sign.

·        Signer Name: The name of the signer. If no account or contact is linked, you can manually enter the name and email.

·        Email: The email address of the signer.

·        Regarding: The related record. This is a _polymorphic lookup_, meaning it can reference different types of entities.  Your technical colleague will need to add it to the lookup control using tools like the _XRM Toolbox – Polymorphic Lookup Manager_.

### Parameters

All parameters required to make dox42 work are stored here. These are typically configured by a technical consultant from 9A.\
![](<../../.gitbook/assets/image (208).png>)

·        Name: The name of the parameter.

·        Value: A short text value associated with the parameter.

·        Description: A more detailed description or long text value of the parameter. This field can contain a JSON string or other types of structured data.

·        Encrypt Value: Enable this if you want the value to be stored securely (e.g., for passwords or sensitive data). For the moment, it only works on the _dox42\_FetchQuery\_CustomAPI\_Settings_ parameter.

### Users

On the user record, you can define the Default Sending Queue. When sending a template via email, this queue will automatically be pre-filled in the template:<br>

<figure><img src="../../.gitbook/assets/image (257).png" alt=""><figcaption></figcaption></figure>

### dox42 Admin Configuration

This opens the dox42 Admin Configuration page (MAUI) provided by dox42.

<figure><img src="../../.gitbook/assets/image (210).png" alt=""><figcaption></figcaption></figure>

### dox42 Resources

This opens a page provided by dox42 containing various webinars, tutorials, and other resources on how to create/configure documents:

<figure><img src="../../.gitbook/assets/image (211).png" alt=""><figcaption></figcaption></figure>

### dox42 Downloads

This opens a dox42 page containing all the necessary downloads required to create documents in Microsoft Word.

The most commonly used components:

* dox42 Enterprise Add-Ins:\
  Includes the Word add-in needed to configure your templates. As a partner, you can request a free license by contacting [hello@dox42.com](mailto:hello@dox42.com) .
* dox42 D365 CE / Dynamics CRM / Dataverse:\
  Legacy method for creating data sources and connecting to Dynamics 365 CE. A separate license is required for this component.
* dox42 Server:\
  A graphical user interface (GUI) layer over the dox42 API, allowing you to test document generation functionality.

### Template Configuration

#### Types of Template Configuration

The screen layout will adapt based on the selected type, displaying only the relevant options.

**Document Template**

This is the default type of Template Configuration. It will appear in the template chooser under the “Generate Documents” button.  This configuration generates a document (saved as a Note in D365 CE), and optionally allows you to send it as a standard email or a signable email:

<div align="left"><figure><img src="../../.gitbook/assets/image (212).png" alt=""><figcaption></figcaption></figure></div>

<div align="left"><figure><img src="../../.gitbook/assets/image (213).png" alt=""><figcaption></figcaption></figure></div>

This means that a document will be generated. If “Create Draft Email” is selected, an email will be prepared with the generated document, and—based on the Raptor settings—standard documents can be included as attachments if needed. 

**E-mail Template**

This type appears in the template chooser under the “Generate Email” button.\
It is used to generate an email based on a document or a dox42 configuration, without necessarily storing a separate document record:

<div align="left"><figure><img src="../../.gitbook/assets/image (214).png" alt=""><figcaption></figcaption></figure></div>

<div align="left"><figure><img src="../../.gitbook/assets/image (215).png" alt=""><figcaption></figcaption></figure></div>

This means that no document will be generated—only the email itself, which can be sent to the customer.  Based on the Raptor settings, you can still include standard documents as attachments if needed.

This is comparable to Microsoft’s standard Email Templates, but it works across all entity types and offers many more options.

**E-mail Body/Description Document**

This is used by the Email Templates to define the subject and body of the email. It supports multilingual configurations and offers several advanced options.\
\
For example, you can use a dox42-generated document as the email body, or directly insert additional dox42 template fields into the description.

### General Configuration

This is the most basic configuration you need to set up. Below, you’ll find the various options. If a setting is only applicable to a specific template type, this will be indicated accordingly.<br>

<figure><img src="../../.gitbook/assets/image (258).png" alt=""><figcaption></figcaption></figure>

&#x20;

* Template Type: Choose between _Document Template_, _E-mail Template_, or _E-mail Body/Description_.
* Name: The name displayed to the user in the “Templates” list.
* Primary Entity: The entity the template is associated with.
* Service Connection _(Document Template & E-mail Body/Description only)_: Defines the connection to SharePoint.
* Allowed Output Types _(Document Template only)_: Specify the allowed document output formats (e.g., DOCX, PDF, DOC, …).
* Template URL _(Document Template & E-mail Body/Description only)_: The path to the document relative to the base URL of your service connection. For example, if the base URL is [https://yourtenant.sharepoint.com/sites/MyDocuments/Shared%20Documents/Dox42/](https://9altitudesgtm.sharepoint.com/sites/9ADocumentManagement/Shared%20Documents/Dox42/) , you can specify myDocument.docx, or subfolder/myDocument.docx if located in a subfolder.
* HTTP Method _(Document Template & E-mail Body/Description only)_: Always keep this set to the default value POST.
* Operation _(Document Template & E-mail Body/Description only)_: Always leave this as Generate Document.
* Alternative Create Document URL: Optionally, you can provide a custom HTTP Power Automate endpoint to perform additional actions. This is typically used during a transition from the old dox42 approach to the new XML-based setup. The standard HTTP Power Automate flow is configured in the _'dox42\_CreateDocument\_PowerAutomate\_URL'_ parameter, which should be set up by a technical colleague.
* Use dox42 Connector _(Document Template only)_: Always set this to No. The dox42 connector is no longer used due to high monthly costs and incompatibility with FO and BC. This option will be hidden in newer versions of the product.
* Sort Order _(Document Template & E-mail Template only)_:  Determines the order in which templates appear in the “Template Chooser” screen visible to users.

{% hint style="warning" %}
ATTENTION: After you have filled in all the “General Information”, make sure to save the record — otherwise, you won’t be able to complete the remaining fields.
{% endhint %}

#### E-mail Configuration (Document Template & E-mail Template only)

Here you can define how the e-mail creation process works. The subject and description can be configured in multiple ways. However, a new approach is being introduced, and going forward, only the standard options — as explained below — will be supported.

If you see something like (@id and @language can be used as parameters), this means those parameters will be automatically replaced within your FetchXML.

<figure><img src="../../.gitbook/assets/image (218).png" alt=""><figcaption></figcaption></figure>

·        Multi Language Subject/Description Configuration: Always set this to “Yes”. This enables translation of the subject and description based on the selected language.\
If set to “No”, separate fields for _Subject_ and _Description_ will appear instead.

<figure><img src="../../.gitbook/assets/image (219).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Important: Make sure to keep this option set to “Yes”, as the “No” option will be deprecated in the future.
{% endhint %}

·        Use dox42 Data Sources (JSON/XML): Always set this option to “Yes”. This ensures that the “dox42 Data Sources” — which will be explained later — are used. The same FetchXML results will then be applied to define the e-mail subject and description.

\
If you choose “No”, you’ll instead be able to use the _Filename Fetch_ for your e-mail subject and body as well:

<figure><img src="../../.gitbook/assets/image (220).png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Important: Make sure to keep this option set to “Yes”, as the “No” option will be deprecated in the future.
{% endhint %}

&#x20;

·        Filename for Generated Document: Currently, only a single (global) filename can be defined, meaning it's not yet possible to translate the filename into multiple languages. However, users can manually change the filename in the “Template Chooser” screen.

<div align="left"><figure><img src="../../.gitbook/assets/image (221).png" alt=""><figcaption></figcaption></figure></div>

You can also use specific placeholder codes within the filename, for example:\
{name}-{createdon:dd/MM/yyyy}-{linkedcontact.fullname}<br>

Explanation of the placeholders:

_{name}:_ Retrieves the value of the _name_ field from the FetchXML result.

_{createdon:dd/MM/yyyy}:_ Retrieves the _createdon_ (date) field and formats it using standard date format patterns.

_{linkedcontact.fullname}:_ Retrieves the _fullname_ of a related (linked) entity. Use the format: \<linked entity schema name>.\<field name on linked entity>

·        Fetch Used for the Filename only: Since the filename is generated within the “Template Chooser”, the dox42 Data Sources cannot be used — those heavier FetchXML queries are only executed when clicking “Create” or “Preview”. That’s why a separate FetchXML query is required specifically for generating the filename.

<figure><img src="../../.gitbook/assets/image (222).png" alt=""><figcaption></figcaption></figure>

We are currently investigating whether this fetch can be cached, so that it is already executed when the user opens the “Template Chooser”.

·        Subgrid “dox42 Email Configuration”: This opens a separate screen where you can define the subject and description of the e-mail:

<figure><img src="../../.gitbook/assets/image (223).png" alt=""><figcaption></figcaption></figure>

o   Name: The name of your dox42 Email Configuration.

o   Parent Template Configuration: Automatically populated when you click “+ New” from the subgrid.

o   Language: The language to which this configuration is linked.

o   Subject: The subject line of the e-mail.

o   Use Document as body: If set to Yes, you can select an “E-mail Body/Description Document” template.

<figure><img src="../../.gitbook/assets/image (224).png" alt=""><figcaption></figcaption></figure>

o   Description: An HTML editor where you can define the e-mail body content.

&#x20;

{% hint style="warning" %}
Important: When you see the “![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACMAAAAcCAMAAADcK/YTAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAHIUExURf///8zjzBKKEx+pIBGYEj2VPcTfxPX69fv9+/7+/sziyyetKCPiKS/gNjC9MDCfMHu6e8nhyfr8+v3+/f39/cvhyyyyLhbjHQXjEhrkIirWLzK3MjWdNZHCkuTv5P7//iqyLBXiHgTiEQPjEQbjESDjKDzWPS2uLTmXOq/Rr/z9/CqxKxXiHQPiEAPiEQHjDgXZDzTaNzPENBKUE2iuaN/u3/b79srhyiixKRTiHQPhDwPYDQLMCQG/AwG5AhXHFy3NLyKwIiWXJYO+hNzs3Pn8+SiyKRTdHAPTCwLIBgG+AwC6AQa9BxbFFxO9FRemGECeQa7TrsrgyiivKRXHFgC7AQG6AgO8BQScBUmcSSatKBPEFAK3AwWSBkOaQ8ngySWtJhHCEQK4AwSkBAaJByaLJ4C8gCGrIg/BDwC8AQSmBQaNBwt/C0ueTLPXtPP58yCqIA3ADQC+AQKwBAaOBwh8CTiVOK3Trez17BqmGwm/CgK0AwWWBgl8CSWJJoW/hfH48RKiFAO9BAKyAwqFCymLKmetZ87lzsrjyg2WDQKvAwOdBAaGBxGBEWWsZcLfwvL48s3kzQ+ADwV8BgV5BkScRcjhyO/273I9WUoAAAAJcEhZcwAADsQAAA7EAZUrDhsAAAEVSURBVDhPY2AY0oCRiZmFlY2dg5MTXQYBuLh5ePn4BQSFhEVwqhIVE5eQlJKWkZUTFpZnwK5MVEFRSVlFVU1dQ1NIWAu7IlFtHV1dPX0DQyNjE1MzLRF0eRAwt7BUtrK2sbWzd3B0cnZxRZcHAXM3dw9PL29vb28fXz//gEB0eRAICg7x9g4NDQ319vYOC4+IRJcHgaCo6NBQkCKQypjYOHR5EIhPSASbEhoampSckpqGLg8CQekZYEMyw7Kyc3Lz8tHlQSCooBBkSlFxSWlZeYWQMLo8CAhWVoV6e1fX1NbVN3BqyWMNQ8HGptDmiJbWtnYtLWGsKhgYOjq7unt6+/onCOOO+YmTJk+ZOm26Fo6oGpkAAI0xPrMQSnQDAAAAAElFTkSuQmCC)” icon next to the Subject or HTML Editor fields, it means you can insert _fields_ from the related _Document Template_. These fields are retrieved from the Generated XML/JSON produced during testing of the _dox42 Data Source_. More details on this will be explained further in the documentation.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (225).png" alt=""><figcaption></figcaption></figure>

·        Related Account Field for the Recipients Picklist: In the “Template Chooser”, users can select a _Recipient_. To populate this list, you need to specify the field from which to retrieve the related contacts — for example, customerid.\
This tells the Template Chooser to gather all contacts linked via the customerid lookup, as well as information from the customerid entity itself. The recipient list will then be automatically populated with all relevant contacts.

·        Contact Job Title Field: This refers to the technical field name on the _Contact_ entity where the job title is stored. This can either be a Text field or a Lookup field, depending on your configuration. (e.g., jobtitle or aug\_jobtitleid)

#### Languages

Here you can define in which languages your template will be available via the “Template Chooser” for the users.

<figure><img src="../../.gitbook/assets/image (226).png" alt=""><figcaption></figcaption></figure>

·        Separate Documents per Language:

* If you choose “Yes”, you’ll need to create a separate document for each language.
* For example, if your template URL is myDocument.docx, you must provide separate files such as:
* myDocument\_nl-be.docx
* myDocument\_fr.docx
* myDocument\_en-us.docx

{% hint style="warning" %}
&#x20;The language code at the end of the filename should match the dox42 language code (e.g. en-us), not the CE language code. The CE code is only used for mapping multiple CE languages to a single dox42 language file.
{% endhint %}

* If you choose “No”, only one document is needed. Translations must then be handled within the template itself using the Language parameter and conditional logic (e.g. IF/ELSE statements).
* Subgrid “dox42 Language”: Use this to add all languages that the template supports.
* Related Language Fields:These three fields allow the system to automatically determine the correct language based on information from a related record.
* Default Language Field: Select either a Text or Lookup field that stores the language information.
* If a Lookup field is chosen, the Default Language Related Attribute will allow you to select a related attribute.
* Default Language Related Attribute: Only available if a Lookup field is selected in Default Language Field.
* If another Lookup is selected here, you can continue with Default Language Related Attribute 2.
* Default Language Related Attribute 2: This is the deepest level supported. Here, you must select the final field containing the language code (usually a Text field).<br>
* Example:\
  1\. Lookup: Primary Contact (primarycontactid) – Entity: Contact →\
  2\. Related Lookup: Preferred Language (adx\_preferredlanguageid) – Entity: adx\_portallanguage →\
  3\. Related Text: Language Code (adx\_languagecode)

➡️ Based on the values in these fields, the Template Chooser will automatically preselect the appropriate language. The user can still manually override this selection if needed.

#### JSON/XML dox42 Data Sources

This section is required to retrieve all necessary information from Dataverse in JSON or XML format. You will define one or more FetchXML queries that can interact with each other.

Whenever possible, try to consolidate everything into a single FetchXML query to improve performance and simplify maintenance. You can create FetchXML queries in various ways:

* Using existing Views
* Using the FetchXML Builder plugin in XrmToolBox

Make use of link-entities wherever applicable to efficiently retrieve related data.

For more information and examples, refer to the official Microsoft documentation: [FetchXML Overview – Microsoft Docs](https://learn.microsoft.com/en-us/power-apps/developer/data-platform/fetchxml/overview).

{% hint style="warning" %}
This setup will only work if all required parameters are correctly defined.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (227).png" alt=""><figcaption></figcaption></figure>

&#x20;

·        Fetch via Custom API: A custom API has been implemented to retrieve data. Previously, Power Automate flows were used, but they proved to be too slow.\
Always set this to "Yes". This setting will be deprecated in the future.

·        Default Value for Placeholder: If a specific value cannot be found, it will be replaced with this placeholder. Leave this field empty if no fallback is required. Otherwise, you can use something like \_ or N/A as a placeholder.

·        Choose your Testing Record: Select a record based on the _OData Entity Name_. This will automatically populate the Default Entity Id field.

·        Default Entity Id: This field is populated with the result of _Choose Your Testing Record_, or you can manually enter a GUID. It is used when generating the test XML/JSON.

·        Default dox42 Language: Specifies the language to be used during test XML/JSON generation.

·        Default User: Defines the user context in which the test XML/JSON will be generated.

·        Generated XML: Clicking the Generate JSON/XML button will populate this field with the resulting XML.\
This XML is what will be used in your dox42 template.\
\
✅ Make sure all attributes referenced in your FetchXML are properly filled, so you end up with a complete and valid XML structure.

·        Generated JSON: Contains the same data as the _Generated XML_, but in JSON format.

·        Always Save Generated XML as Note: When enabled, clicking the Generate JSON/XML button will also save the generated XML as a Note.\
This makes it easier to access and reuse when designing your dox42 templates.

Dox42 Data Source: These are the FetchXML queries used to generate the XML and power your document templates.

<figure><img src="../../.gitbook/assets/image (228).png" alt=""><figcaption></figcaption></figure>

**Name**: The name of your Data Source

**OData Entity Name**: The entity on which the fetchXML will be executed.

**Owning Business Unit**: Read-only; this will be filled automatically.

**Select View**: Based on the selected _OData Entity Name_, available system views will be listed. Selecting a view will auto-fill the FetchXML in the Fetch Query field, which you can then adjust (e.g., to include @id or other parameters):

<figure><img src="../../.gitbook/assets/image (229).png" alt=""><figcaption></figcaption></figure>

**Fetch Query**: The actual FetchXML used to retrieve data from the specified entity.

**Owner**: Automatically set to the current owner of the Data Source.

**Dependent Data Source**: This allows you to make one FetchXML query dependent on the result of another.

* &#x20;Dependent Data Source: The parent _dox42 Data Source_ it depends on.
* Dependent Data Source Field: The specific field from the parent’s result set that is used.
* Dependent Data Source Replacement String: The filter or condition you want to apply, using dynamic values from the parent source.

Example:

<figure><img src="../../.gitbook/assets/image (230).png" alt=""><figcaption></figcaption></figure>

contactFetchQuery is the related “dox42 Data Source”. You will get the fullname in the result.\
In your dependent FetchXML, you reference @fullname.\
The system will automatically replace @fullname with the actual value returned from the contactFetchQuery .

<figure><img src="../../.gitbook/assets/image (231).png" alt=""><figcaption></figcaption></figure>

#### Raptor Configuration

<figure><img src="../../.gitbook/assets/image (232).png" alt=""><figcaption></figcaption></figure>

·        Template Code: Allows you to assign a _Raptor Template Code_ to the generated document.

·        Template Tags (| Separated): Allows you to add multiple _Template Tags_ to the generated document, separated by a vertical bar (|).

{% hint style="warning" %}
Both options are deprecated. It is now recommended to define these values via a parameter in the _Raptor Configuration_.
{% endhint %}

·        Raptor Tags/Template Configuration Subgrid: This option will add extra attachment to the generated e-mails.

<figure><img src="../../.gitbook/assets/image (233).png" alt=""><figcaption></figcaption></figure>

* &#x20;Name: The name of your Raptor Attachment Reference.
* &#x20;Dox42 Template configuration: If you click “+ New” from the subgrid, this field will be automatically populated with the parent template configuration.
* &#x20;Tags (; separated): Here you can enter the _Tag IDs_ (separated by semicolons) of the documents that need to be included.
* &#x20;Templates (; Separated): You can also specify _Template IDs_. This allows multiple documents to be added via the template.
* &#x20; Linked To Record: Only documents related to the current record will be included.
* Language Dependent: Only _Raptor documents_ matching the user’s selected language will be considered.
* &#x20;Owner: Automatically set to the user who creates the _dox42 Raptor Attachment Reference_.

{% hint style="warning" %}
If you require automatic document generation or tag assignment, feel free to reach out to a Raptor colleague for assistance. There are multiple ways to ensure tags are added automatically where applicable.
{% endhint %}

#### eSigning

The eSigning functionality has been fully configured for Signicat, including some features specifically built for this provider. We are planning to support DocuSign in the near future. Note that some of the current options may not be relevant for other signing providers:

<figure><img src="../../.gitbook/assets/image (234).png" alt=""><figcaption></figcaption></figure>

·        Send E-mail Via: Choose between _Via CE_ or _Via Signicat_. Currently, only Via Signicat has been configured and tested.

·        Signature Required: Indicates whether a signature is mandatory for this type of document.

·        Signature Required Fields: Defines which checkboxes (fields) must be selected before a document can be signed via Signicat.

·        Alternative Sign Response URL: Specifies the endpoint where the signing response is processed. For example, you can use this to update the status of a Quote to _Signed_ after completion. The standard HTTP Power Automate flow URL is configured in the _‘dox42\_Signicat\_Response\_PowerAutomate\_URL’_ parameter, which should be set up by a technical colleague.

·        Alternative Sign Document URL: Determines the logic to execute when someone starts signing the document. This may vary depending on the entity type, allowing you to define a custom Power Automate flow based on the existing _Signing_ flow. The standard HTTP Power Automate flow URL is configured in the _‘dox42\_Sign\_PowerAutomate\_URL’_ parameter, which should be set up by a technical colleague.

·        Check Checkboxes: Allows you to preselect certain checkboxes that should appear as checked in the generated PDF.

·        Is Signing Enabled Fetch: Controls whether the _Sign_ option is shown. The button will only appear if the defined FetchXML condition is met.

·        Is Signing Enabled Eror Message: The error message displayed when signing is not allowed (e.g., when the Sign button is disabled or hidden).

## Functional Configuration

### First Steps

After the initial setup is complete, you can start configuring the document in Word itself.

·        Install the Word Add-in\
First, install the Word add-in available via the “dox42 Downloads” page: [dox42 Download | Free-Program](https://www.dox42.com/Modules/Download) .

·        Request a License\
You can request a free license by emailing [hello@dox42.com](mailto:hello@dox42.com) , or you can use the free 1-month trial license.

·        Activate the Add-in\
Once the add-in is installed, you'll see a new dox42 tab in Word.

<figure><img src="../../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>

Click the Activate button to activate dox42.

<figure><img src="../../.gitbook/assets/image (236).png" alt=""><figcaption></figcaption></figure>

Before you start building your template, you’ll need a good XML file containing all the required data. It’s crucial that this XML includes all necessary attributes — without them, you won’t be able to generate your document correctly.

To generate the XML:

1. Go to your dox42 Template Configuration in Dynamics.
2. Ensure the following fields are filled in:
3. Default Entity ID
4. Default dox42 Language
5. Default User
6. Click the Generate JSON/XML button at the top of the screen to generate the XML file.&#x20;

{% hint style="warning" %}
Make sure the configuration is complete before generating the XML. If not, the file may be empty.
{% endhint %}

### XML Explained

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><p>&#x3C;crmfetch></p><p>               &#x3C;entityQueryContainer></p><p>                              &#x3C;valueEntityQuery></p><p>                                             &#x3C;attribute1>value&#x3C;/attribute1></p><p>                                             &#x3C;attribute2>value&#x3C;/attribute2></p><p>                                             ...</p><p>                              &#x3C;/valueEntityQuery></p><p>               &#x3C;/entityQueryContainer></p><p>&#x3C;/crmfetch></p></td></tr></tbody></table>

Detailed Explanation

1. \<crmfetch> (Root Element)\
   This is the root node of the document. It groups all fetched data.
2. Entity Query Containers\
   Each child element of \<crmfetch> (e.g., \<accountfetchquery>, \<contactsFetchQuery>, \<systemuser>) represents the result of a specific entity query.
3. Value Nodes (\<value...>)\
   These elements (e.g., \<valueaccountfetchquery>, \<valuecontactsFetchQuery>) represent individual records (rows). Each entity query can return one or more of these nodes.
4. Attributes of Each Record\
   Inside each \<value...> node, you’ll find fields/columns such as:
5. Standard attributes (e.g., name, emailaddress1, industrycode)
6. Display values (e.g., \_parentaccountid\_value\_displayvalue)
7. Keys (e.g., \_parentaccountid\_value)
8. Empty Elements\
   Some nodes may appear empty (e.g., \<aug\_htmltest />) if the value is null.
9. Metadata Attributes\
   Elements like odata.etag are metadata typically used for caching or concurrency control. These can be ignored in most templating scenarios.



Example: Contact Query

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><p>&#x3C;contactsFetchQuery></p><p>                    &#x3C;valuecontactsFetchQuery odata.etag="W/&#x26;quot;66428312&#x26;quot;"></p><p>                                        &#x3C;contactid>763d7c83-2a6c-ee11-9ae7-000d3a4a3c25&#x3C;/contactid></p><p>                                        &#x3C;fullname>Le Fred&#x3C;/fullname></p><p>                                        &#x3C;_parentaccountid_value_displayvalue>MHP's Account&#x3C;/_parentaccountid_value_displayvalue></p><p>                                        &#x3C;_parentaccountid_value>b0e9a65a-2780-eb11-a812-000d3abc7615&#x3C;/_parentaccountid_value></p><p>                                        &#x3C;industrycode_displayvalue>Building Supply Retail&#x3C;/industrycode_displayvalue></p><p>                                        &#x3C;industrycode>5&#x3C;/industrycode></p><p>                    &#x3C;/valuecontactsFetchQuery></p><p>&#x3C;/contactsFetchQuery></p></td></tr></tbody></table>

·        contactsFetchQuery = container for all contact records

·        valuecontactsFetchQuery = one record

·        contactid, fullname, … = record attributes

\
**Why This Format and not JSON?**

This structure makes it easy to:

* Support multiple datasets (queries) in a single XML file.
* Handle multiple records per entity.
* Access both raw values and display values in templates.
* JSON isn’t that well supported by dox42 and gives strange results.

### Creating your document

Once you have the XML and have saved it as a .xml file, you can start configuring your document.\
I won’t go into detail about all available options—there are plenty of tutorials and guidelines available both within our company and from dox42.

#### Step 1 – Setting up the Data Map:

Save your empty Word document.

Go to the dox42 tab in Word and click on “Data Map”.

<figure><img src="../../.gitbook/assets/image (237).png" alt=""><figcaption></figcaption></figure>

• Click on the “Input Parameter” button and create a parameter named language as shown below:

<figure><img src="../../.gitbook/assets/image (238).png" alt=""><figcaption></figcaption></figure>

_This allows you to dynamically use the language selected by the user within your document._

·        Next, create an RequestBody input parameter. This will hold the XML content passed by Power Automate when generating the document:

<figure><img src="../../.gitbook/assets/image (239).png" alt=""><figcaption></figcaption></figure>

• Before adding XML parts, close the Data Map Designer. You’ll be prompted to save your .dm file:

<figure><img src="../../.gitbook/assets/image (240).png" alt=""><figcaption></figcaption></figure>

• In the save dialog use the same name as your Word document (e.g. howTo.dm)

<figure><img src="../../.gitbook/assets/image (241).png" alt=""><figcaption></figcaption></figure>

• Ensure “Data Map and Document in Same Directory” is selected and click OK.

<figure><img src="../../.gitbook/assets/image (242).png" alt=""><figcaption></figcaption></figure>

·        Now we can begin adding the XML parts to the template:

* Open the Data Map again.
* Click on the “XML/JSON” button
* Enter a descriptive name
* Set the method to GET.
* For the URL or input, enter <%RequestBody%>; This tells dox42 to use the content of the RequestBody parameter as the XML input.

<figure><img src="../../.gitbook/assets/image (243).png" alt=""><figcaption></figcaption></figure>

·        Then click on “Init from XSD/XML/JSON/WSDL”. Use the “...” button to browse to your XML file and click “Load”.

·        Always select the value\<queryname> node to include the correct portion of the XML with all the necessary fields.

·        Leave all other settings as they are and click “OK”.

<figure><img src="../../.gitbook/assets/image (244).png" alt=""><figcaption></figcaption></figure>

• You will now see an XML part added—for example, for Contact Information.

<figure><img src="../../.gitbook/assets/image (245).png" alt=""><figcaption></figcaption></figure>

·        Repeat this process for all other value\<queryname> nodes. Once done, you're ready to start configuring your document layout.

·        Finally, close the window and save your changes.

#### Step 2 – Using the Data Map:

·        Once everything is configured in your Data Map, click on “Insert Data Field” in the dox42 tab.

·        A panel will appear on the right side of your Word window.

·        This panel lists all the fields you’ve defined in your Data Map.

·        To insert a field into your document, simply double-click on it.

·        You can also assign a data type to the field. Don’t forget to click “OK” afterward to apply the type to the field in your document.

<figure><img src="../../.gitbook/assets/image (246).png" alt=""><figcaption></figcaption></figure>

#### Step 3 – Testing your Template in Word:

Now you're ready to test your template in Word:

* Click on “Generate” in the dox42 tab.
* You’ll be prompted to save the document — click “OK”.
* Enter the language code as defined in your dox42 settings (e.g. nl-be).

<figure><img src="../../.gitbook/assets/image (247).png" alt=""><figcaption></figcaption></figure>

• Click “Choose File”, select your XML file, and then click “Generate”.

<figure><img src="../../.gitbook/assets/image (248).png" alt=""><figcaption></figcaption></figure>

• A new window will open displaying your generated document.

<figure><img src="../../.gitbook/assets/image (249).png" alt=""><figcaption></figcaption></figure>

#### Step 4 – Finalizing and Uploading Your Template

After successfully testing the document and verifying everything works as expected, follow these steps:

* Save your document to SharePoint, using the location defined in your Service Connection combined with your Template URL.
* Make sure that a document is available for each configured language.
* Don’t forget to upload your .dm file as well—this file is the core of your dox42 setup, containing all data sources and template configuration.
*

    <figure><img src="../../.gitbook/assets/image (250).png" alt=""><figcaption></figcaption></figure>
* Navigate to the entity where you want to generate the document.
* Select a record or open it, then click on “dox42 > Generate Document” in the command bar.

<figure><img src="../../.gitbook/assets/image (251).png" alt=""><figcaption></figcaption></figure>

• Select your template, configure all other required options, and click “Create Document”.

<figure><img src="../../.gitbook/assets/image (252).png" alt=""><figcaption></figcaption></figure>

• If everything was set up correctly, you’ll see a confirmation message indicating that the document was successfully created.

<figure><img src="../../.gitbook/assets/image (253).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (254).png" alt=""><figcaption></figcaption></figure>
