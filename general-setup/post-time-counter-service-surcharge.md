# Post Time Counter (Service) - Surcharge %

Select which _rate_ is used in connection with [Time Counter posting](../daily-use/pre-pay-time-calculation.md).

*   No,Yes (Unit Cost = Standard NAV)
    *   No posting.
*   Yes (Unit Cost = Pay Rates)
    *   Posting is enabled.
    *   Standard NAV/BC is used to find the rate. In other words, the same rate as if the line is entered _manually_ in the system in e.g. _Job Journal_, _Output Journal_ or similar.
*   Yes (Cost price = Wage rates)
*   Posting is enabled.
    *   The rate is found in the JobManager [Pay Type Rate](../all-tables/pay-type-rate.md) for the relevant _Pay Type_.
*   Yes (Unit Cost = Pay Rates+Surcharge%)
*   Posting is enabled.
    *   The rate is found in the JobManager [Pay Type Rate](../all-tables/pay-type-rate.md) for the relevant _Pay Type_.
    *   To this is added a _Surcharge %_, which is also found in this table.
