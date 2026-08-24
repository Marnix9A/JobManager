# Registration approval

Performed **Calculation** and **Approval** of the employees [registrations](../all-tables/stamp-journal-lines-2.md). Typically performed by the Manager in charge of the Employee.

The calculation runs through all registrations and calculates the Employee's time for the day.

*   There is a list of all Employees with one line for each day. These are filtered by [Calucation Group](../general-setup/employee-groups.md) and/or [Approval Group](../general-setup/employee-groups.md). _If the user is [responsible](./responsible.md) for a group, the filter is automatically set accordingly._

The columns can be setup (Almost) after desire. Read more [here](../all-tables/statistics-column.md)

*   Example could be:
    *   Clock-in/Clock-out
    *   Std. hours per day
    *   Weekly hours
    *   Overtime (1-3)
    *   Absence
    *   Flexbalance movement pr. day
    *   Flexbalance
*   At the right the following Fact Boxes _could_ be shown (some _might_ be hidden)
    *   Warnings/Errors
    *   Details for Job Id
    *   Stamp Journal add-on
    *   Mileage
    *   Item consumption
    *   GPS Log
    *   Comments
    *   Employee
    *   Employee Picture
    *   Pay Events

[Edit](N_6182766.htm) opens a new _Page_ with the _marked_ employee registrations for that day.

An Employee are **Calculated** by _checking the box_ [Calculated](./calculated.md) and **Approved** by _checking the box_ [Approved](./approved.md).

If the Employee registrations differs from the [Time Schedule](../jobmanager-calculations/time-schedule.md), there must be entered absence.

It is possible to [delegate](./delegate-calculate-group.md) calculation or approval.

_Setup regarding **Calculation** can be found [here](../jobmanager-calculations/README.md)._

_Need help to [debug](../q-and-a-questions-and-answers/q-and-q-time-calculation.md) **Calculation**._

When the day is **Calculated** specification can be seen in [Period Calculated Lines](../all-tables/calculated-lines.md).

When the day is **Approved** the time is set for posting in the respective NAV modules through [Stamp Events](../all-tables/stamp-events.md). This function must be activated under [Setup](../general-setup/jobmanager-setup.md).

Several employees can be **Calculated** and **Approved** or **Undone** with the functions **Multi calculation**, **Multi approval** or **Undo** ....

The page respect the special statistic column filters when performing the multi actions.

There _could_ be a [Pre-approval](../other-features/pre-approval.md) prior to calculation, typically performed by the employee responsible for _Job_.

To have **permissions** for _Calculate_ or \*Approval\*\* the User should be responsible for a [group](../general-setup/employee-groups.md) of specified type og associated to one of the following [Permission Sets](../other-setup/set-default-permissions.md):

*   SUPER
*   JOBMAN-ADMINISTRATOR

## See also

[Q&Q (Time Calculation)](../q-and-a-questions-and-answers/q-and-q-time-calculation.md)  
[Q&A (Calculation setup)](../q-and-a-questions-and-answers/q-and-a-calculation-setup.md)  
[Pre-Approval](../other-features/pre-approval.md)  
[Stamp Events](../all-pages/stamp-events.md)  
[Post to NAV/BC](./post-to-nav-bc.md)
