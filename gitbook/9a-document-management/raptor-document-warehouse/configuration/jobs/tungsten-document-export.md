# Tungsten Document Export

The 'Tungsten Document Export' job in Raptor allows you to export processed invoices from Tungsten AP Essentials and forward them to the Raptor E-Platform, where it can be distributed to systems like Dynamics 365 F\&O.

## Connecting E-Platform and Tungsten

To set up a Tungsten Document Export job, you need to create a service connection to both systems:

E-Platform: [#e-platform-service-connection](./#e-platform-service-connection "mention")

Tungsten AP Essentials (Document export): [#tungsten-service-connection](./#tungsten-service-connection "mention")

{% hint style="info" %}
Jobs created before April 2025 might not use Service connections yet and have their credentials stored inline in the 'Delta Fetch Settings' or 'E-Platform settings' section of the job. It is advised to switch to using Service credentials for more secure and easier maintainable credential storage.
{% endhint %}

## Configuring the job

Once both service connections are created, a job can created of type 'Tungsten Document Export'.\
Fill in the Tungsten Export connection as the Service Connection source and the E-Platform connection as the Service Connection destination.\
\
Add a cron schedule and service account ('On behalf of') to complete the job configuration.

