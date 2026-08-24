# Set default permissions

**Attention: If JobManager is installed as an Extenstion/APP, these Permission Sets already exists (as they are part of the installation).**

The menu item _Set default permissions_ create the below _Permission Sets_, subsequently assigned to _Users_.

If a _BASIC_ Permission Set is selected, common JobManager permissions are added to the selected _BASIC_ Permission Set.

Otherwise **all users** _must_ be assigned to _JOBMAN-ALLUSERS_.

The task is completed when a page is showing the relevant Permission Sets.

| Permission Set | Name |
| :-- | :-- |
| JOBMAN-ALLUSERS | JobMan assign to ALL users |
| JOBMAN-ADMINISTRATOR | JobMan role for administration / payroll |
| JOBMAN-FOREMAN | JobMan role for the foremen / line manager _(eg. Time Calculation and Approval)_ |
| JOBMAN-SHOPFLOOR | JobMan role for the shopfloor _(Time registration)_ |
| JOBMAN-QUESTIONADMIN | JobMan Questionnaire admin |
| JOBMAN-ANSWERAPPROVE | JobMan Answer approver |

**In addition to one or more of the above, a user must also be assigned some basic NAV/BC privileges. For this, choose between the standard NAV/BC Permission Sets.**

**It's recommended NOT to change/add permissions in the above JOBMAN Permission Sets!**

**Usually select YES to overwrite.**

## See also

[Role Center](./role-center.md)
