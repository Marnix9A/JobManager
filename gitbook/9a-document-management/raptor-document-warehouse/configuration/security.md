# Security

## The Basics

By default users can do _**nothing**_!

If they can do something, it is because they have been granted permission to do that.

Exceptions to the rule are:

* Reading your own user details\
  Meaning: a logged in user can see his name, email, tenants, ...
* Access all security roles\
  Roles define which permissions are granted to users in that role. This in itself is considered 'public' knowledge.

<details>

<summary><strong>Work in progress</strong></summary>

Not all actions in a 9A Raptor DWH tenant are protected by permissions yet, making them available to every user. Examples are viewing tags, templates and fields.

</details>

Permissions are defined in a **role**, and **roles** are assigned to users.\
A user can be assigned multiple roles.\
A role consists of rules (= permissions).\
Assigning a role can never take away permissions from a user.<mark style="color:red;">**\***</mark>

<details>

<summary><mark style="color:red;">*</mark>Exception: the UI Read-only rule</summary>

Normally adding extra roles only can add extra permissions, with one exception:\
A role that has the **UI Read-only** rule will prevent the users from modifying documents in the UI.

As the name suggests, this rule only prevents document modification in the 9A Raptor DWH user interface. The users **will still be able to make modifications by using the 9A Raptor DWH API**.

The rule is only available through a feature flag and is kept for backwards compatibility. For Raptor tenants containing this feature flag, we discourage further use of the rule and refer to the newly available security rules to provide both front- and backend security.



</details>

{% hint style="warning" %}
Configuring security in a system requires time and effort. Every customer is different and has to consider what is important and where the balance is between security, usability and maintainability.

Configuring security rules requires technical knowledge about it's internal workings. Do not hesitate to ask a 9A Raptor DWH consultant for guidance on this topic.
{% endhint %}

## Definitions and naming

### Role

Roles are the main container used to assign permissions to users. A single role can have multiple permissions known as "rules". It is the role that is eventually assigned to the users.

### Rule

A Rule is the combination of 3 parts

* A **key** \
  _&#x69;.e. "meta.document.rec"_
* A **grant** \
  _&#x69;.e. "read"_
* A **condition** _\[optional]_ \
  _&#x6C;imiting the set of records for which the rule applies_

#### Key

Every rule has a key, and the goal is to eventually have one key for each possible action.\
\
For instance, there is a key for "adding a tag to a document", a key for "removing a tag from a document", and a key to "see a document". Some actions do not (yet) have a specific key assigned to them. In that case the server will take the nearest key when checking if the action is allowed (see [inheritance](security.md#inheritence)).

#### Condition

Conditions are limitations to the permissions granted.

An example: users should be allowed to see some documents in the document warehouse, but not all documents. To do this, we can set a query filter on the 'View documents' rule to makes this access conditional.

#### Grant: read / write / execute

Permissions can be one of the following "Grant" types:

* **Read**\
  Read access means a user is allowed to see a certain resource, such as documents, tags, fields, etc.\
  It is not possible to grant a "partial" read to a record, meaning that you can't allow a user to see the name and the tags of a document, but not the fields. It's all or nothing!<br>
* **Write**\
  Write access means that a user is allowed to create, modify and delete records. So if a user is granted write access on a document, he or she can upload a document, assign tags and fields to it and delete the document again.<br>
* **Execute**\
  With execute you allow users to "execute" an action, like allowing a user to assign a template to a document. This can be considered a "partial write" to a record.

### Inheritance

Inheritance is a concept that applies to keys. And it creates a "parent-child" like relation to keys. Adding a rule on a higher level key makes it so that all child keys are automatically applied.

The user interface has a tree like structure that attempts to show the inheritance structure of the keys. However, keys do not have a single parent, and can actually be a child (/ subset) of multiple parent keys.

<figure><img src="../../.gitbook/assets/image (632).png" alt=""><figcaption><p>Rules are presented in a hierachical manner</p></figcaption></figure>

A few examples of how inheritance works:

<details>

<summary>Example "view document"</summary>

To view a document, the application will check if the user has read access to the key:\
_**meta.document.rec**_.

This key is a subset of _**meta.document.\***_\
Which in turn is a subset of _**meta.\***_\
Which in turn is a subset of _**\***_\
\
This means that granting read access to _**meta.\***_ will allow users to view the documents.

</details>

<details>

<summary>Example "admin role"</summary>

See [#the-administrator-role](security.md#the-administrator-role "mention")

</details>

Inheritance can be used to reduce the amount of work to configure a role, but are bound to some limitations:

* **Conditions cannot be set on "higher level" keys**, meaning they, by definition, allow everything.\
  This is because higher level keys can impact different resources, which is why no generic condition that can be applied.
* **It is not possible to exclude sub keys** from a higher level key. If a higher level key would grant access to 50 sub keys, and you only want to allow 49 of them, you cannot use the higher level key.
* **New features will include new keys**. If access was granted on one of the higher level keys it is not possible to prevent users to use the new feature after it was released, as their assigned roles immediately inherit the related sub keys.

## Configuring rule conditions

To view or modify a condition, find the rule in the table or tree view, and click on the pencil icon. Note that not all rules allow to set conditions.

<figure><img src="../../.gitbook/assets/image (626).png" alt=""><figcaption><p>active permisions in role, condition applies to visible documents</p></figcaption></figure>

When the pencil is clicked the condition is shown:

<figure><img src="../../.gitbook/assets/image (633).png" alt=""><figcaption><p>Visualized condition after clicking the pencil button</p></figcaption></figure>

## Reusing conditions

Conditions can be created to define a reusable filter that can be applied in roles and rules. The full list of these conditions can be found in the "Conditions" tab in the Configuration page. Each condition has a unique code, a resource type (i.e. "document"), a name, and the actual filter. The conditions can be nested, although loops are not allowed.

{% hint style="danger" %}
You can not delete a condition if it is used by another condition, or used in a role.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (458).png" alt=""><figcaption><p>example of reusable conditions</p></figcaption></figure>

Once a named condition is created, you can add them in a security Rule. To do so, pick the condition from the drop down, and then select "contains" if you want to match all records that match the condition, or "does not contain" if you want to exclude those records instead.

<figure><img src="../../.gitbook/assets/image (615).png" alt=""><figcaption><p>Reusing the 'Recent &#x26; complete' condition as a filter</p></figcaption></figure>

## The Default role

One (and only one) role can be marked as the “default role” this role is automatically assigned to users who are created in the systems. This allows administrators to provide a basic set of access right for new users.



<figure><img src="../../.gitbook/assets/image (634).png" alt=""><figcaption><p>The role marked as the default role for new users</p></figcaption></figure>

## The Administrator role

In the user interface, there is a checkbox on the roles editor that allows you to convert a role to an administrator role. When checked, the effect will be that 3 rules are added to the role:

* read on key \* without condition
* write on key \* without condition
* execute on key \* without condition

An administrator role has unlimited access to the tenant's resources and should therefore be reserved for specific users.

Deselecting the Administrator rights checkbox will remove all permissions from that role, so use with care.

<figure><img src="../../.gitbook/assets/image (635).png" alt=""><figcaption></figcaption></figure>



## Creating a new Role

To create a new role click the “+” button at the top of the role table.\
Next give the role a Name in the details section, and click the save button.\
This should create an empty role, which now can be modified.

{% hint style="info" %}
When you create a new role, it should automatically be selected, and show up at the top of the table. Once you refresh the list of roles it will be displayed in alphabetical order.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (616).png" alt=""><figcaption></figcaption></figure>

## How to edit/modify a Role

1. Open the configuration
2. Select the “Roles” tab.
3. Select the created role.
4. Make your changes.
5. Save your changes (!)

The permissions granted by a role can be visualized in two ways:

### Table view

The table view is the most basic visualization of the two, and only shows the actual rules / permissions of the role. You can see the actual key, and edit the condition if possible by clicking on the pencil icon.

<figure><img src="../../.gitbook/assets/image (617).png" alt=""><figcaption></figcaption></figure>

### Tree view

The tree view visualization can be used to more easily see all the possible options, and gives the possibility to just click on certain permissions in order to add them to the role. You can switch to show only "active" nodes, and all nodes with the toggle button at the top right of the tree view.

Note that this view is a combination of a "read" and "write" (/execute) tree mixed into a single view. We believe that this is the most informative way to display the options in a still rather condensed manner.

Note that not all the options are visualized in this tree. Some rules are "hidden" and will only be shown in the UI if they are active on the role, such as the UI Read-only rule and the Administrator rights.

<figure><img src="../../.gitbook/assets/image (618).png" alt=""><figcaption></figcaption></figure>

