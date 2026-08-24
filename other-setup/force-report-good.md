# Force Report Good

This option is only applies to production jobs.

Allows to force report [Qty Good](../all-tables/good-qty.md) when changing job (og on Clock-out).

| Option | Upon Stop Time | Upon Finish | Last Operation | Alle operations |
| :-- | :-: | :-: | :-: | :-: |
| Never | No | No | No | No |
| All upon Finish | No | Yes | Yes | Yes |
| All upon Stop Time and Finish | Yes | Yes | Yes | Yes |
| Last Operation upon Finish | No | Yes | Yes | No |
| Last Operation upon Stop Time and Finish | Yes | Yes | Yes | Yes |

Now looks into account quantity reported earlier on the same (this) registration. This avoids errors when the employee has just reported the stop/finish for the registration and accepted, after which the job is immediately reported as finished.

## See also

[Registration Cockpit](../daily-use/registration-cockpit.md)  
[JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)  
[Mobile Role Center](../daily-use/mobile-role-center.md)
