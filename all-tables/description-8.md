# Description

If [Type](./type-3.md) of **Job Id (present)** the following applies:

*   If field _empty_, the system will automatically generate an appropriate text based on the other fields/values.
*   The field can be overridden with custom text. Parameters %1 and %2 can be used, which inserts the appropriate value:
    *   %1 = [Description](../general-setup/description-3.md) from the job.
    *   %2 = [Job Id](../general-setup/job-id-2.md) from the job.

If [Type](./type-3.md) of **Time Counter (condition)** the following applies:

*   If field _empty_, the system will create the text from the _formula_ to the [condition](./condition.md). Numbers on Time Counters are replaced by [Description](../jobmanager-calculations/description.md) from these Time Counters.
*   The field can be overridden with your own text.
