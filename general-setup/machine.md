# Machine

The following applies if Employee is marked as **Machine**:

In the page [Registration Cockpit](../daily-use/registration-cockpit.md) and [JobManager - Registration Client](../daily-use/jobmanager-registration-client.md):

*   The caption is changed to _Machine_ (instead of the Clock-In time).
*   If midnight is passed, active registrations are divided. The active is set to stop at midnight, and new registrations are created for the following day.

Upon [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md):

*   [Wait Jobs](./wait-job-id.md) _aren't_ inserted.
*   Lines passing midnight are divided. Updated to stop at midnight, and new registrations are created for the following day.

In older versions of JobManager _(before 01.18)_ this field had several additional meanings as well. These have been moved to:

*   The field [Skip Clock-In & Clock-Out](./skip-clock-in-and-clock-out.md) in this table.
*   The field [Refresh time](../other-setup/refresh-time.md) in the [JobManager User Interface](../other-setup/jobmanager-user-interface.md) table.
*   The field [Continue registration on Commit](../other-setup/continue-registration-on-commit.md) in the [JobManager User Interface](../other-setup/jobmanager-user-interface.md) table.

## See also

[Registration Cockpit](../daily-use/registration-cockpit.md)  
[JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)
