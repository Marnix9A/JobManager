# Invoice totals matching

Starting from the 10.2022.3.1 release, you can filter imported invoices based on the matching of totals. Two new menu items have been introduced to facilitate this:

<figure><img src="../../../.gitbook/assets/image (100).png" alt=""><figcaption></figcaption></figure>

1. **All unmatched totals invoices:**\
   Displays all imported invoices with the status "Imported" where the totals are not matched.
2. **All matched totals but unposted Invoices:**\
   Displays all imported invoices with the status "Imported" where the totals are matched but the invoices remain unposted.

The **TotalsAreMatched** field from the `EXAPurchInvoiceImported` table indicates whether the totals are matched. Please note that this field must never be used for other purposes, such as validation or posting. It is populated exclusively through the batch job **Match Imported Invoice Totals** found under **9A Raptor DWH > Periodic Tasks > Input Management**. This batch job can be scheduled according to customer priorities—for example, once or three times per day should generally suffice.

For backward compatibility, the **TotalsAreMatched** field of older, existing imported invoices can also be updated. This requires modifying the query used by the batch job to remove the invoice status filter. After running the batch job, you can reset and, if needed, extend the query.
