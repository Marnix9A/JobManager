---
description: >-
  The Approval Dashboard is a Power App developed by 9altitudes that seamlessly
  integrates with the Process Management module as part of the Raptor D365 F&O
  integration.
---

# Approval Dashboard

## About Approval Dashboard

The Approval Dashboard app enables users to manage approval workflows outside the ERP system while leveraging the Raptor Document Warehouse to visualize the documents requiring approval.\
\
The Power App is provided as a Kickstart package with essential approval functionality. It is delivered as an Unmanaged solution, allowing low-code developers to customize and extend the app to meet your organization’s specific needs.

## **Accessing the Power App**

Depending on your setup, you can open the Power App either through **Power Apps (Dataverse)** or **Microsoft Teams (Dataverse for Teams)**.

***

#### **1. Access via Power Apps (Dataverse license)**

1. Open your browser and go to https://make.powerapps.com.
2. Sign in with your Microsoft 365 account.
3. In the left-hand menu, select **Apps**.
4. Find the app you want to open — for example, **Approval Dashboard**.
5. Click the app name to launch it.
6. _(Optional)_ Pin the app to your favorites for quicker access next time.

<figure><img src="../.gitbook/assets/image (708).png" alt=""><figcaption></figcaption></figure>

***

#### **2. Access via Microsoft Teams (Dataverse for Teams)**

1. Open **Microsoft Teams**.
2. Go to the **team** or **channel** where the app has been published.
3. In the tab bar at the top, look for the **Power App tab** (e.g., _Approval Dashboard_).
4. Click the tab to open the app directly within Teams.
5. _(Optional)_ If you don’t see the tab, click the **Apps** icon in the left sidebar and search for the app name to add it manually.

<figure><img src="../.gitbook/assets/image (709).png" alt=""><figcaption></figcaption></figure>

***

{% hint style="info" %}
If you’re unsure which version you have access to (Dataverse or Dataverse for Teams), check with your system administrator or IT contact.
{% endhint %}

## **Sharing the Power App with Other Users**

You can easily share the Power App with colleagues so they can also access and use it.\
The sharing method depends on where the app is hosted.

***

#### **1. Sharing from Power Apps (Dataverse license)**

1. Go to https://make.powerapps.com and sign in.
2. In the left-hand menu, select **Apps**.
3. Find the app you want to share (for example, **Approval Dashboard**).
4. Click the **three dots (…)** next to the app name and choose **Share**.
5. In the sharing panel:
   * Enter the names or email addresses of the users or security groups you want to share the app with.
   * Choose the appropriate **permissions**:
     * **Can use** – allows users to run the app.
     * **Can edit** – allows users to modify the app (for makers or low-code developers).
6. Click **Share** to confirm.
7. The users will now see the app in their **Power Apps** environment.

***

#### **2. Sharing from Microsoft Teams (Dataverse for Teams)**

1. Open **Microsoft Teams**.
2. Navigate to the **team** where the app is published.
3. Go to the **Power Apps tab** (e.g., _Approval Dashboard_).
4. Click the **More options (⋯)** icon next to the tab name, and select **Manage access** (or **App details** depending on your Teams version).
5. Add additional team members if needed — everyone who is part of that **Team** automatically gets access to the app.
6. If you need to share the app with users **outside** the Team, you can either:
   * Add them as **members** of the Team, or
   * Publish the app in another Team or environment.

{% hint style="info" %}
For security and performance reasons, it’s best practice to share the app with **security groups** or **Teams**, rather than with individual users. This makes permission management easier over time.
{% endhint %}

## **Adding an Admin User**

The **admin user** has an additional privilege: they can assign other users as approvers on behalf of someone else.\
When the admin user performs this action, a user will then be able to view the invoices of another user.

To add an admin user, follow these steps:

1. In **Power Automate**, open the appropriate **Solution**.
2. Click on **Tables**.
3. Search for the table **AdminUser**.
4. Add the **email address** of the person who should be assigned as an admin.

<figure><img src="../.gitbook/assets/image (710).png" alt=""><figcaption></figcaption></figure>

### **Act on Behalf Of**

An **admin user** has access to an additional button in the app: **Settings**.\
In this screen, the admin can specify **on whose behalf** another user is allowed to perform approvals.

* Click on the desired **user**.
* A text field will appear at the **bottom right** of the screen.
* Enter the **email address** of the person on whose behalf approvals should be made.
* Click **Add** to confirm.

<figure><img src="../.gitbook/assets/image (711).png" alt=""><figcaption></figcaption></figure>

## **Troubleshooting**

If an invoice does not appear in the **Approval Dashboard**, or if an approved invoice is not correctly reflected in **Finance & Operations (F\&O)**, there may be an issue with one of the **Power Automate flows**.

In such cases, it is recommended to open the **Cloud Flows** listed below to identify the source of the problem.\
Here you can view all available flows connected to the app.\
Each flow has its own specific purpose and function.\
\
Below is an example of the screen that appears when you click **“Cloud Flows.”**\
If you then click on a flow, you can view the **run history** of that specific flow.

Below you can see the **history of the flow** that was executed to notify F\&O that an invoice has been approved.

* On the **left side**, you can see when the flow was run. Clicking on this entry allows you to view **detailed information** about what succeeded and what failed.
* On the **right side**, you can see which flows **ran successfully** and which **encountered errors**.

<figure><img src="../.gitbook/assets/image (713).png" alt=""><figcaption></figcaption></figure>

### **Maintaining Connection References in the Solution**

Connection references define which services your app and flows use. Keeping them up to date ensures that your **Dataverse, F\&O, email, and Office 365 integrations** continue to work correctly.

***

#### **1. Open the Solution**

1. Go to https://make.powerapps.com and sign in.
2. In the left-hand menu, select **Solutions**.
3. Open the **Solution** containing your app and flows.

***

#### **2. Locate Connection References**

1. Inside the Solution, click **Connection References** in the left-hand menu.
2. You will see all existing connections, such as:
   * **Dataverse** – for accessing tables and data.
   * **Finance & Operations (F\&O)** – for ERP integration.
   * **Mail (Office 365 Outlook)** – for sending approval notifications.
   * **Office 365 Users / Other Office services** – for user profiles or additional actions.

***

#### **3. Update or Reconnect a Connection**

1. Click on the **connection reference** you want to maintain.
2. If the connection is broken, expired, or requires a different user, click **Edit** or **Reconnect**.
3. Sign in with the appropriate credentials for that service.
4. Save your changes.

***

#### **4. Verify Connections in Flows and Apps**

1. Open each **flow** in the Solution.
2. Check that the connection references are correctly applied in all actions.
3. Do the same for the **Power App**, ensuring that all data sources point to the correct connection references.

***

#### **5. Best Practices**

* Use **service accounts** for connections that require shared access, rather than individual user accounts.
* Regularly review connection references to prevent failures due to expired credentials.
* Keep documentation of which account is used for each connection.
