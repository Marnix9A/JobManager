# Power BI (DIY)

This section provides a brief overview of possible tables for use by Business Intelligence - such as Power BI.

The JobManager installation includes [ready to use examples](../advanced-setup/power-bi.md).

**This section discusses how to make your own BI.**

For OnPremise installations, best performance is achieved by direct SQL access. Some hints for search and delimitation are listed in the following, since SQL uses numerical values for option fields.

Most common tables and fields for use by BI (press the fields to see Caption and further information):

**JobManJob** [JobManager Jobs](../general-setup/jobmanager-job.md)

*   [JobNo](../general-setup/job-id-2.md)
*   [RefType](../general-setup/ref-type.md)
*   [JobType](../general-setup/job-type.md)
*   [RefNo](../general-setup/ref-number.md)
*   [RefSubNo](../general-setup/sub-ref-number.md)
*   [ResourceGroupNo](../general-setup/resource-group-no.md)
*   [ResourceNo](../general-setup/resource-no.md)
*   [WorkCenterNo](../general-setup/work-center-no.md)
*   [MaskinCenterNo](../general-setup/machine-center.md)
*   [Description](../general-setup/description-3.md)
*   [StartDate](../general-setup/starting-date.md)
*   [StartTime](../general-setup/starting-time.md)
*   [StopDate](../general-setup/ending-date.md)
*   [StopTime](../general-setup/ending-time.md)
*   [WokTypeCode](../general-setup/work-type.md)
*   [ReportedFinished](../general-setup/finished.md)
*   [CalculatedTimeDecimal](../general-setup/calculated-time-consump.md)
*   [ProdStatus](../general-setup/prod-status.md)
*   See [here](../general-setup/jobmanager-job.md) for other fields on the table. Note that some of them may be calculated fields that _are not_ in the database.

**JobManStampJournalLine** [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md)

*   [EmployeeNo](../all-tables/employee-6.md)
*   [ProfileDate](../all-tables/profile-date-2.md)
*   [LineSequence](../all-tables/sequence-8.md)
*   [StartDateTime](../all-tables/start-time.md)
*   [StopDateTime](../all-tables/end-time.md)
*   [WorkTypeCode](../all-tables/work-type-2.md)
*   [Active](../all-tables/active-5.md)
*   [JobNo](../all-tables/job-id-5.md)
*   [JobType](../all-tables/job-type-2.md)
*   [RefType](../all-tables/ref-type-2.md)
*   [ReportQtyGood](../all-tables/good-qty.md)
*   [ReportQtyScrap](../all-tables/scrap-qty.md)
*   [SumActualTimeDecimal](../all-tables/time-comsump.md)

## See also

[Power BI](../advanced-setup/power-bi.md)
