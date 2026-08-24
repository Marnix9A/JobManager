# Skip Clock-In & Clock-Out

The following applies if Employee is marked as **Skip Clock-In & Clock-Out**.

In general, this means that the Employee register **without** _Clock-In_ and _Clock-Out_.

In the page [Registration Cockpit](../daily-use/registration-cockpit.md) and [JobManager - Registration Client](../daily-use/jobmanager-registration-client.md):

*   _Clock-In_ and _Clock-Out_ is hidden.
*   Registrations are _always_ done with _today_ as _Profiledate_.
*   _Can't_ register absence.
*   _Clock-In_ is _not_ inserted upon the first registration.
*   Verification of [Leave Warning](./leave-warning.md) is _excluded_.
*   Varification of [Idle Timeout](../other-setup/idle-timeout.md) is _excluded_.

In the pages [JobManager - Time Sheet](../daily-use/jobmanager-time-sheet.md) and [JobManager - Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md):

*   _Clock-In_ and _Clock-Out_ is hidden.
*   If register as [Hours](../other-setup/use-hours.md), the time is set to midnight _(beginning of the day)_.
*   Total hours is _hidden_.

Also note the [Machine](./machine.md) field on this table.
