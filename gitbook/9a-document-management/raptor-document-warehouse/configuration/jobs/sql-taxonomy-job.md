# SQL Taxonomy Job

The SQL Taxonomy job retrieves masterdata from a SQL database. Raptor will use the exported data to generate tags from it using the [entity-configuration.md](../entity-configuration.md "mention").\
Taxonomy jobs are useful to proactively create tags that might be useful for Raptor users.

{% hint style="info" %}
In most cases, Raptor integrations are capable of making tags ad-hoc, whenever they are needed. Taxonomy jobs are therefore not essential for a working production environment. Their primary purpose is to make tags available for manual search in Raptor.
{% endhint %}

SQL taxonomy Taxonomy jobs use a Source service connection to a SQL database (see [#service-connections](./#service-connections "mention")) and can use the Default delta packager (for publicly accessible databases) or a custom delta packager for on-premise databases. Contact a 9altitudes consultant if a custom delta packager needs to be set up.



To configure a SQL sync job, the following components must be defined:

1. **Target Database Connection**\
   Specify the connection string for the source SQL database.
2. **SQL Queries**\
   Provide the SQL queries to retrieve the required data. You can:
   * Use views or direct `SELECT` statements
   * Include SQL parameters (e.g., timestamp filtering)
   * Rename columns using `AS`
   * Apply any SQL logic, as long as the final output is a single result set (table)
3. **Delta Sync (Optional)**\
   To enable delta (incremental) synchronization:
   * Define a storage connection string to track job progress
   * Specify a schema where progress metadata will be stored
   * Use a timestamp parameter in your queries to fetch only changed/new records

All delta-related settings are defined in the **`Delta Fetch`** section of the configuration.

#### Example Configuration

Below is a sample JSON configuration for a SQL sync job:

```json
{
  "source": "SQL",
  "raptorTenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "TaxonomyConfig": {
    "UseEntitySource": "EXAMPLE"
  },
  "packageInfo": {
    "package": "TEST-PACKAGE",
    "source": {
      "connectionString": "Server=SRV\\DB;Database=XX;User Id=USR;Password=PASS;"
    },
    "storage": {
      "connectionString": "inherit",
      "schema": "raptor-integration"
    },
    "entities": [
      {
        "name": "INVOICES",
        "select": "
        DECLARE @date AS NVARCHAR(50);
        IF (@timestamp IS NULL) 
          SET @date = ''; 
        ELSE 
          SET @date = CONVERT(varchar, @timestamp, 23); 
        
        SELECT 
          [inv].[id] AS [ID], 
          [inv].[net amount] AS [AMOUNT],
          [inv].[ref] AS [CUSTOMER]
        FROM [dbo].[invoice-table] AS [inv]
        WHERE [inv].[change] >= @date OR [inv].createdAt >= @date",
        "timestampParameter": "timestamp"
      },
      {
        "name": "ORDERS",
        "select": "SELECT * FROM [dbo].[ORDERS]"
      },
      {
        "name": "USERS",
        "select": "SELECT * FROM [dbo].[user table]",
        "timestampParameter": "none"
      }
    ]
  }
}
```

#### Explanation of the Configuration

* **Entities Exported:**\
  The configuration defines three entities: `INVOICES`, `ORDERS`, and `USERS`. The job output will be a ZIP file containing three XML files:
  * `INVOICES.xml`
  * `ORDERS.xml`
  * `USERS.xml`
* **Delta Sync Behavior:**
  * The `INVOICES` query uses the `@timestamp` parameter, so only changed or newly created records are fetched.
  * The `ORDERS` and `USERS` queries do not filter on timestamp, so they will always return the full table contents.
* **Column Mapping and Custom Logic:**\
  The `INVOICES` query demonstrates key features:
  * Selecting specific columns
  * Renaming columns using `AS`
  * Incorporating conditional logic while ensuring a single `SELECT` statement is returned
* **Storage Configuration:**
  * `connectionString: "inherit"` allows the storage connection to be inherited when running in a hosted environment (e.g., 9Altitudes server park).
  * For on-premise execution, you may need to explicitly define this connection string.
  * The `schema` is used to store delta progress and must exist in the database. For cloud deployments, it will be created by 9Altitudes. For on-premise use, ensure the schema exists and the configured login has full access (read/write/create).

***

#### Important Notes

* Column names must be valid XML tag names.
* Column names must match those defined in the [entity-configuration.md](../entity-configuration.md "mention").
* You can override the default entity configuration source by setting `TaxonomyConfig.UseEntitySource`. In the example above, it uses the configuration from source `"EXAMPLE"`.
* To perform a full sync instead of a delta sync, you can change the `package` name. This resets the stored timestamp.
