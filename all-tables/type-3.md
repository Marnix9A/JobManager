# Type

Use the following options:

*   **Job Id (present)** for warnings/errors if [Job Id](../general-setup/job-id-2.md) specified in [Condition](./condition.md) found in [Stamp Journal](./stamp-journal-lines-2.md) for the employee on the day. Searching [Stamp Journal](./stamp-journal-lines-2.md) can be further narrowed by [Filter Stamp Journal](./filter-stamp-journal.md).
*   **Time Counter (condition)** for warnings/errors if the formula in [Condition](./condition.md) is _true_.
*   **Codeunit** to add customer specific warnings/errors.

By using _Codeunit_ one **avoids** changes to JobManager objects, making updating JobManager versions much easier. _The installation package for JobManager contains some examples._ Read more [here](T6182409_19.htm)

*   **Registration add-on (used)** if Registration add-on is used it will trigger a warning/error.
    
*   **Work type code for mileage (used)** (KM/Miles) if Work type code for mileage is used it will trigger a warning/error.
    

## See also

[API (Registration)](../advanced-setup/api-registration.md)
