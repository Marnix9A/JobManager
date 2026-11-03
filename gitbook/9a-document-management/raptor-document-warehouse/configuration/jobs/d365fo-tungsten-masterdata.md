# D365FO Tungsten Masterdata

The 'D365FO Tungsten Masterdata' job in Raptor allows you to take an export from D365 Finance & Operations using the Data Management feature, and upload it as masterdata to Tungsten AP Essentials.

## Connecting D365 and Tungsten

To set up a Tungsten Masterdata job, you need to create a service connection to both systems:

Dynamics 365 F\&O: [#dynamics-365-f-and-o](./#dynamics-365-f-and-o "mention")

Tungsten AP Essentials (Master data): [#tungsten-service-connection](./#tungsten-service-connection "mention")

{% hint style="info" %}
Jobs created before April 2025 might not use Service connections yet and have their credentials stored inline in the 'Authentication' or 'Entity configuration' section of the job. It is advised to switch to using Service credentials for more secure and easier maintainable credential storage.
{% endhint %}

## Setting up the Data Management project

In D365 F\&O, an export project should be created which will export the masterdata needed in Tungsten. During customer onboarding, this project is usually created beforehand with the name 'RAPTOR\_KOFAX'. By default it contains the entities Vendors, Bank accounts and Purchase orders.\
All entities should be set to 'Incremental push only' to avoid continuous large exports.

## Delta Fetch Settings

Once both systems are connected through service connection, a new Raptor job can be created.\
Here the Service connection (Source) is the D365 service connection and the Service connection (Destination) is the Tungsten service connection.

In the 'Delta Fetch Settings', the Data Management export project in D365 should be specified.\
Enter the required parameters:

* Uri: this should be the same as in the F\&O service connection
* Definition Group Id: the name of the export project in Data Management (typically called 'RAPTOR-KOFAX)
* Package Name: name of the package as your internal reference, free to choose
* Legal Entity: the legal entity for which the data should be exported (eg. DAT)
* Retention days: determines for how many days the data export should be stored in Raptor - for recovery

## Entity configuration

In the 'Entity configuration' panel, the mapping from D365 to Tungsten is specified in JSON format.

The 'organizationId' parameter should contain the ID of the buyer in Tungsten which you wish to sync the masterdata to.

The 'mappings' parameter contains the mapping from the F\&O data entity to the Tungsten tables.\
The configuration below contains the default mappings.\
For a full overview of the available fields in Tungsten, visit [https://services.readsoftonline.com/documentation/rest#masterdata](https://services.readsoftonline.com/documentation/rest#masterdata)

The 'incrementalPush' parameter determines if the data export is added in add-or-update mode (true) or replace mode (false). Replace mode will delete all existing masterdata for that table and replace it with the exported data from F\&O.

{% hint style="info" %}
If you wish to push a boolean field to Tungsten (such as the 'Blocked' field), make sure that the field in D365 is exported as "1" or "0".&#x20;
{% endhint %}

```
{
     "kofaxConnection": {
          "organizationId": "15203a050cae4e232323c149224b48103"
     },
     "mappings": [
          {
               "EntityNameExternal": "VENDVENDORV2ENTITY",
               "masterdataObjectName": "suppliers",
               "fieldMapping": {
                    "VENDORACCOUNTNUMBER": "SupplierNumber",
                    "VENDORORGANIZATIONNAME": "Name",
                    "TAXEXEMPTNUMBER": "TaxRegistrationNumber",
                    "ADDRESSCITY": "City",
                    "ADDRESSSTREET": "Street",
                    "ADDRESSZIPCODE": "PostalCode",
                    "ORGANIZATIONNUMBER": "OrganizationNunmber",
                    "PRIMARYPHONENUMBER": "TelephoneNumber"
               },
               "incrementalPush": true
          },
          {
               "EntityNameExternal": "PURCHPURCHASEORDERHEADERV2ENTITY",
               "masterdataObjectName": "purchaseorders",
               "fieldMapping": {
                    "PURCHASEORDERNUMBER": "OrderNumber",
                    "ORDERVENDORACCOUNTNUMBER": "SupplierNumber",
                    "CURRENCYCODE": "CurrencyCode",
                    "ACCOUNTINGDATE": "DateCreated"
               },
               "incrementalPush": true
          },
          {
               "EntityNameExternal": "VENDVENDORBANKACCOUNTENTITY",
               "masterdataObjectName": "supplierbankaccounts",
               "fieldMapping": {
                    "BANKNAME": "BankName",
                    "VENDORACCOUNTNUMBER": "SupplierNumber",
                    "ROUTINGNUMBER": "BankNumber",
                    "IBAN": "AccountNumber"
               },
               "incrementalPush": true
          }
     ]
}
```

