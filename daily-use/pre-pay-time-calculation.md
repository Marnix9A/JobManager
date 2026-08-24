# Pre-Pay (Time Calculation)

### Introduction

This job is executed in continuation of the normal [**Time Calculation** and Approval](../all-pages/time-calculation-and-approval.md).

It can insert additional [Time Counters](../jobmanager-calculations/time-counters.md) in [Calculated lines](../all-tables/calculated-lines.md) based on the extra fields found in [Agreement Setup](../all-tables/agreement-setup.md). Agreement Setup is normally used by [Create Pay Transactions](./create-pay-transactions.md).

Furthermore, it is possible that these extra [Calculated lines](../all-tables/calculated-lines.md) can be posted in connection with [Post to NAV/BC](./post-to-nav-bc.md).

This function will normally be able to replace the cases where dayly [Create Pay Transactions](./create-pay-transactions.md) where choosen.

### Setup

To activate the function for an Employee, the field [Pre-Pay Agreement](./pre-pay-agreement.md) must be filled in on the [JobManager Employee](../general-setup/jobmanager-employee.md) table. It _may_ have the same value as the _normal_ [Agreement](./agreement.md).

In order for a rule from [Agreement Setup](../all-tables/agreement-setup.md) to be included in this job, this must be set up in the field[Execution](./execution.md), and the field [Time Conuter](./time-counter.md) must be filled in.

If the value from the [Time Counters](../jobmanager-calculations/time-counters.md) should be posted in connection with [Post to NAV/BC](./post-to-nav-bc.md), there the field [Specify per. Journal stamping](./specify-per-stamp-journal-line.md) on [Agreement Setup Formula](../all-tables/agreement-setup-formula.md) should be selected.

The _rate_ used for posting is set in [JobManager setup](../general-setup/jobmanager-setup.md) in the fields: [Post Time Counter to Production](./post-time-counter-to-production.md), [Post Time Counter to Job](./post-time-counter-job.md) and [Post Time Counter to Service](./post-time-counter-service.md).

### Remarks

As opposed to [Create Pay Transactions](./create-pay-transactions.md), _this_ limits to loop _one_ date.

If it is desired to disconnect the normal posting, this is done by selecting [Only Time Counter](./post-time-counter-job-only.md) on [JobManager setup](../general-setup/jobmanager-setup.md).

## See also

[Time Calculation and Approval](../all-pages/time-calculation-and-approval.md)  
[Post to NAV/BC](./post-to-nav-bc.md)  
[Create Pay Transactions](./create-pay-transactions.md)
