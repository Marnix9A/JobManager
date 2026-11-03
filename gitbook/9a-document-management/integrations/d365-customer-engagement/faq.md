# FAQ

A FAQ for the Raptor Document Warehouse integrated with Microsoft Dynamics 365 Customer Engagement, including explanations and screenshots that address the most common issues and questions.

<details>

<summary>Raptor is not available on an entity. What should I do?</summary>

This means the entity was not yet enabled in the Raptor Configuration app.\
**Solution:** Add the entity in the Entity Configurations screen in the Raptor Configuration app. See [entity-configurations.md](entity-configurations.md "mention")

</details>

<details>

<summary>A user gets an error when opening Raptor inside CE. How do I fix this?</summary>

The user was not added to Raptor or does not have the external system assigned.\
**Solution:** Make sure the user was created in Raptor and has the **external system** assigned.

</details>

<details>

<summary>Raptor is available on the entity, but all documents are shown and no context filter appears. Why?</summary>

This means the entity has not been configured in the Entity Configuration. Without it, no tags can be created for it.\
**Solution:** Add the entity to the **Raptor Entity Configuration**.

</details>

<details>

<summary>When dragging a document into the Raptor context, the template is not available. How do I fix this?</summary>

**Solution**: Make sure the template was created in the Raptor Configuration screen. Add a contextual tag for your data entity to ensure it's visible in the right context.

</details>
