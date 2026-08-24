# Type

Type of the [Relation](./relation.md):

| Type | Anvendelse |
| :-- | :-- |
| User | Brugerinterface is selected based on the NAV login user . |
| Permission Set | Brugerinterface is selected based on the NAV login users affiliation to _Permission Set_. |
| All | If none of the above where found, this brugerinterface is selected. |
| Employee | Brugerinterface is selected base on the [JobManager Employee](../general-setup/jobmanager-employee.md). (1) |
| Employee Group | Brugerinterface is selected based on the [JobManager Employees](../general-setup/jobmanager-employee.md) affiliation to the [group](../general-setup/employee-groups.md). (1) |
| Test | Inaktiv brugerinterface for testing only. Use the page actions to start _Registration Cockpit_, _Registration Client_ or _Time Sheet_. The field _Stop_ should be _True_. |

1.  These are only used when Employee is selected in the application. That could be _after_ selection Employee in the [JobManager - Registration Client](../daily-use/jobmanager-registration-client.md). However, this can be prevented with [this field](./stop.md).

## See also

[Registration Cockpit](../daily-use/registration-cockpit.md)  
[JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)  
[JobManager - Time Sheet](../daily-use/jobmanager-time-sheet.md)
