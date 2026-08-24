# Q&A (Post to NAV/BC)

This article describes how troubleshoot [Post to NAV/BC](../daily-use/post-to-nav-bc.md).

If [Stamp Events](../all-tables/stamp-events.md) fails when [posting](../daily-use/post-to-nav-bc.md) try use the _Manual post (journal only)_ in the [Stamp Event](../all-tables/stamp-events.md) page.

Standard NAV/BC posting of Productions _can_ fail with the dialog _The operation has been finished. Do you want to post output for the finished operation?_, which can be solved in two different ways:

*   Post the line manual using the _Manual post (journal only)_ in the [Stamp Event](../all-tables/stamp-events.md) page.
*   Remove the dialog from code:
    *   For BC18 and newer set `IsHandled := TRUE` with `[EventSubscriber(ObjectType::Table, Database::"Item Journal Line", 'OnBeforeConfirmOutputOnFinishedOperation', '', false, false)]`
    *   For older FOB installations(NAV2013 to BC14)
    *   _Remote_/_Comment_ `CONFIRM` for this in the table `Item Ledger Journal`.

## See also

[Post to NAV/BC](../daily-use/post-to-nav-bc.md)
