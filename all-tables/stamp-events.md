# Stamp Events

This table contains all the _actions_ which registrations in [Stamp Journal Line](./stamp-journal-lines-2.md) has resulted in.

Every time a new registration is made, or reporting qty/status, there will be added a line in this table.

Item consumption, which are linked to a [Stamp Journal Line](./stamp-journal-lines-2.md) will also add a line in this table (and later be posted).

Time consumption will also add a line in this table (and later be posted). Howefter, only when the registrations are [Approved](../all-pages/time-calculation-and-approval.md). This function must be activated under [setup](../general-setup/jobmanager-setup.md).

It is possible to [setup rounding](../general-setup/jobmanager-setup.md) for the Time consumption.

The hourly rate _can_ be overridden per Employee when setting up [Pay Type for posting](../general-setup/posting-rate.md).

Posting time consumption to **Production** can be limited with [Post time (Flusing Method=Forward)](../general-setup/post-time-flushing-method-forward.md) and [Post time (Flusing Method=Backward)](../general-setup/post-time-flushing-method-backward.md).

When posting time consumption to **Job** or **Service**, the resource associated with the NAV/BC _Employee_ is used.

If the field _Usage Link_ is used on _Job Planning Lines_, the resource from the Job Planning Line is used instead. The hourly rate _can_ still be overridden per Employee when setting up [Pay Type for posting](../general-setup/posting-rate.md).

Lines in this table may later be posted in the relevant NAV/BC modules - according to this [this field](./event.md).

Lines are [posted menually](../all-pages/stamp-events.md) or [automatically with Job Queue](../daily-use/post-to-nav-bc.md).

[Sequence](./sequence-10.md)  
[Journal Reference](./journal-reference-2.md)  
[Timestamp](./timestamp.md)  
[Event](./event.md)  
[Status](./status.md)  
[Registration Source](./registration-source-2.md)  
[Employee](./employee-9.md)  
[Job Id](./job-id-7.md)  
[Job Type](./job-type-3.md)  
[Stamp Type](./stamp-type-3.md)  
[Work Type](./work-type-4.md)  
[Ref. Type](./ref-type-3.md)  
[Ref. Number](./ref-number-2.md)  
[Sub. Ref. Number](./sub-ref-number-2.md)  
[Profile date](./profile-date-5.md)  
[Posting Counter](./posting-counter.md)  
[Error timestamp](./error-timestamp.md)  
[Posted method](./posted-method.md)  
[Posted by](./posted-by.md)  
[Posted timestamp](./posted-timestamp.md)  
[Posted Document No.](./posted-document-no-2.md)  
[Cancel Document No.](./cancel-document-no.md)  
[Stop-code](./stop-code.md)  
[Good Qty](./good-qty-2.md)  
[Scrap Qty](./scrap-qty-2.md)  
[Actual Time Comsump](./actual-time-comsump.md)  
[Scrap Code](./scrap-code.md)  
[Serial No. (output)](./serial-no-output.md)  
[Lot No. (output)](./lot-no-output.md)  
[Location Code (output)](./location-code-output.md)  
[Bin Code (output)](./bin-code-output.md)  
[Item No. (consumption)](./item-no-consumption.md)  
[Consump now](./consump-now.md)  
[Reason Code](./reason-code.md)  
[Back](./back.md)  
[Expected Quantity](./expected-quantity.md)  
[Consumped Qty](./consumped-qty.md)  
[Variant Code (consumption)](./variant-code-consumption.md)  
[Serial No. (consumption)](./serial-no-consumption.md)  
[Lot No. (consumption)](./lot-no-consumption.md)  
[Location Code (consumption)](./location-code-consumption.md)  
[Bin Code (consumption)](./bin-code-consumption.md)  

## See also

[Stamp Events](../all-pages/stamp-events.md)  
[Post to NAV/BC](../daily-use/post-to-nav-bc.md)
