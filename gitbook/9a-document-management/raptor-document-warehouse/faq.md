# FAQ

A FAQ for Raptor Document Warehouse with clear explanations and screenshots, answering the most common questions about access, roles, templates, taxonomy, and configuration.

### Access & authentication

<details>

<summary>I see an error when opening <code>raptor.9altitudes.com</code>. What does it mean?</summary>

This means you do not have access to **any** Raptor tenant.

</details>

<details>

<summary>I get an error saying I don’t have enough permissions. What should I do?</summary>

Your assigned role doesn't provide sufficient rights for this environment.\
**Solution:** Assign or create a role with the required permissions.

</details>

<details>

<summary>I cannot see the configuration screen. Why?</summary>

Your role doesn’t allow access to the configuration panel.\
**Solution:** Assign a role with configuration permissions.

</details>

<details>

<summary>I still get an access error even though I am added to Raptor with the correct rights. Why?</summary>

Check for a **typo in the user's email address,** this is a common cause.

</details>

<details>

<summary>I cannot change the field type. Is this normal?</summary>

Yes. Once a field is saved, the field type cannot be changed.

</details>

### Metadata ,Tags & Taxonomy&#x20;

<details>

<summary>I added a field but it isn’t used anywhere. How do I delete it?</summary>

You can only delete fields via **the Raptor API**, following the [**developer documentation**](../developers/api-starting-guide.md#id-1.-introduction)&#x20;

</details>

<details>

<summary>I added a document type in the Taxonomy, but it does not appear when i search for it. Why?</summary>

New taxonomy tags take a moment to become available.\
**Solution:** Wait a little it will show up shortly.

</details>

<details>

<summary>My template was created incorrectly and is not applied anywhere. How do I delete it?</summary>

Templates cannot be deleted via the UI.\
**Solution:** Delete it via [**Swagger**](../developers/api-starting-guide.md#id-1.-introduction), using the template ID.&#x20;

</details>

<details>

<summary>Tags are not correctly organized in the taxonomy tree. What should I do?</summary>

**Solutions:**

* Ensure the entity config is correct before adding parent tags
* Press the **Refresh** button so the service recalculates the correct parent
* Manually assign the correct parent tag

</details>

### External system

<details>

<summary>The external system is missing in the User screen. Why?</summary>

It is likely not set to **public**.\
**Solution:** Mark the external system as **public**.

</details>

