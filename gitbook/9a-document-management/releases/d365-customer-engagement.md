# D365 Customer Engagement

{% hint style="info" %}
Newer release notes can now be found on the [9altitudes release notes website](https://releasenotes.9altitudes.com/9A%20Productivity%20Suite/9A%20Raptor%20Document%20Warehouse/D365-Customer-Engagement/)!
{% endhint %}

### Raptor - CE Core

#### Raptor - CE Core (2025.11.24.2)

* The PCF control will now be bound with the connected user and not always the chosen Admin User
* The PCF Control will use the domainname instead of the internalemailadress of the User in CE

#### Raptor - CE Core (2025.11.13.1)

* Some Bug Solving
* Added extra Custom API for the Resolve Context

#### Raptor - CE Core (2025.11.5.3)

* Added entity form tabs
* Added tab translations
* Added raptor admin auto-assign based on the credentials page
* Solved some minor bugs
* Created new select attributes PCF Control

#### Raptor - CE Core (2025.20.10.1)

* New Raptor PCF Control
* Added Custom API for getting the Raptor Token
* Added possiblity to connect a lookup to the "Raptor Documents"-tab
* Solved the Translations Issues
* New Credentials Page
* Deprecation of the old Processes (Workflow Activities) -> Replaced with Custom API's and Plug-in's
* Created Console APP to Convert old PCF Control to new PCF Control
* Solved some minor issues in the Attachment Manager
* Added a Publish Functionality -> Will solve a lot of issues while configuring the tab
* Added a new Attachment Manager -> It's not depending on the D9A solution anymore

#### Raptor - CE Core (2025.2.20.1)

* Solving issues with the Email JavaScript.
* Adding the custom api for retrieving raptor Files and the content of the raptor Files.

#### Raptor - CE Core (2024.12.9.1)

* Adding new fields for extra possiblities with the "Attachment Manager".

#### Raptor - CE Core (2024.12.2.1)

* Adding extra security on the APP.
* Working with an "Raptor Administrator" to avoid Security Errors.

#### Raptor - CE Core (2024.11.25.1)

* Adding extra fields for the Initial Load Power Automate.

#### Raptor - CE Core (2024.11.13.1)

* Changes to the Custom API to add attachments to raptor.
* Added the "Parent Tag Ids" to the "Raptor Entity Configuration".

#### Raptor - CE Core (2024.11.6.1)

* Added Javascript for better support of the D9A Attachment Manager.
* Extra fields needed for the Flows.

#### Raptor - CE Core (2024.10.23.2)

* Adding extra fields on e-mail for tags/tempalte generation.
* Extra functionality to choose which mails attachments need to be sent to raptor.
* Changing names and solving minor bugs.
* Adding an extra Custom API to extract the attachments from a MSG or EML.

#### Raptor - CE Core (2024.9.9.3)

* Option to create EML from received e-mails.
* Adding Thumbnails + Sorting for the "Attachment Manager"
* Added Extra Power Automate Functionalities to retrieve/push data to/from raptor
* Added Extra Languages Support for 1036 (French) & 1043 (Dutch). Those or not the translations yet, but all text is now visible.

#### Raptor - CE Core (2024.7.8.1)

* Solved issue with the "Act on Behalf"-optionset that is empty on the "Raptor Credentials Page". You can use the "ExArte Raptor Administrator"-role on the user, then it's not language dependent.
* Added support for the "Attachment Manager"
* Added the functionality to be able to delete the data from notes / attachments and use raptor as "Data Storage" => It looks the same in CE, but the behind the scene, it gets data from Raptor

#### Raptor - CE Core (2023.7.11.1)

* Bug solved when connecting to the raptor via the "Raptor Credentials Page", when you connect for the first time

#### Raptor - CE Core (2023.6.22.1)

* Solved issues with fixed Guid's when creating the "Documents"-tab in code
* Solved other issues for better performance
* Added the "Attachment URL's"-functionality, to be able to see the Raptor attachments on your timeline + Direct link to the attachment in Raptor (first version)

#### Raptor - CE Core (2022.12.28.1)

* 10895 - Hotfix - Opportunity lifecycle field blocks Raptor

#### Raptor - CE Core (1.0.2.23)

* Added Fields / Views / Forms
* Added D365 CE Configuration APP
* Added Applicaton Ribbon (for buttons)
* Added PCF Controls:\
  \* Context App\
  \* Select Entity Picklist
* Added Plug-in Assemblies / Workflows
* Added Security Roles
* Added HTML Resource APP

### Raptor - Power Automate

{% hint style="info" %}
The Raptor - Power Automate solution has been merged with the Raptor - Core solution in the latest versions.
{% endhint %}

#### Raptor - Power Automate (2025.11.24.1)

* Solved an issue with the incorrect Connection Reference used within a Power Automate.

#### Raptor - Power Automate (2025.11.13.1)

* Deprecation of some extra flows.
* Removal of the not needed flows.
* Changed the "Raptor" connector in all the remaining flows.

#### Raptor - Power Automate (2025.20.10.1)

* Deprecation of all the HTTP Flows -> Everything works via Custom API now.
* Retrieving the token in the FLows is done via an Custom API.
* A lot of 'Environment Variables' are deprecated. Those are replaced by the Credential Page.

#### Raptor - Power Automate (2024.12.9.2)

* Changes to fill up the extra Date and Old Object fields.

#### Raptor - Power Automate (2024.12.2.1)

* Changing flows + adding extra security.

#### Raptor - Power Automate (2024.11.25.1)

* Adding a Flow for an Initial Load for the EMLs and Attachments.

#### Raptor - Power Automate (2024.11.13.3)

* Adding impersonation when adding attachments and notes to Raptor.

#### Raptor - Power Automate (2024.11.6.2)

* Added the functionality to add a tag for a sent/received e-mail.
* Changed flows for better performance.

#### Raptor - Power Automate (2024.10.22.3)

* Changing existing Power Automate flows to facilitate new functionalities.

#### Raptor - Power Automate (2024.9.9.2)

* Adding extra "Power Automates" to fetch/push data to Ratpor. We are deprecating the old way of working.
* Adding a "Power Automate" to get the Tags/Templates from Raptor and associate them with a document.
* Adding a "Power Automate" to create the EML files via a Custom API.

#### Raptor - Power Automate (2024.7.8.1)

* Adding a "Custom API" to fetch the body data from raptor
* Adding "Power Automates" to be able to get the file from raptor
* Adding extra Security where needed

#### Raptor - Power Automate (2023.9.8.1)

* Some minor bugs were fixed

#### Raptor - Power Automate (2023.6.22.1)

* Solved but in the, so that the "Attachment Manager" would work faster

#### Raptor - Power Automate (1.0.0.1)

* Raptor - Get Raptor File
* Raptor - Get Raptor File List
* Added Environment Variables:\
  \* D365-CE: Raptor Secret\
  \* D365-CE: Raptor System Id\
  \* D365-CE: Raptor User

### &#x20;Raptor - Custom Connector

{% hint style="info" %}
The Raptor Custom Connector has been deprecated in the latest versions. We now use the certified 9A [Raptor Document Warehouse connector](https://learn.microsoft.com/en-us/connectors/raptordocmanagement/).
{% endhint %}

#### Raptor - Custom Connector (2024.11.13.3)

Extra API call to get the tags details.

#### Raptor - Custom Connector (2024.10.23.1)

Adding extra API calls within the Raptor Connector (Query Templates by Code, Query Documents V2, Upload Documents with Parameters)

Adding the "Get Tag by Id"-functionality + solving the microsoft bug for the "API"-URLS that have multiple request methods (Get, Post, Delete, ...)

#### Raptor - Custom Connector (2024.9.9.1)

Adding extra API calls within the Raptor Connector (Getting Thumbnails, Getting the Document, ...)

#### Raptor - Custom Connector (2024.7.8.1)

Added extra functionality to fetch via Tags

#### Raptor - Custom Connector (2023.9.8.1)

Changed some security settings

#### Raptor - Custom Connector (2023.6.22.1)

Changed some security settings

#### Raptor - Custom Connector (1.0.0.4)

First version of the "Custom Connector"Added Environment Variables:\
\* Raptor Host URL&#x20;
