# Entity Configuration

Entity Configuration is the mapping of **data from external systems** to tags. It is an essential part of integrating your 9A Raptor DWH tenant in an external system, such as Dynamics 365 Finance & Operations.

{% hint style="success" %}
A well-configured Entity Configuration is vital for any 9A Raptor DWH tenant. Incorrect configuration can lead to duplicate or corrupt tags, as well as significantly reduce the maintainability of the Taxonomy. It is therefore strongly advised to carefully read this documentation before getting started.&#x20;
{% endhint %}

### **Providing business context**

To start, the external system (e.g., Dynamics 365 F\&O) must send relevant business context to Raptor. This context is usually delivered in JSON format and includes information about the system, the selected table or entity, and a set of **key-value pairs** containing details about the record.

Take the example of a user selecting the vendor 'Expertbike' in D365 Finance & Operations. Selecting this record will trigger the external system to send the following info to 9A Raptor DWH:

```
{ 
   "source": "D365-FO",
   "type": "VENDVENDORV2ENTITY",
   "legalEntity": "USMF"
   "fields": {
      "VENDORACCOUNTNUMBER": "S0000008",
      "VENDORORGANIZATIONNAME": "Expertbike"
}
```

This business context will serve as the **input** of the Entity configuration. This input can be checked in 9A Raptor DWH by clicking your username on the top right and selecting 'Plugin'.

<figure><img src="../../.gitbook/assets/image (701).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (292).png" alt=""><figcaption></figcaption></figure>

#### Key aspects of Entity Configuration:

Once the external system is configured to provide the necessary business context to 9A Raptor DWH, an entity configuration can be set up to translate it into a tags.\
Making an entity configuration consists of the following key steps:

* Mapping records to **a unique tag code**
* Creating **labels** that users will see
* Defining **parent-child relations** to establish tag hierarchy
* Defining **link relations** to other tags

### Accessing the Entity Configuration

1. Go to the Configuration panel (see [.](./ "mention"))
2. On the left, choose 'Entity Configuration'

You'll see a list of all configured entities (tables), and the external systems they originate from.

<figure><img src="../../.gitbook/assets/image (703).png" alt=""><figcaption><p>This tenant has entity configurations for several entities in D365 Customer Engagement and D365 Finance &#x26; Operations. <br>("D365-CE', 'D365-FO')</p></figcaption></figure>



When selecting an Entity Configuration, you will be able to view the details. Entity Configurations are stored in JSON format, this format is visible using the JSON editor. See [#using-the-json-editor](entity-configuration.md#using-the-json-editor "mention") for more info.

<figure><img src="../../.gitbook/assets/image (279).png" alt=""><figcaption><p>Use the JSON editor toggle to view the configuration in JSON format</p></figcaption></figure>

***

### Creating an entity configuration

You can create a new entity configuration by clicking the '+' icon in the overview. Provide the source, name and - if applicable - legal entity to create the base for the configuration. \
\
Note that the legal entity is only required if this entity configuration should only apply for a specific legal entity. In most cases, this field can be left empty and will be dynamically filled up by the external system when passing the legal entity value in the business context.

<figure><img src="../../.gitbook/assets/image (280).png" alt=""><figcaption></figcaption></figure>

Taking the Vendor entity example from before, see [#providing-business-context](entity-configuration.md#providing-business-context "mention"):

* The source should match the input, so this would be 'D365-FO'
* The name of the entity is the logical name of the 'Vendors V2' entity in D365: VENDVENDORV2ENTITY
* The Legal Entity field can be left blank here, as the legal entity value is dynamically provided in the business context

<figure><img src="../../.gitbook/assets/image (281).png" alt=""><figcaption></figcaption></figure>

Hit 'Save' to create the entity configuration.

### Defining fields

In the "All fields" list, we provide the names of fields that we wish to use to build our tag. These fields must exactly match the field names used in the external system.

Make sure you have:

* A field representing the primary key of the entity, or a combination of fields that make up a primary key
* A field to show in the resulting tag's label - this is what the user will see
* (Optional) foreign key fields, that represent the primary key of other entities. These can be used to create relations to other entities.

By default, the entity configuration may also have a few **placeholder fields**. These fields will automatically inject a value when the entity configuration is used.

* `$LegalEntity`: injects the 'legalEntity' field value provided by the external system
* `$Provider`: injects 'providerCode' field&#x20;
* `$ExternalEntityName`: replaced with the value in the 'name' field

You can add fields by clicking on the “+” button.

You can also change the name of a field in case a mistake was made by double clicking on the field, which will open a small popup where you can edit the text.&#x20;

Changes are applied automatically in all places where the field is used, when clicking outside of the popup. However you must still explicitly **save the changes** with the save button at the bottom.

Let's take the example from [#providing-business-context](entity-configuration.md#providing-business-context "mention") and add them to the list:

<figure><img src="../../.gitbook/assets/image (282).png" alt=""><figcaption></figcaption></figure>

VENDORACCOUNTNUMBER is the vendor's unique number in Dynamics 365 and makes a perfect primary key field.&#x20;

VENDORORGANIZATIONNAME contains the vendor's name, this is the value we want to show to the user when they see the resulting tag.

### Defining the tag code

The tag code format in an entity configuration makes sure that every tag created for a certain entity has a unique, humanly readable 'code'. This code not only guarantees the uniqueness of a tag, but can also be used to easily find the tag back with the 9A Raptor DWH API.\
\
As the tag code's main responsibility is to guarantee the tag's uniqueness, it should always contain the primary key field, or a combination of fields that guarantee uniqueness.

**To create or edit the tag code format:**

1. Double-click the code, or click the edit button.
2. Use the drag-and-drop interface to place fields in the correct position, or type the code using `{{FIELD_NAME}}` to add fields manually (in case you know their names by heart).
3. Spaces between fields are automatically trimmed.

**Important Rules for Tag Codes:**

* Avoid spaces in tag codes
* Use consistent casing
* Be consistent with the casing of other entity configurations
* Use `\` to structure your format
* Do not end tag codes with a `\`

<figure><img src="../../.gitbook/assets/image (283).png" alt=""><figcaption><p>Using a combination of the $LegalEntity placeholder and the primary key field, we make a unique tag code format. The resulting tags will be only used for a specific legal entity.</p></figcaption></figure>

In the example above:

* We prefix our tag code format with 'D365-FO\Vendors' so that it is clear which entity it represents
* We use the placeholder field '$LegalEntity' to inject the legal entity (provided by the business context) into the the tag code
* Lastly, we use our primary key field 'VENDORACCOUNTNUMBER' to guarantee uniqueness

If the business context from our example would be used:

```
{ 
   "source": "D365-FO",
   "type": "VENDVENDORV2ENTITY",
   "legalEntity": "AM01"
   "fields": {
      "VENDORACCOUNTNUMBER": "S0000008",
      "VENDORORGANIZATIONNAME": "Expertbike"
}
```

A tag would be created with a tag code 'D365-FO\Vendors\AM01\S0000008'.

***

### Defining the tag label

Next to a unique tag code, a tag is also required to have a label. A label is the text that will be shown to Raptor users when they view or search a tag.

Defining a label formats works similarly to the code definition:

* You can use drag-and-drop, `{{FIELD_NAME}}`, or manually type the label format
* Spaces between fields are kept intact, but leading and trailing spaces are trimmed

In our example, we add the vendor's name, number, as well as the legal entity value to provide the users with an informative tag label.

<figure><img src="../../.gitbook/assets/image (285).png" alt=""><figcaption></figcaption></figure>

### Testing the entity configuration

Now that we've defined both a code and label format, we are able to save the entity configuration and perform a first test. We refer back to our original example and open 9A Raptor DWH on the vendor 'Expertbike'.

The following tag is created:

<figure><img src="../../.gitbook/assets/image (289).png" alt=""><figcaption></figcaption></figure>

In the 9A Raptor DWH configuration panel, we are also able to see the tag that was generated in the Taxonomy hierarchy. Here we can verify that the tag code and label format are createad as expected:

<figure><img src="../../.gitbook/assets/image (288).png" alt=""><figcaption></figcaption></figure>



### Defining relations

As described in [taxonomy.md](taxonomy.md "mention"), tags can have relations to other tags:

1. **Parent relation**: defining the tag's place in the tag hierarchy (taxonomy)
2. **Link relations**: defines other tags that are automatically added when the main tag is used

#### Parent Relations

* A tag can only have one parent. If multiple parent relations are defined, the system will use the first parent with non-empty fields.
* It is **always** recommended to create a parent relation for each entity configuration. This will ensure that tags are not added to the root of the tag hierarchy, but instead given a place under the correct parent tag.

<figure><img src="../../.gitbook/assets/image (293).png" alt=""><figcaption><p>By defining a parent relation, we can ensure that vendor tags created through entity configuration are added under 'Vendors', and not in the root of the Taxonomy</p></figcaption></figure>

### Creating a parent relation

To create a parent relation, you can click the '+' icon next to 'Parents'. This will open a wizard giving you multiple options:

<figure><img src="../../.gitbook/assets/image (294).png" alt=""><figcaption></figcaption></figure>

* **Generate a default parent hierarchy**

This option will auto generate a parent relation for you, based on the already specified tag code format. Be sure to double check if the resulting relation is valid.

* **Pick an existing tag**

If the parent tag for this entity already exists or was manually created, this option will allow you to locate this parent with the tag picker.

* **Link another entity**

Allows you to use an existing entity configuration to build the format of the parent tag relation.

An example could be the 'Projects' entity. A project tag can have another project tag as a parent (the parent project). In this case, you would select the PROJECTENTITY entity configuration, and use the 'PARENTPROJECT' field to dynamically create a parent relation:

<figure><img src="../../.gitbook/assets/image (296).png" alt=""><figcaption><p>Creating a parent relation to the same entity</p></figcaption></figure>



The resulting parent relation:

<figure><img src="../../.gitbook/assets/image (297).png" alt=""><figcaption></figcaption></figure>

In the example above, we added an additional parent relation that refers to the static 'Projects' tag (with code D365-FO\Projects).

* If the PARENTPROJECT is filled in, a tag will be created for the parent project and set as the parent of the current tag.
* If the PARENTPROJECT is empty, 9A Raptor DWH will fallback to the static parent tag 'Projects'.

This parent tag relation setup ensures that project tags are either created under 'Projects' or under their respective parent project tag in the taxonomy:

<figure><img src="../../.gitbook/assets/image (298).png" alt=""><figcaption><p>Two project tags created by the same entity configuration. Their parent tag is dynamically chosen based on the value of the PARENTPROJECT field.</p></figcaption></figure>

* **Custom**

Using the Custom method, you can manually define the code and label format of the parent relation. Parent relations do not necessarily need fields in their code formats, as they are usually static tags.

<figure><img src="../../.gitbook/assets/image (299).png" alt=""><figcaption></figcaption></figure>

### Creating a link relation

A tag can have 'related tags': tags that are automatically added when the main tag is put on a document. Related tags are usually the result of link relations in the entity configuration.

Defining link relations is not required, but can be very useful. The resulting 'related tags' can give more context to the document and make them more easily searchable.

A link relation can be added by clicking the '+' icon next to 'Links':

<figure><img src="../../.gitbook/assets/image (300).png" alt=""><figcaption></figcaption></figure>

This will open the same wizard as seen in [#creating-a-parent-relation](entity-configuration.md#creating-a-parent-relation "mention").&#x20;

<figure><img src="../../.gitbook/assets/image (302).png" alt=""><figcaption></figcaption></figure>

The options to create a Link relation are:

* **Pick an existing tag**

As mentioned in [#creating-a-parent-relation](entity-configuration.md#creating-a-parent-relation "mention"), this option allows you to make a relation to a specific tag, meaning that this particular tag will be added as a related tag every time.

* **Link another entity**

This is the most commonly used option for link relations.

When linking from one entity to another (e.g., linking a project to a customer, or an invoice to a purchase order), the system can help automate this process. Just as with parent relations, you can use an existing entity configuration and copy it over as a link relation. This requires you to map the fields from your main entity to the one that you're linking too, which requires a **foreign key field**.

As an example, we will make a link relation from the Project entity to the Customer entity. The goal is that every time a project tag is added on to a document, the related customer is also automatically added as a related tag.\
\
This link relation can be created by using the foreign key field 'CUSTOMERACCOUNT' on the Projects entity, referring to the customer entity's primary key.

<figure><img src="../../.gitbook/assets/image (303).png" alt=""><figcaption></figcaption></figure>

As a result, a link relation is made to the Customers entity. Not only the tag code format is copied from the customer Entity Configuration, but also it's parent relation:

<figure><img src="../../.gitbook/assets/image (307).png" alt=""><figcaption></figcaption></figure>



An entity may not have all necessary fields to complete the mapping. In that case, you can add a temporary value and remove it after completing the wizard.

Note that this can only be done for the fields that are used in the referenced entity's label. Fields used in the tag code should always be fully mapped for the link relation to work.\
\
In the example above, no field is available to match the 'ORGANIZATIONNAME' of the Customers entity, which is used for the Customer entity's tag label. \
In this case the value of the tag label can be left empty. <br>

{% hint style="info" %}
Not providing the fields that the linked entity uses for it's label may result in the related tag being created as a 'Dummy' tag. A dummy tag is a tag which was created through a link relation, but which does not contain a label yet, only a tag code.
{% endhint %}

Not providing the fields that the linked entity uses for it's label may result in the related tag being created as a 'Dummy' tag. A dummy tag is a tag which was created through a link relation, but which does not contain a label yet, only a tag code.

<figure><img src="../../.gitbook/assets/image (305).png" alt=""><figcaption><p>Example of a Dummy tag created through a link relation. If a link relation can only provide the related tag's code but not the tag's label, and that tag does not exist yet, a Dummy tag will be created when that entity configuration is used. The dummy tag will be automatically updated when it receives a tag label.</p></figcaption></figure>

* Custom

As with parent relations, you are also able to generate the link relation by manually defining the related tag's code and label format.

#### Assigning parent relations to link relations

It is recommended to provide each link relation with a respective parent relation. In case a link relation results in a Dummy tag, the tag will be placed in the taxonomy root by default.\
To prevent this, you can define a parent relation to ensure that even in case of a Dummy tag, the tag gets it's correct spot in the tag hierarchy.

<figure><img src="../../.gitbook/assets/image (306).png" alt=""><figcaption><p>This entity configuration contains a link relation to the Customers entity. This link relation has it's own parent relation to the static 'Customers' tag to ensure that - even in case of a Dummy tag - the resulting customers tags will always be added beneath the static Customers tag.</p></figcaption></figure>

### Using the JSON Editor

With the JSON editor, you can:

* **View and edit the JSON** directly for faster changes.
* **Copy and paste configurations** between different environments (e.g., from UAT to PROD).
* **Compare old and new configurations** to ensure no unintended changes.

The system will **not save invalid JSON** or changes that affect the target entity (like source, entity name, or legal entity).

Below is an example of the JSON format used to define an entity configuration:

```json
[
  {
    "name": "PROJECTENTITY",
    "source": "D365-FO",
    "legalEntity": null,
    "providerCode": "D365-FO",
    "codeFields": ["$LegalEntity", "PROJECTID"],
    "codeFormat": "D365-FO\\Projects\\{0}\\{1}",
    "nameFields": ["PROJECTID", "PROJECTNAME"],
    "nameFormat": "[{0}] {1}",
    "relations": [
      {
        "codeFields": ["$LegalEntity", "CUSTOMERACCOUNT"],
        "codeFormat": "D365-FO\\Customers\\{0}\\{1}"
      },
      {
        "codeFields": ["$LegalEntity"],
        "codeFormat": "D365-FO\\Legal-Entities\\{0}"
      },
      {
        "isParentTag": true,
        "codeFields": ["$LegalEntity"],
        "codeFormat": "D365-FO\\Projects\\{0}",
        "nameFields": ["$LegalEntity"],
        "nameFormat": "{0}",
        "relations": {
          "isParentTag": true,
          "codeFields": [],
          "codeFormat": "D365-FO\\Projects",
          "nameFields": [],
          "nameFormat": "Projects"
        }
      }
    ]
  }
]
```

#### Structure of an Entity Configuration

* **name**: name of the entity or table (required)
* **source**: the external system providing the business context (required)
* **legalEntity**: specifies a particular legal entity if needed (optional)
* **providerCode:** specifies the code of the tag provider (optional)
* **codeFields**: list of fields required to create the tag’s unique code (required)
* **codeFormat**: string format to combine fields into a tag code (required)
* **nameFields**: fields used to create the tag’s label (required)
* **nameFormat**: string format to define the tag’s label (required)
* **relations**: defines parent and related tags (optional)
* **isParentTag**: indicates if the relation is a parent relation (optional)

***

### Copying Entity Configurations

To copy configurations across tenants:

1.  Click the “copy” icon to copy all selected configurations

    <div align="left"><figure><img src="../../.gitbook/assets/image (308).png" alt=""><figcaption></figcaption></figure></div>
2. On the target tenant, click the "+" icon and use the **Bulk Import** option to paste the JSON

<figure><img src="../../.gitbook/assets/image (309).png" alt=""><figcaption></figcaption></figure>

3. Verify that no errors are shown (errors appear in red).

{% hint style="info" %}
* Check the JSON carefully before pasting it into a new tenant
* To copy all entities, select them using the checkbox at the top left corner
* For partial copies, select the entities you need using Shift+Click
{% endhint %}

***

