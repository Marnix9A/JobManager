# Pre-Approval (Responsible)

Setup for Pre-approval of _Jobs_.

[Pre-approval](../other-features/pre-approval.md) is a procedure _ahead_ of [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md). Where the last is typically the Manager in charge of the Employee, then Pre-approval is typically the responsible for _Job_.

The table allows to define a team, group, or all employees - combined with _Jobs_ and/or _Job Tasks_.

Furthermore, the function must be activated [here](../general-setup/activate-pre-approvement.md).

When JobManager decides _who_ to Pre-Approve a [Stamp Journal](../all-tables/stamp-journal-lines-2.md), it's based on the following search table.

_Searching stops when a responsible is found. Automatic Pre-approval is now enabled with blank Pre-Approver - enabled with parameter_

Lock registrations after Pre-Approval (enabled with parameter)

| Ref. Type | Ref. Number | Job No. | Job Task No. | Remark |
| :-- | :-- | :-- | :-- | :-- |
| Employee | Employee No. | Job No. | Job Task No. | Only if [Employee search is activated](../general-setup/use-employee-no.md) **and** if [Job No. search is activated](../general-setup/use-job-no.md) **and** if [Job Task No. search is activated](../general-setup/use-job-task-no.md) |
| Group | [Pre-Approval Group](../general-setup/employee-groups.md) | Job No. | Job Task No. | Only if [Employee Group search is activated](../general-setup/use-employee-group.md) **and** if [Job No. search is activated](../general-setup/use-job-no.md) **and** if [Job Task No. search is activated](../general-setup/use-job-task-no.md) |
| All |  | Job No. | Job Task No. | Only if [All Employees search is activated](../general-setup/use-all-employees.md) **and** if [Job No. search is activated](../general-setup/use-job-no.md) **and** if [Job Task No. search is activated](../general-setup/use-job-task-no.md) |
| Employee | Employee No. | Job No. |  | Only if [Employee search is activated](../general-setup/use-employee-no.md) **and** if [Job No. search is activated](../general-setup/use-job-no.md) |
| Group | [Pre-Approval Group](../general-setup/employee-groups.md) | Job No. |  | Only if [Employee Group search is activated](../general-setup/use-employee-group.md) **and** if [Job No. search is activated](../general-setup/use-job-no.md) |
| All |  | Job No. |  | Only if [All Employees search is activated](../general-setup/use-all-employees.md) **and** if [Job No. search is activated](../general-setup/use-job-no.md) |
| Employee | Employee No. |  |  | Only if [Employee search is activated](../general-setup/use-employee-no.md) |
| Group | [Pre-Approval Group](../general-setup/employee-groups.md) |  |  | Only if [Employee Group search is activated](../general-setup/use-employee-group.md) |
| All |  |  |  | Only if [All Employees search is activated](../general-setup/use-all-employees.md) |

[Type](./type-3.md)  
[Number](./number.md)  
[Job No.](./job-no.md)  
[Job Task No.](./job-task-no.md)  
[Responsible](./responsible.md)  
[Job Description](./job-description.md)  
[Job Description 2](./job-description-2.md)  
[Job Task Description](./job-task-description.md)  

## See also

[Pre-Approval](../other-features/pre-approval.md)  
[Time Calculation and Approval](../all-pages/time-calculation-and-approval.md)
