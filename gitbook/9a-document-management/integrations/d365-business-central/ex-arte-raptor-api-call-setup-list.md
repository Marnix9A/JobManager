---
hidden: true
---

# Ex Arte Raptor API Call Setup List

In this form we specify the API endpoints that Raptor can use to fetch table data.

The list will be prefilled with the default api endpoints.\
Additional (custom) API's can be added by a BC technical consultant.

<figure><img src="../../.gitbook/assets/image (512).png" alt=""><figcaption></figcaption></figure>

Column 2 : Filter Field functionality is not working at this moment. This field also has no added value

Column 3: The checkmark Custom API specifies If the data should be fetched from the default API endpoint: /api/v1.0/(before BC21) or /api/v2.0/(bc21 and onwards) (If unchecked) or from the custom Raptor api endpoint:  api/raptor/custom/v1.0/ (If checked).

## Raptor On-Prem Configuration:

### Setup

You can access the Jobs in Raptor if you use this path:\
&#x20;                   Raptor> Configuration> Job

### Authentication

Select the D365BCTaxonomy with the right Leagal Entity (Company)

<figure><img src="../../.gitbook/assets/image (573).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
D365 Business Central Taxonomy synchronization In Document Warehouse uses basic authentication (only) to connect to D365BC. OAuth2.0 is added as an  alternative. OAuth2.0 is required for use with version as of BC21. Lower versions can still use Basic Authentication
{% endhint %}

&#x20;

You have to make sure that the User you choose, exists in your Company (Legal Entity)

<figure><img src="../../.gitbook/assets/image (421).png" alt=""><figcaption></figcaption></figure>

### Delta Fetch Settings

<figure><img src="../../.gitbook/assets/image (568).png" alt=""><figcaption></figcaption></figure>

The Package ID field will be explained In the next section

The URL will be the URL of the Business Central environment.

Raptor Base Path Is:  /api/raptor/custom/v1.0/

Entity Path: /api/v1.0/

Company ID: Search to Companies (Table 2000000006) en press Cntrl+Alt+F1 and search for ID. Enter this ID In Company ID.

<figure><img src="../../.gitbook/assets/image (416).png" alt=""><figcaption></figcaption></figure>

## Raptor Cloud Configuration:

### **Setup**

You can access the Jobs in Raptor if you use this path:\
&#x20;                   Raptor> Configuration> Job

### **Authentication**

Select the D365BCTaxonomy with the right Leagal Entity (Company)

<figure><img src="../../.gitbook/assets/image (510).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
D365 Business Central Taxonomy synchronization In Document Warehouse uses basic authentication (only) to connect to D365BC. OAuth2.0 is added as an  alternative. OAuth2.0 is required for use with version as of BC21. Lower versions can still use Basic Authentication
{% endhint %}

The Active Directory Tenant, Client app Id and Client app secret should be provided by the customer.\
Azure resource will always be: https://api.businesscentral.dynamics.com

It's important to Enable the Azure Active Directory & give the right permissions (SUPER(DATA))

<figure><img src="../../.gitbook/assets/image (335).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (499).png" alt=""><figcaption></figcaption></figure>



### **Delta Fetch Settings**

<figure><img src="../../.gitbook/assets/image (536).png" alt=""><figcaption></figcaption></figure>

The Package ID field will be explained In the next section

The URL will be the URL of the Business Central environment.

Raptor Base Path Is:  /api/raptor/custom/v1.0/

Entity Path: /api/v2.0/

Company ID: Search to Companies (Table 2000000006) en press Cntrl+Alt+F1 and search for ID. Enter this ID In Company ID.

<figure><img src="../../.gitbook/assets/image (552).png" alt=""><figcaption></figcaption></figure>

You might have a problem with the Taxonomy Job of Items, but you can solve this by using this parameters:

<figure><img src="../../.gitbook/assets/image (558).png" alt=""><figcaption></figcaption></figure>

You don't need the vendorItemNumber or vendorNumber for the Taxonomy job.
