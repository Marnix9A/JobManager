# Environment Setup

The Environment Setup links and authenticates your Dynamics CE environment with a Raptor tenant. \
To do this, fill in the required parameters:\
\
**Development**: this checkbox should only be toggled on for development environments. Checking the 'Development' option will allow you to publish Raptor tabs on to your own forms, allowing users to open Raptor on the form using a tab.

{% hint style="warning" %}
Publishing a Raptor tab on your form creates an unmanaged layer. This is why the 'Development' setting should only be turned on for development environments.
{% endhint %}

**API URL**: the URL of the Raptor API environment which you're connecting to. Customers can always set this to https://raptor.9altitudes.com/apigateway

**External system**: the ID of your external system. See [external-systems.md](../../raptor-document-warehouse/configuration/external-systems.md "mention")

**Secret**: the secret of your external system. See [external-systems.md](../../raptor-document-warehouse/configuration/external-systems.md "mention")

**Act behalf of**: the user which will be used for background operations in Raptor. Make sure this user was added to your Raptor tenant with the external system assigned.

After clicking 'Validate', you should see a message 'You are connected to the 9A Raptor Document Warehouse'.&#x20;

{% hint style="info" %}
In case an error occurs, check if:

* The ID and secret of your external system are correct
* The 'Act behalf of' user was added in Raptor with the external system assigned
{% endhint %}

