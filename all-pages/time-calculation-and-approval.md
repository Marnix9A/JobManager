# Time Calculation and Approval

Note: JobManager 01.32 introduces a new page for [Registration approval](../daily-use/registration-approval.md), which will eventually replace the one below!

Performed **Calculation** and **Approval** of the employees [registrations](../all-tables/stamp-journal-lines-2.md). Typically performed by the Manager in charge of the Employee.

The calculation runs through all registrations and calculates the Employee's time for the day.

*   At the top is a list of all Employees with one line for each day. These are filtered by [Calucation Group](../general-setup/employee-groups.md) and/or [Approval Group](../general-setup/employee-groups.md). _If the user is [responsible](../daily-use/responsible.md) for a group, the filter is automatically set accordingly._
*   In the middle is a list of relevant [Time Counters](../jobmanager-calculations/report-favorite.md) for the selected employee.
*   Below is a list of all registrations for the selected employee. If the line are **not** yet calculated, one can edit these lines.
*   At the right the following Fact Boxes _could_ be shown (some _might_ be hidden)
    *   Warnings/Errors
    *   Details for Job Id
    *   Stamp Journal add-on
    *   Mileage
    *   GPS Log
    *   Comments
    *   Employee
    *   Employee Picture
    *   Pay Events

An Employee are **Calculated** by _checking the box_ [Calculated](../daily-use/calculated.md) and **Approved** by _checking the box_ [Approved](../daily-use/approved.md).

If the Employee registrations differs from the [Time Schedule](../jobmanager-calculations/time-schedule.md), there must be entered absence.

It is possible to [delegate](../daily-use/delegate-calculate-group.md) calculation or approval.

_Setup regarding **Calculation** can be found [here](../jobmanager-calculations/README.md)._

_Need help to [debug](../q-and-a-questions-and-answers/q-and-q-time-calculation.md) **Calculation**._

When the day is **Calculated** specification can be seen in [Period Calculated Lines](../all-tables/calculated-lines.md).

When the day is **Approved** the time is set for posting in the respective NAV modules through [Stamp Events](../all-tables/stamp-events.md). This function must be activated under [Setup](../general-setup/jobmanager-setup.md).

Several employees can be **Calculated** and **Approved** or **Undone** with the functions **Multi calculation**, **Multi approval** or **Undo** ....

There _could_ be a [Pre-approval](../other-features/pre-approval.md) prior to calculation, typically performed by the employee responsible for _Job_.

To have **permissions** for _Calculate_ or \*Approval\*\* the User should be responsible for a [group](../general-setup/employee-groups.md) of specified type og associated to one of the following [Permission Sets](../other-setup/set-default-permissions.md):

*   SUPER
*   JOBMAN-ADMINISTRATOR

## See also

[Registration approval](../daily-use/registration-approval.md)  
[Q&Q (Time Calculation)](../q-and-a-questions-and-answers/q-and-q-time-calculation.md)  
[Q&A (Calculation setup)](../q-and-a-questions-and-answers/q-and-a-calculation-setup.md)  
[Pre-Approval](../other-features/pre-approval.md)  
[Stamp Events](./stamp-events.md)  
[Post to NAV/BC](../daily-use/post-to-nav-bc.md)
