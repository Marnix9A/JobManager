# Production Overhead

Allows you to add _overhead_ (additional costs) when [posting time consumption](../daily-use/post-to-nav-bc.md) to _productions_.

The overhead are posted by an extra line in the _Output Journal_.

The overhead are selected by checking all of the following conditions one at a time. The first one which meets the condition is selected:

*   There is overhead for a single production:
    *   [Prod Routing No.](./prod-routing-no.md)
    *   [Prod Routing Ref No.](./prod-routing-ref-no.md)
    *   [Prod Opr. No.](./prod-opr-no.md)
*   There is overhead for a product's route:
    *   [Item Routing No.](./item-routing-no.md)
    *   [Item Opr. No.](./item-opr-no.md)
*   There is overhead for a _Standard operation code_:
    *   [Standard Task Code](./standard-task-code.md)

If [Overhead Number](./overhead-no.md) is specified, the overhead will be posted on it. Otherwise, the value is taken from the [job](../general-setup/jobmanager-job.md).

The field _Active_ is to be filled in to activate calculation. The first time the function is used, a dialog appears to confirm.

**NOTE**: If all of the above search fields are empty, overhead are added to **ALL** registrations.

[Work Center No.](./work-center-no.md)  
[Machine Center](./machine-center.md)  
[Standard Task Code](./standard-task-code.md)  
[Item Routing No.](./item-routing-no.md)  
[Item Opr. No.](./item-opr-no.md)  
[Prod Routing No.](./prod-routing-no.md)  
[Prod Routing Ref No.](./prod-routing-ref-no.md)  
[Prod. Line No.](./prod-line-no.md)  
[Prod Opr. No.](./prod-opr-no.md)  
[Overhead Type](./overhead-type.md)  
[Overhead No.](./overhead-no.md)  
[Gross Time](./gross-time.md)  
[Excl. Break](./excl-break.md)  

## See also

[Post to NAV/BC](../daily-use/post-to-nav-bc.md)
