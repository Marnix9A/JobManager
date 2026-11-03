# Print destinations

* **9A Archive**: Archives documents in the Document Warehouse. This print destination is available only for non-proforma documents. To enable tag linking, the primary table name must be configured in the report setup.
* **9A Screen**: Displays documents on the user’s portable device. The file extension determines the application used to open the document (for example, Microsoft Excel for `.xls` files or a PDF viewer for `.pdf` files).
* **9A Printer**: Supports PDF documents only when the Document Routing Agent is running in interactive mode. When Dox42 is configured as the provider, EMF images can also be generated.
* **9A Email**: Sends emails either immediately or as batch jobs when tracking is enabled.
* **9A Email Interactive**: Sends interactive emails that can be reviewed and edited before sending. When used with BCC Integration, the email provider must be set to `EML_Raptor` in **Email parameters** (`System administration > Setup > Email > Email parameters`).

<figure><img src="../../../.gitbook/assets/image (721).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you're using 9A Email Interactive, but the mail is still nog generated as an EML message, be sure to check the user preferences: User options > Account > Email provider ID.
{% endhint %}
