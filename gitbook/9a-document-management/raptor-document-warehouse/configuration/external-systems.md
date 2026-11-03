# External Systems

An **external system** represents any external application that embeds or integrates with the Raptor Document Warehouse. External systems allow for a single sign-on authentication with Raptor, as well as managing the user access from that system.

Typical examples of external systems include:

* Dynamics 365 Finance & Operations
* Dynamics 365 Business Central
* Power Apps
* Other custom applications or integrations

### Single Sign-On

An external system can generate authentication tokens that allow users to access the 9A Raptor DWH user interface without signing in again. \
For example, this is the mechanism used when clicking the **Dino** icon in D365 F\&O.\
\
It is therefore important that users who access Raptor through an external system are first assigned to that external system in the **Raptor Configuration** panel.

### Linking Internal and External Users

Registering an external system alone is not sufficient. Each external user must also be linked to an **internal** 9A Raptor DWH user.

For every link, the following information is required:

* The **internal** 9A Raptor DWH user.
* The user's unique identifier in the external system (the _External username_)

This mapping allows a single internal user to be associated with multiple external systems, each using its own unique user identifier.

#### Example

The same person may have different identifiers in different systems:

| System             | User Identifier           |
| ------------------ | ------------------------- |
| D365 F\&O          | `john.doe@9altitudes.com` |
| Custom application | `johnd`                   |

Although these identifiers are different, they all represent the same user. By mapping each external identifier to a single internal 9A Raptor DWH user, the platform can correctly identify the user regardless of the source system.

> **Note:** An internal user can be linked to multiple external systems. However, only one user mapping is allowed per external system. Multiple mappings from the same external system to the same internal user are not supported.

### Token Validation

An authentication token is considered valid only if all of the following conditions are met:

* The external system exists and is active.
* The provided secret matches one of the two configured secrets for the external system.
* The supplied external user identifier is linked to an internal 9A Raptor DWH user.
* The linked internal user account is active.

{% hint style="info" %}
**Important remark**

Do not share the same external system between different applications. Each application should have its own dedicated external system configuration.

Sharing an external system across multiple applications can lead to security and maintenance issues. For example, secrets should be independently managed so that they can be rotated or changed for one application without affecting any other integrations.
{% endhint %}

## About secrets

When creating an external system, two secrets are generated:

* **Primary secret**
* **Alternate secret**

The recommended approach is to use the **primary secret** for authentication and securely store the **alternate secret** in a separate, protected location.

This setup allows secrets to be rotated without causing downtime. Since an external system secret functions like a password and may provide access to data for multiple users, it is important that compromised secrets can be replaced quickly and safely.

### Secret Rotation Procedure

If one of the secrets is suspected to be compromised, follow these steps:

1. Replace the **primary secret** in the application with the existing **alternate secret**.
2. In the Raptor web interface, click **Renew secret** once.
3. A new secret will be generated and displayed. Store this new secret securely.
4. Update the application configuration by replacing the old alternate secret with the newly generated secret.
5. In the Raptor web interface, click **Renew secret** once again.
6. Store the newly generated secret securely in a separate protected location. This becomes the new alternate secret.

After completing these steps, the application continues to operate without interruption while both secrets have been safely rotated.

<figure><img src="../../.gitbook/assets/image (506).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
After clicking the “Renew secret” button, the original “Primary secret” is voided, and the original When the **Renew secret** button is clicked, the following process takes place:

* The current **Primary secret** is invalidated and can no longer be used for authentication.
* The current **Alternate secret** is promoted to become the new **Primary secret**.
* A new secret is generated and becomes the new **Alternate secret**.

This means that after the first renewal:

* The original **Primary secret** is no longer valid.
* The original **Alternate secret** remains valid and becomes the new **Primary secret**.
* The newly generated secret becomes the new **Alternate secret**.

For this reason, the secret should be renewed a second time immediately after updating the application configuration. This repeats the rotation process and replaces both original secrets with newly generated secrets.

When performed correctly, secret rotation should have **no impact on the running application**. The application can continue authenticating throughout the process while the compromised secret is removed and the security risk is resolved.
{% endhint %}



## Creating an external system

To create a new external system, follow these steps:

1. Navigate to the **Configuration** page.
2. Open the **External Systems** tab.
3. Click the **+** button to create a new external system.
4. Set **Public** to **Yes**.
5. Click **Save**.

After saving, the external system will be created and two secrets will be displayed.

> **Important:** Store both secrets in a secure location immediately. These are application credentials and will only be displayed at this point. They cannot be retrieved again later.

After creating the external system, at least one user must be assigned to it before the system can be used for authentication.

## Revoking user access via an external system

To remove a user's access through an external system, follow these steps:

1. Select the relevant **external system** from the list.
2. In the external system details pane, select the user whose access should be removed.
3. Click the **Delete** button above the user list.

> **Note:** Removing a user from an external system only revokes access through that specific external system. The user can still sign in to Raptor through the web interface if they have valid web access permissions.

## Adding a user to an external system

To add a user to an external system, follow these steps:

1. Select the required **external system** from the list.
2. In the external system details pane, click the **+** button above the user list to add a new user.
3. Enter the required user details in the fields above the table:
   * **External user ID**: The unique identifier of the user as known by the external system.
   * **Internal user**: Select the corresponding existing user in Raptor.
4. Click **Save** to apply the changes.

After saving, the external user identifier will be linked to the selected internal Raptor user, allowing authentication through the configured external system.



