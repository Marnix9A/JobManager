# FAQ

A FAQ for the Raptor Document Warehouse integrated with Microsoft Dynamics 365 Finance & Operations, including explanations and screenshots that address the most common issues and questions.



<details>

<summary>The Raptor 'dino' icon is not available on the page. What should I do?</summary>

Please check if

1. The relevant data entity was added in Data Management on the Raptor export project. This project is typically called 'RAPTOR\_CONTEXT' and should have the toggle 'Used for 9A Raptor DWH' enabled. Note that this toggle should be enabled at creation time of the export project.<br>
2. You have sufficient permissions. See [#viewing-the-raptor-dinosaur-button](security-and-permissions.md#viewing-the-raptor-dinosaur-button "mention")\
   \
   This means the entity is not yet included in the Raptor data management project.\
   Make sure to add it to an export project where 'Used for 9A Raptor DWH' was enabled **at creation time of the project**.<br>

</details>

<details>

<summary>A user gets an error when opening Raptor inside Finance &#x26; Operations. How do I fix this?</summary>

The user was not added to Raptor or does not have the external system assigned.

See [users.md](../../raptor-document-warehouse/configuration/users.md "mention") and [external-systems.md](../../raptor-document-warehouse/configuration/external-systems.md "mention")

</details>

<details>

<summary>Raptor is available on the page, but all documents are shown and no context filter appears. Why?</summary>

This means the entity has not been configured in the Entity Configuration. Without it, no tags can be created for it.\
\
**Solution:** Add the entity to the [entity-configuration.md](../../raptor-document-warehouse/configuration/entity-configuration.md "mention")

</details>

<details>

<summary>When dragging and document into Raptor, I don't see the template that I need. How do I fix this?</summary>

**Solution**: Make sure the template was created in the Raptor Configuration screen. Add a contextual tag for your data entity to ensure it's visible in the right context.

</details>

<details>

<summary>I get the error 'Output management: The operation has timed out' when generating documents.</summary>

The document creation service (Smartflows, Dox42, ...) is taking too long to generate the document, causing a timeout error.

**Solution:**&#x20;

1. Check if the document creation service is running into any errors
2. If there are no errors, try configuring a higher timeout setting in [#timeout](9a-raptor-dwh-parameters/general.md#timeout "mention")

</details>
