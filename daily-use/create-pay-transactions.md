# Create Pay Transactions

[Pay Events](../all-tables/pay-events.md) are generated based on the calculated time of day in conjunction with the setup of the [Agreement](../jobmanager-calculations/agreement.md):

| Create Pay Transactions |  |
| :-- | :-- |
| Time Counters | Add up the calculated time for the day |
| Pay Counters | Calculate the Pay Counters based on Time Counters |
| Pay Types | Pay Types are associated with a given Pay Counter |

The function creates the [Pay Events](../jobmanager-calculations/agreement.md) that are relevant for salaries, allowances, absence.

A _Pay Date_ must be specified, which is converted into a _Date Interval_. The start/end date of this _interval_ is respectively first and last day of the _Period_ stated on the employee's [agreement](../jobmanager-calculations/agreement.md).

The basis is [Calculated Lines](../all-tables/calculated-lines.md), [Agreement](../jobmanager-calculations/agreement.md) and [the other pay setup tables](../payroll-setup/README.md).

If [mileage](../all-tables/mileage.md) should be included, the relevant _Work Types_ should be associated a [Pay Type](../payroll-setup/pay-type.md).

All [Pay Events](../jobmanager-calculations/agreement.md) are saved for each Employee per Day. Pay Events can be printed or exported [exported to file](../payroll-setup/pay-export-type.md).

**Need help to [debug](../q-and-a-questions-and-answers/q-and-a-create-pay-transactions.md).**

## See also

[Q&A (Create Pay Transactions)](../q-and-a-questions-and-answers/q-and-a-create-pay-transactions.md)  
[Q&A (Agreement setup)](../q-and-a-questions-and-answers/q-and-a-agreement-setup.md)  
[Time Calculation and Approval](../all-pages/time-calculation-and-approval.md)  
[Payroll Setup](../payroll-setup/README.md)  
[Pre-Pay (Time Calculation)](./pre-pay-time-calculation.md)  
[Export Payroll](./export-payroll.md)
