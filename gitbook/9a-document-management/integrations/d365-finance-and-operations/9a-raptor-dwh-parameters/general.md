# General

## Enable HTTP Logging

See [#http-logging](../inquiries-and-reports.md#http-logging "mention")

## Timeout

Sets the timeout in milliseconds for outgoing network requests.\
When set to 0, it defaults to 100000 (100 seconds).\
This setting can be put higher in case you encounter timeout errors.

## Use Key Vault

**Azure Key Vault Integration Overview**

Starting with the release of **9A Document Management 10.2021.10.1**, Azure Key Vault is supported for storing secret keys and passwords for integrations. This documentation provides details on setting up Azure Key Vault in D365 F\&O. For more information on specific integrations, refer to related documentation.

**Key Resources for Azure Key Vault**

* [Azure Key Vault Documentation | Microsoft Docs](https://docs.microsoft.com/azure/key-vault/)
* [Set Up Azure Key Vault Client - Dynamics 365 | Microsoft Docs](https://docs.microsoft.com/dynamics365/)
* Best Practices for Azure Key Vault Usage

**Key Considerations**

* **Resource Groups**: Resource group usage varies by customer policies.
  * Use separate resource groups for **non-production** and **production** environments.

**Setting Up Azure Key Vault for D365 F\&O**

1. **Create an Azure Key Vault**.
2. **Register an Azure App** and generate a **secret key**.
3. **Create an Access Policy** in the Key Vault and link it to the App registration.

<figure><img src="../../../.gitbook/assets/image (272).png" alt=""><figcaption></figcaption></figure>

**Adding New Secrets**

The creation of secrets depends on the modules the customer has purchased. It is recommended to use the following names, but custom names can be used if necessary:

* **ContextManagement**: Secret key for access to Document Warehouse.
* **OutputManagementDox42**: Client secret for the Dox42 Azure App registration.
* **OutputManagementDox42User**: Password of the user account linked to Dox42.
* **OutputManagementSmartFlows**: API key for access to SmartFlows.
* **ProcessManagementAgilePointUser**: Password of the user account linked to AgilePoint.

**Configuring Azure Key Vault in D365 F\&O**

Once the steps above are completed, configure Azure Key Vault in D365 F\&O as follows:

1. **Set the Default Company**: Set the company to **DAT** for Azure Key Vault parameters. The Key Vault parameters are stored per company, but the Raptor parameters are stored globally.
2. **Access Key Vault Parameters**:
   * Navigate to **System Administration** > **Setup** > **Key Vault Parameters**.
   * Create a new Key Vault setup with the name **'RaptorKeys'**.
   * Enter the following required parameters:
     * **Key Vault URL**: The Vault URI (can be found in the Azure Key Vault Overview).
     * **Key Vault Client**: Application ID of the App registration used for authentication between D365FO and Azure Key Vault.
     * **Key Vault Secret Key**: The secret key from the App registration (step 2).
3. **Create New Secrets**:
   * The secret names must match the proposed names below to ensure proper integration. The "Secret" field in D365FO should match the secrets created in Azure Key Vault (step 3). Set the **secret type** to 'Manual'.
     * **RaptorDocumentManagementSecret**
     * **RaptorOutputManagementDox42Secret**
     * **RaptorOutputManagementDox42UserPwd**
     * **RaptorOutputManagementSmartFlowsSecret**
     * **RaptorProcessManagementAgilePointUserPwd**
   * Format the **Secret URL** as: `vault://keyVaultName/keyVaultSecretName`.

**Activating Azure Key Vault Integration in 9A Document Management**

After the setup is complete, activate the Azure Key Vault integration:

1. Navigate to **9A Raptor DWH Parameters** via **9A Raptor DWH** > **Setup**.
2. Enable **Use Key Vault** and complete the necessary parameters for existing integrations, including endpoints and user accounts.

<figure><img src="../../../.gitbook/assets/image (273).png" alt=""><figcaption></figcaption></figure>

