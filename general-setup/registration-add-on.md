# Registration add-on

Registration add-on is additional usage/costs, to be registred in [Stamp Journal add-on](../all-tables/stamp-journal-add-on.md).

**Posting to Job and Service**

The lines _can_ be [posted](../daily-use/post-to-nav-bc.md) to Job and Service.. This happens _if_ the field _Resource No_ **or** _Work Type_ is filled in.

*   If _Resource No_ is filled in, this is used. Otherwise, the resource is used from the [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md).
*   If _Work Type_ is filled in, this is used. Otherwise, the Work Type is taken from the resource.

**Timecounter to Agreement Setup**

An extra line _can_ be formed [Calculated lines](../all-tables/calculated-lines.md). This extra line _can_ be used in the [Agreement Setup](../all-tables/agreement-setup.md). This happens _if_ [Timecounter](../jobmanager-calculations/time-counters.md) is filled in.

**Transfer to Pay Transactions**

The lines _can_ be transferred to [Pay Events](../all-tables/pay-events.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md). This happens _if_ the field _Pay Type_ is filled in.

Pay Events _can_ later be transferred to Job. In which case:

*   If _Resource No_ is filled in, this is used. Otherwise, the resource is used from the [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md).
*   When transferred. it uses the _Work Type_ from the [Pay Type](../payroll-setup/pay-type.md).

**Remark: Qty to be posted/transferred can be:**

*   Given a [mandatory value](./qty-type.md)
*   Corrected with [rounding](./rounding-precision.md)
*   Corrected by [minimum/maximum](./minimum.md)

[Code](./code.md)  
[Description](./description-6.md)  
[Qty Type](./qty-type.md)  
[Rounding Precision](./rounding-precision.md)  
[Round type](./round-type.md)  
[Minimum](./minimum.md)  
[Maximum](./maximum.md)  
[Resource No.](./resource-no-2.md)  
[Resource Group](./resource-group.md)  
[Unit of Measure](./unit-of-measure.md)  
[Rate Type](./rate-type-2.md)  
[Pay Type](./pay-type.md)  
[Factor (Pay Type)](./factor-pay-type.md)  
[Time Counter](./time-counter.md)  
[Factor (Time Counter)](./factor-time-counter.md)  
[Start Trigger](./start-trigger.md)  
[Stop Trigger](./stop-trigger.md)  
[Inserted Trigger](./inserted-trigger.md)  
[Minimum duration](./minimum-duration.md)  
[Maximum duration](./maximum-duration.md)  
[Allocation](./allocation.md)  

## See also

[Registration Cockpit](../daily-use/registration-cockpit.md)  
[JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)  
[JobManager - Time Sheet](../daily-use/jobmanager-time-sheet.md)  
[JobManager - Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md)  
[Q&A (11 hours rule)](../q-and-a-questions-and-answers/q-and-a-11-hours-rule.md)  
[Post to NAV/BC](../daily-use/post-to-nav-bc.md)  
[Create Pay Transactions](../daily-use/create-pay-transactions.md)
