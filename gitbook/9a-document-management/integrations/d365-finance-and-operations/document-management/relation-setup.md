# Relation setup

The relation setup give the end-users possibility to see the documents of a specific entity/tag from a form where the selected record is not used as entity/tag. This can be achieved with relation setup. This form can be found via 9A Raptor DWH > Setup > Document management > Relation setup.

The **Relation Setup** feature allows end-users to view documents associated with a specific tag, even when the selected record is not directly used as a tag. This capability is enabled through relation configurations.

To access the Relation Setup:\
Navigate to **9A Raptor DWH > Setup > Document Management > Relation Setup**.

#### Example Scenario

Suppose you want to view all documents related to an imported invoice from a ledger journal. Although ledger journals are not used as tags, there is a relationship between the imported invoice and the ledger journals. To achieve this, you can define a relation between the `DocNo` field in the `EXAPurchInvoiceImported` table and the `EXADocNo` field in the `LedgerJournalTable`.

#### Supported Relation Types

We support two types of relations:

1.  **Direct Relation**\
    A direct link exists between the selected record and the associated entity. In this case, the DocNo field.

    * **Example:** \
      Entity: `EXAPurchInvoiceImportedEntity`\
      Field: `DocNo`\
      Table: `LedgerJournalTable`\
      Field: `EXADocNo`

    <figure><img src="../../../.gitbook/assets/image (127).png" alt=""><figcaption></figcaption></figure>

    Result: when opening Raptor on the ledger journal, the Document Warehouse will open filtered on the associated 'EXAPurchInvoiceImported' tag, instead of the ledger journal entry itself.
2.  **Indirect Relation**\
    An indirect link exists between the selected record and the associated entity. Indirect relations require a **direct relation** as a base (finish-relation). Therefore, you must configure direct relations before creating indirect ones.

    Additionally, indirect relations can connect tables through different fields or table names.

    * **Example:**

    &#x20;      Entity: `EXAPurchInvoiceImportedEntity`\
    &#x20;      Field: `DocNo`\
    &#x20;      Table: `LedgerJournalTrans`\
    &#x20;      Field: `JournalNum` (via the direct relation mentioned above).

<figure><img src="../../../.gitbook/assets/image (128).png" alt=""><figcaption></figcaption></figure>

Result: when opening Raptor on the ledger journal lines, the Document Warehouse will open filtered on the associated 'EXAPurchInvoiceImported' tag, instead of the selected line itself. This is accomplished by linking the line level to the imported invoice through the ledger journal header, an indirect link.

These are a few handy relations to set up for entity EXAPurchInvoiceImported. These will make invoices from the All Invoices screen in Raptor Input Management available in multiple places:

<table data-header-hidden data-full-width="false"><thead><tr><th valign="bottom"></th><th width="99" valign="bottom"></th><th width="216" valign="bottom"></th><th width="235" valign="bottom"></th><th valign="bottom"></th><th width="198" valign="bottom"></th></tr></thead><tbody><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">AccountingDistribution</td><td valign="bottom">SourceDocumentHeader</td><td valign="bottom">VendInvoiceInfoTable</td><td valign="bottom">SourceDocumentHeader</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">LedgerJournalTrans</td><td valign="bottom">journalnum</td><td valign="bottom">LedgerJournalTable</td><td valign="bottom">journalnum</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">LedgerJournalTrans</td><td valign="bottom">vendtransid</td><td valign="bottom">vendtrans</td><td valign="bottom">recid</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">ProjCostTrans</td><td valign="bottom">VoucherJournal</td><td valign="bottom">Vendtrans</td><td valign="bottom">Voucher</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">ProjPostTransView</td><td valign="bottom">TransId</td><td valign="bottom">ProjCostTrans</td><td valign="bottom">TransId</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">SpecTrans</td><td valign="bottom">RefRecId</td><td valign="bottom">VendTransOpen</td><td valign="bottom">RecId</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">VendInvoiceInfoLine</td><td valign="bottom">parmid</td><td valign="bottom">vendinvoiceinfotable</td><td valign="bottom">parmid</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">vendpackingsliptrans</td><td valign="bottom">inventtransid</td><td valign="bottom">VendInvoiceInfoLine</td><td valign="bottom">inventtransid</td></tr><tr><td valign="bottom">Indirect</td><td valign="bottom"></td><td valign="bottom">VendTransOpen</td><td valign="bottom">RefRecId</td><td valign="bottom">Vendtrans</td><td valign="bottom">RecId</td></tr><tr><td valign="bottom">Direct</td><td valign="bottom">DocNo</td><td valign="bottom">LedgerJournalTable</td><td valign="bottom">EXADocNo</td><td valign="bottom"></td><td valign="bottom"></td></tr><tr><td valign="bottom">Direct</td><td valign="bottom">DocNo</td><td valign="bottom">VendInvoiceInfoTable</td><td valign="bottom">EXADocNo</td><td valign="bottom"></td><td valign="bottom"></td></tr><tr><td valign="bottom">Direct</td><td valign="bottom">DocNo</td><td valign="bottom">VendInvoiceJour</td><td valign="bottom">EXADocNo</td><td valign="bottom"></td><td valign="bottom"></td></tr><tr><td valign="bottom">Direct</td><td valign="bottom">DocNo</td><td valign="bottom">VendTrans</td><td valign="bottom">EXADocNo</td><td valign="bottom"></td><td valign="bottom"></td></tr></tbody></table>
