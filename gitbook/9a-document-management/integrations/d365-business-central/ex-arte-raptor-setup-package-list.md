---
hidden: true
---

# Ex Arte Raptor Setup (Package) list

In this form, Packages are defined that can be requested by a Raptor Taxonomy job. For each package we can specify the API endpoints (defined in previous section) that the package should include. The package code will be defined in the taxonomy job.

For each API In the package we can also specify If all data from the endpoint should be forwarded, or only newly modified/created data (= Delta Migration), this setting should be turned on after a full sync by the taxonomy job was completed. If let turned off, the taxonomy job might take exponentially more time as it needs to re-sync all data In the system every time.

&#x20;

<figure><img src="../../.gitbook/assets/image (565).png" alt=""><figcaption></figcaption></figure>

\
You can’t edit the checkbox Custom API because you need to change this in Ex Arte Raptor API Call Setup List

<figure><img src="../../.gitbook/assets/image (547).png" alt=""><figcaption></figcaption></figure>

You don’t have to use the filter field

Important: The OData settings of your on-prem server should be: (You can access this in the NavAdministrator)

&#x20;

<figure><img src="../../.gitbook/assets/image (578).png" alt=""><figcaption></figcaption></figure>

The Credential Type should be NavUserPassword.

<figure><img src="../../.gitbook/assets/image (579).png" alt=""><figcaption></figcaption></figure>

&#x20;
