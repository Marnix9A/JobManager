# Power BI

The JobManager installation includes ready to use examples.

Power BI, the perfect tool for analysing all registrations made in JobManager.

Power BI makes it easy to access your data through reports and dashboards. All important information is stored, and you can easily visualise significant trends and developments in your business. Power BI can be set to be updated regularly (available on a daily basis).

The registrations are available for update after they have been calculated, approved and for payroll records, generated earnings.

*   The front page shows graphs for the past six months.
*   Separated by means of statistic groups that deal with both time records, the original registrations and salary records. Salary records are time records that have been processed by using the rules set out in the wage agreement.
*   It is possible to export to PDF, PowerPoint or print.
*   Get a quick overview by subscribing and receiving an email in your inbox as often as you wish. The email shows the page you interested in, as well as a link for quick access.
*   If there is something that needs further investigation, it is possible to create a comment that can be sent to a specific employee for further investigation. The mail that is sent, contains a link with the same information that you want to be examined, with the same filter. A fast and effective tool that leaves nothing to chance.
*   Drill-down by right-clicking and select Drill-down. A detailed report opens with the desired time or salary records.

Detect trends on both time and salary items per employee or per month. Trends in weekly profile and work type distribution. In the company as a whole or specific departments or groups. There are many filter options available.

All useful tools for many levels of management.

You can edit the statistics groups setup in Business Central at any time. After a change in the setup has been made, wait until the next scheduled refresh has been completed or trigger a manuel refresh of the semantic model. After the update, the report will automatically inherit the changes.

Changes will also reflect historical data (but will not affect them).

**SETUP GUIDE FOR _STATISTICS GROUP_ IN NAV/BC:**

The statistic groups are defind in [Jobmanager Bi Group](../all-tables/jobmanager-bi-group.md)

Here you select which groups you want to collect data on:

*   JobManager BI Mapping (Journal Entries / Journal Stamps.)
*   [Time Counters](../jobmanager-calculations/time-counters.md) (Time Entries)
*   [Paytype](../payroll-setup/pay-type.md) (Pay Events)

[Column No.](./column-no.md) defines the order off the columns in the BI Report.

[Caption](./caption-3.md) Is the Caption of the Column in the i BI report.

**JobManager BI Mapping**

Journal Entries is a Comsumption of the registrated time - The raw time from the modules (IPC, Job/project, production. etc.).

Useful tool when you want insight in procceses.

_JobManager BI Mapping_ is a subtable (In JobManager Bi group) Where you can combine _Journal Stamps_.

Examples:

| Ref.Type | Level 1 | Level 2 | Worktype |
| :-- | :-- | :-- | :-- |
| IPC | IPC Categori | IPC Activity |  |
| Job | Resource group | Resource | Worktype |
| Production | Work Centre | Prod.resource (NAV)/ Machincentre (BC) |  |
| Serviceordre | Resource group | Resource |  |
| Assemblyordre | Resource group | Resource |  |

The scenarios are defined from the top down, that it is sufficient to specify an overall combination, that consump the underlying hours. E.g.:

*   Ref.type = Everthing under that ref.type
*   Ref.type + Level 1 = Everthing under that ref.type and level 1
*   Ref.type + Level 1 + Level 2 = Everthing under that ref.type and level 1 and level 2

On Job/Projekts you can combine the combinations above and add a worktype.

Every combination must have a short description, that is usefull if you make a _drilldown_ on the Column header in the BI Report.

You can make several combinations that covers over the same data, without counting doubble in the BI report.

**Time Counters**

Shows the calculated time in relation to the _Time Schedule_, which can be split up on std. hours, overtime, absence etc.

When the column no. and caption are filled out, the specific Time Counters must be _mapped_ with a [BI Group](../jobmanager-calculations/bi-group.md) on the [Time Counter](../jobmanager-calculations/time-counters.md).

To get the best results on the Power BI report, it is important that _Column no._ 99 gets filled out with std. hours/profiletime Time Counter. Then you can make the right percentage calculation e.g.. how many % absence compared to the profiletime.

**Pay Type**

Shows the calculated _Pay Events_ in relation to the Agreement rules. Time and Rates (If you have them in JobManager) will be calculate per _Pay Type_. i.e. It can be calculated ind time and amount - e.g. The cost if an Employee has been sick in X number of days.

When the column no. and caption are filled out, the specific Pay Type must be _mapped_ with a [BI Group](../payroll-setup/bi-group.md) on the [Pay Type](../payroll-setup/pay-type.md).

When NAV/BC BI Groups and mapping is set up, the information must be updated in the Power BI, before it shows any data.

## See also

[Power BI (install)](../all-articles/power-bi-install.md)  
[Power BI (DIY)](../all-articles/power-bi-diy.md)
