---
description: >-
  This document provides an overview the existing features for the Process
  Management solution.
---

# Process Management

## Activation module

Via the module 9A Raptor DWH > Setup > 9A Document Management parameters – tab Process Management can the process integration activated by choose a supported provider. The Process management solution supports two providers at this moment: Business events and AgilePoint. When you want to work with AgilePoint, please activate the Active checkbox and fill the necessary parameters in the group Setup. These fields aren’t used if you want to work with business events.

<figure><img src="../../.gitbook/assets/image (266).png" alt=""><figcaption></figcaption></figure>

To activate the process integration, navigate to the **9A Raptor DWH > Setup > 9A Raptor Document Warehouse Parameters** and select the **Process Management** tab.

The **Process Management** solution currently supports two providers:

1. **Business Events**
2. **AgilePoint** **NX**

To use **AgilePoint NX** as the provider, follow these steps:

* Check the **Active** checkbox.
* Fill in the required parameters in the **Setup** group.
  * **URL**: e.g. [https://as.nxone.eu](https://as.nxone.eu)
  * **Portal URL**: e.g. [https://app.nxone.eu](https://app.nxone.eu)
  * **Username**: Service account (ensure you include the domain) e.g. `nxone\user`
  * **Password**: The password for the specified service account

<div align="left"><figure><img src="../../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure></div>

## Functionalities

The following functionalities are available in the **Process Management** solution when used in combination with the **Input Management** solution. Each functionality indicates which process provider is supported.

1. **Start Process**:\
   Initiates a new process and stops the current process.\
   _&#x53;upported by all process providers._
2. **Cancel Process**:\
   Stops the current process.\
   _&#x53;upported by all process providers._
3. **Open Process**:\
   Provides an overview of the current process.\
   _&#x53;upported only by AgilePoint._

<figure><img src="../../.gitbook/assets/image (75).png" alt=""><figcaption></figcaption></figure>

Two new fields are added to the imported invoice data:

* **Current Process Status**: Displays the status of the current process.
* **Process Actual User**: Displays the user currently responsible for the process.

These fields enable the creation of custom views with filters, allowing you to:

* View and manage **open processes**.
* Identify the **responsible user** for each invoice.

<div align="left"><figure><img src="../../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure></div>

## Process comment integration

Since version 10.2021.8.1, it’s possible to put comments before start/cancel a process. This comment is stored in your imported invoice.Before starting with this functionality, the functionality should be activated in the 9A Raptor DWH parameters.

Starting from version **10.2021.8.1**, you can now add comments before starting or cancelling a process. These comments will be stored with the corresponding imported invoice.

Before using this functionality, ensure that it is activated in the **9A Raptor Document Warehouse Parameters**.

<div align="left"><figure><img src="../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure></div>

<figure><img src="../../.gitbook/assets/image (267).png" alt=""><figcaption></figcaption></figure>



## Actor Integration

Starting from **version 10.2021.8.1**, the **Process Management** solution includes support for actors. By default, there are six actors available:

* **First 2 Actors**: These represent the **vendor responsible** and **purchase requesters**.
* **Remaining 4 Actors**: These are optional actors that can be manually populated in your imported invoices.

To apply this feature to existing invoices, simply **reinitialize** the invoices, and the default actors will be automatically filled in.

<div align="left"><figure><img src="../../.gitbook/assets/image (78).png" alt=""><figcaption></figcaption></figure></div>

## Process history integration

Since version 10.2021.11.1, we included support for history in the Process Management solution. The purpose Is to fill every change In the process from the Power Platform or AgilePoint. This way, the end user has an idea of what is happening during the flow of current process.

Starting from **version 10.2021.11.1**, the **Process Management** solution now includes **history tracking**. This feature logs every change made to a process through Power Platform or AgilePoint.

The purpose of this functionality is to provide end users with a clear overview of the changes and actions that occur during the flow of the current process. By tracking these changes, users can easily understand the process progression and identify what has happened at each stage.

<div align="left"><figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption></figcaption></figure></div>

The current **history table** includes four fields that are available for logging changes during the process. These fields are **free-text** and do not have any validation or relationships with other existing tables. The fields are as follows:

1. **Created Date and Time**: The timestamp indicating when the change was made.
2. **Status**: A description of the current status of the process at the time of the change.
3. **Actual User**: The user responsible for the change or action at that point in the process.
4. **Comment**: A free-text field where additional context or notes about the change can be added.



## Developing workflows

To develop your own workflows using the Process Management entities in Finance & Operations, we refer to the Developers section: <br>

{% content-ref url="../../developers/d365-finance-and-operations/process-management.md" %}
[process-management.md](../../developers/d365-finance-and-operations/process-management.md)
{% endcontent-ref %}
