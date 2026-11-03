# Document management

## Setup

The document management integration can be activated through the following path:

**9A Raptor DWH** > **Setup** > **9A Raptor DWH Parameters** – tab **Document Management**.

After onboarding, an external system and secret key are provided for the F\&O environment. The URL remains the same for all customers, as **Document Warehouse** operates as a single multitenant environment.

<div align="left"><figure><img src="../../../.gitbook/assets/image (274).png" alt=""><figcaption></figcaption></figure></div>

A **service account** (the 'On behalf of' parameter) is required for all communication between D365 F\&O and the Raptor API. The service account should be a user in Raptor and assigned the 'D365-FO' external system (see [external-systems.md](../../../raptor-document-warehouse/configuration/external-systems.md "mention")).

## General

**Tag documents outside FO**

{% hint style="info" %}
This setting is deprecated and might cause issues when used in combination with cascading tag relations. Please use [#distribution-setup](document-management.md#distribution-setup "mention") instead.
{% endhint %}

For standard D365FO flows, documents attached through document handling (e.g., from a sales order) are automatically copied to related records like sales order confirmation journals or sales order invoice journals. When this parameter is enabled, documents that aren’t directly added to document handling but are available in the **Document Warehouse** will be searched and tagged with the appropriate label (e.g., sales order confirmation, invoice, etc.).

#### Distribution Setup

**Processing Mode Options:**

* **None**: No document distribution is performed.
* **Synchronous**: Documents are tagged or copied to a new tag within the same thread (real-time processing).
* **Asynchronous**: Documents are tagged or copied to a new tag in a separate thread (background processing).
