---
description: >-
  This article demonstrates how you can use the Raptor Process Management
  functionalities in F&O to build your custom workflow logic.
---

# Process Management

### Using Actor Integration

The **Process Management** solution includes support for actors, which can be accessed via the **ProcessInstanceActorsTable** entity. Below is how to use this integration to retrieve actor information for a specific imported invoice.

**Entity Details**

* **Entity Name**: `EXAProcessInstanceActorsTableEntity`
* **Public Collection Name**: `ProcessInstanceActorsTable`
* **Public Entity Name**: `ProcessInstanceActorsTable`

**HTTP Request Example**

When a process is started, you can create an HTTP request to retrieve the list of actors associated with a specific imported invoice. Use the following format:

```
https://d365fo-environment.cloudax.dynamics.com/data/ProcessInstanceActorsTable(dataAreaId='frrt',RefTableName='EXAPurchInvoiceImported',IdentifierId='FRRT-000000121')/
```

* **dataAreaId**: The corresponding legal entity.
* **RefTableName**: Always `EXAPurchInvoiceImported`.
* **IdentifierId**: The unique number of the imported invoice (this is the document number).

**Example Response**

The response will contain detailed information about the actors related to the specified invoice, including their personnel numbers, names, and primary email addresses:

```
{
    "@odata.context": "https://d365fo-environment.cloudax.dynamics.com/data/$metadata#ProcessInstanceActorsTables/$entity",
    "@odata.etag": "W/\"JzE0NzUzNzgyMDcsNTYzNzE1MzU3Nic=\"",
    "dataAreaId": "frrt",
    "RefTableName": "EXAPurchInvoiceImported",
    "IdentifierId": "FRRT-000000121",
    "ActorPurchaseRequester_PersonnelNumber": "000001",
    "Actor2_PersonEmail": "pierre@contoso.com",
    "Actor3_PersonEmail": "april@contoso.com",
    "ActorPurchaseRequester_PersonEmail": "jodi@contoso.com",
    "Actor1_PersonnelNumber": "000021",
    "ActorVendorResponsible_PersonEmail": "theresa@contoso.com",
    "Actor3_PersonnelNumber": "000045",
    "Actor3_PersonName": "April Stewart",
    "Actor2_PersonName": "Pierre Hezi",
    "ActorVendorResponsible_PersonnelNumber": "000005",
    "Actor1_PersonEmail": "reina@contoso.com",
    "Actor4_PersonnelNumber": "000060",
    "Actor1_PersonName": "Reina Cabatana",
    "Actor4_PersonName": "Tjeerd Veninga",
    "ActorPurchaseRequester_PersonName": "Jodi Christiansen",
    "Actor4_PersonEmail": "tjeerdv@contoso.com",
    "Actor2_PersonnelNumber": "000008",
    "ActorVendorResponsible_PersonName": "Theresa Jayne"
}

```

**Response Details**

The response includes the following information for each actor:

* **Personnel Number**: Unique identifier for the worker.
* **Name**: The full name of the worker.
* **Primary Email Address**: The worker's primary email address, sourced from their contact information in the system.

This data allows you to track which actors are involved in the process and provides easy access to their contact details for further communication.



### Using History Integration

The **Process Management** solution includes support for **process history**, which allows you to track changes and log actions during the flow of a process. The process history can be accessed and updated through HTTP requests.

**Entity Details**

* **Entity Name**: `EXAProcessInstanceHistoryTableEntity`
* **Public Collection Name**: `ProcessInstanceHistoryTables`
* **Public Entity Name**: `ProcessInstanceHistoryTable`

**Process History Creation**

When a process is started, you can create a process history record externally by sending an **HTTP request** with a JSON payload in the request body. This enables you to log the change or action associated with the process.

**HTTP Request Example**

To create a history record, send a POST request to the following endpoint:

```
bashCopyhttps://d365fo-environment.cloudax.dynamics.com/data/ProcessInstanceHistoryTables
```

**Example Request Payload**

Below is an example of the JSON payload that you would include in the body of the POST request. This example represents a record in the process history:

```json
{
    "CreatedDateTime": "2025-03-14T12:34:56",
    "Status": "Process Started",
    "ActualUser": "user@example.com",
    "Comment": "Process has been initiated successfully."
}
```

**Explanation of Payload Fields:**

* **CreatedDateTime**: The timestamp when the history record is created.
* **Status**: The current status of the process at the time the record is created (e.g., "Process Started", "Process Completed").
* **ActualUser**: The user who triggered the action or change.
* **Comment**: Any additional notes or details about the action or status.

By using this HTTP request and JSON payload, you can programmatically create process history records from external systems like Power Platform or AgilePoint.

When you query the **ProcessInstanceHistoryTable** entity, you will receive a response that includes details about the process history records. Below is an example of the HTTP response that you would receive:

```json
jsonCopy{
    "@odata.context": "https://d365fo-environment.cloudax.dynamics.com/data/$metadata#ProcessInstanceHistoryTables",
    "value": [
        {
            "@odata.etag": "W/\"JzEsNTYzNzE0NzU3Nic=\"",
            "dataAreaId": "frrt",
            "RefTableName": "EXAPurchInvoiceImported",
            "IdentifierId": "FRRT-000000122",
            "CreationDateTime": "2021-08-02T13:17:48Z",
            "Comment": "test multiline thing",
            "Status": "Start",
            "User": "Other"
        },
        {
            "@odata.etag": "W/\"JzEsNTYzNzE0NzU3Nyc=\"",
            "dataAreaId": "frrt",
            "RefTableName": "EXAPurchInvoiceImported",
            "IdentifierId": "FRRT-000000123",
            "CreationDateTime": "2021-08-02T13:18:05Z",
            "Comment": "test multiline thing",
            "Status": "Start",
            "User": "Other"
        },
        {
            "@odata.etag": "W/\"JzEsNTYzNzE0NzU3OCc=\"",
            "dataAreaId": "frrt",
            "RefTableName": "EXAPurchInvoiceImported",
            "IdentifierId": "FRRT-000000123",
            "CreationDateTime": "2021-08-02T12:18:05Z",
            "Comment": "test multiline thing",
            "Status": "Start",
            "User": "Other"
        }
    ]
}
```
