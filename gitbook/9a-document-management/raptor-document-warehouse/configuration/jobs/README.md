# Jobs

Jobs are specific tasks that are executed according to a scheduled time.\
Raptor has several types of jobs:

## Job configuration

Jobs can be found in the Raptor configuration panel in the tab 'Jobs'.&#x20;

<figure><img src="../../../.gitbook/assets/image (183).png" alt=""><figcaption></figcaption></figure>

Every job has a status indicated by a color. The colors can be:

* Gray: job has not run yet
* Purple: a job execution is running
* Green: last job execution was finished successfully
* Orange: last job execution ran into an error and will retry later
* Red: last job execution failed after multiple retries

A job also has a type. Available job types in Raptor are:

<table data-full-width="false"><thead><tr><th width="261">Job Type</th><th width="441">Function</th></tr></thead><tbody><tr><td>D365FO Taxonomy</td><td>Retrieves an export from Dynamics 365 F&#x26;O and generates tags based on it's contents.</td></tr><tr><td>D365FO Users</td><td>Retrieves an export from Dynamics 365 F&#x26;O and creates Raptor users based on it's contents.</td></tr><tr><td>D365FO Kofax Masterdata</td><td>Retrieves an export from Dynamics 365 F&#x26;O and pushes it as masterdata to Tungsten AP Essentials (formerly Kofax).</td></tr><tr><td>D365CE Taxonomy</td><td>Retrieves an export from Dynamics 365 CE and generates tags based on it's contents.</td></tr><tr><td>D365BC Taxonomy</td><td>Retrieves an export from Dynamics 365 BC and generates tags based on it's contents.</td></tr><tr><td>Kofax Document Export</td><td>Retrieves processed invoices from Tungsten AP Essentials (formerly Kofax) and forwards them to the E-Platform.</td></tr><tr><td>Azure AD - Users</td><td>Retrieves users from Azure Entra ID (formerly Active Directory) and creates them as Raptor user.</td></tr><tr><td>SQL Taxonomy</td><td>Retrieves an export from a SQL database and generated tags based on it's contents.</td></tr><tr><td>Dataverse Taxonomy</td><td>Retrieves an export from Dataverse and generated tags based on it's contents.</td></tr><tr><td>Dataverse Kofax Masterdata</td><td>Retrieves an export from Dataverse and pushes it as masterdata to Tungsten AP Essentials (formerly Kofax).</td></tr><tr><td>SQL Kofax Masterdata</td><td>Retrieves an export from a SQL database and pushes it as masterdata to Tungsten AP Essentials (formerly Kofax).</td></tr></tbody></table>



Next to a type and status, every job has:

* A unique ID
* A cron schedule: this is the schedule for the job execution in the cron-format. Cron schedules can be easily created using the website crontab: [https://crontab.guru/](https://crontab.guru/)

{% hint style="danger" %}
Cron schedules should be set up in a reasonable format. Scheduling jobs in a hyper frequent manner (e.g. every minute 24/7) will result in the job being deactivated. \
\
Jobs that proactively generate tags are usually not critical for the working of a production environment, as tags can always created ad-hoc. For these type of jobs we advise a schedule limited of max. 3 times a day, preferably outside business hours or in the weekend.
{% endhint %}

* A service connection (Source): the connection used to retrieve data. See [#service-connections](./#service-connections "mention")
* A service connection (Destination): the connection used to push data. See [#service-connections](./#service-connections "mention")
* A service account (On behalf of): this is the Raptor user that will be used to make any API calls to Raptor during the job, if applicable.
* Delta packager: the packager service that will be used to retrieve data for the job.



## Service connections

Service connections are used by jobs to connect to external services, such as Dynamics 365, Tungsten AP Essentials or a SQL database. Service connections allow you to store credentials in a safe, central place. Updating a service connection will have an effect on all jobs making use of that connection.

Service connections can be found in the 'Jobs' configuration, tab 'Service Connections'.

### Creating a service connection

To create a service connection, click the '+' icon.\
Provide a meaningful name for your connection and select the service type that you will be connecting to. Based on the selected service type, you can choose the purpose of this connection under 'Data'.<br>

<figure><img src="../../../.gitbook/assets/image (185).png" alt=""><figcaption></figcaption></figure>

Click 'Save' to create the service connection and fill in the required fields.



### Dynamics 365 service connections

Connections to Dynamics 365 are made with the OAuth2.0 protocol using an [App Registration](https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-register-app) in Azure. Raptor uses the ID of the client application as well as the secret value and Directory ID.\
Depending on which Dynamics environment you are connecting to, the app registration may need different API permissions.

#### Dynamics 365 F\&O

For F\&O, the app registration needs following API permissions:

* Dynamics ERP
  * AX.FullAccess (Delegated)
  * CustomService.FullAccess (Delegated)
  * Odata.FullAccess (Delegated)
* Microsoft Graph
  * User.Read (Delegated)

{% hint style="info" %}
Make sure that the client app ID is registered in your F\&O environment under System administration > Setup > Microsoft Entra ID applications.
{% endhint %}

#### Dynamics 365 CE

For CE, the app registration needs following API permissions:

* Dynamics CRM
  * user\_impersonation (Delegated)
* Microsoft Graph
  * User.Read (Delegated)

{% hint style="info" %}
Make sure that the client app is registered as an [application user](https://learn.microsoft.com/en-us/power-platform/admin/manage-application-users) with sufficient permissions in the Power Platform portal.
{% endhint %}

#### Dynamics 365 BC

For BC, the app registration needs following API permissions:<br>

* Dynamics 365 Business Central
  * API.ReadWrite.All (Application)
* Microsoft Graph
  * User.Read (Delegated)

{% hint style="info" %}
Make sure that the client app is registered in the Microsoft Entra Application form in Business Central with sufficient permissions.
{% endhint %}

### Tungsten service connection

The Tungsten service connection allows you to connect Raptor to Tungsten AP Essentials to push masterdata (Master Data type) or export processed invoices (Document Export type):<br>

<figure><img src="../../../.gitbook/assets/image (718).png" alt=""><figcaption></figcaption></figure>

Creating a Tungsten service connection requires a service account in Tungsten with sufficient permissions on the masterdata and/or invoices. You will need:

* The user name of the service account
* The password of the service account
* The Tungsten API key (filled in by default)

### E-Platform service connection

The E-Platform service connection allows you to connect to the Raptor E-Platform, used to distribute electronic messages across systems.

{% hint style="info" %}
The E-Platform solution is in EOD state (End-Of-Development) and can only be configured or accessed by 9altitudes consultants. For service requests, please reach out to your implementation consultant or send a mail to support@9altitudes.com.
{% endhint %}

To create a service connection for E-Platform, you will need:

* The Uri of the E-Platform route
* The E-Platform API version (filled in by default - 2.0)
* The user name of the E-Platform account
* The password of the E-Platform account
