# JobManager Foundation Setup Guide

This guide creates relevant standard setup. Many of these configurations can be _used as_, or they may be changed as required.

**Note: You must run the guide with a NAV client in the language that will be the primary for company!**

The guide does the following:

*   If JobManger has been updated from a previous version, the guide ensures data upgrade.
*   Sets default values in the table [JobManager setup](./jobmanager-setup.md):
    *   [Unit of Measure Code for Capacity Hours](./unit-of-measure-code-for-capacity-hours.md) is set to what _Hours_ are named in this company.
    *   [Dummy Absences Job Jd](./dummy-absence-job-id.md) is set to _Job Id_ for IPC activity _PICK VALUE_.
    *   [Cancel Job Id](./cancel-job-id.md) is set to _Job Id_ for IPC activity _CANCEL_.
    *   [Wait Job Id](./wait-job-id.md) is set to _Job Id_ for IPC activity _WAITJOB_.
    *   [Leave Warning](./leave-warning.md) is set to **16 Hours**.
    *   [Number Series](./job-id.md) for [JobManager Jobs](./jobmanager-job.md) are created (Named **JOBMANJOB** and starts at number **100000**).
    *   Activate create [Jobs](./jobmanager-job.md) for production job type:
        *   [Setup Time](./setup-time-production.md)
        *   [Run Time](./run-time-production.md)
        *   [Wait Time](./wait-time-production.md)
        *   [Move time](./move-time-production.md)
    *   [Job Queue Category Code](../daily-use/job-queue-category-code.md) is set to **JOBMANAGER**.
    *   Creates the following Journals:
        *   [Output](./output-journal.md)(Named **JOBMANAGER**)
        *   [Consumption Journal](./consumption-journal.md) (Named **JOBMANAGER**)
        *   [Job Journal](./job-journal.md) (Named **JOBMANAGER**)
        *   [Job Journal Type](./job-journal-template.md) (Named **JOBS**)
    *   Enable [posting in NAV](../all-tables/stamp-events.md) for the following modules:
        *   [Production](./post-time-to-production.md)
        *   [Job](./post-time-to-job.md)
        *   [Service](./post-service-time.md)
*   Creates relevant [Role Centers](../other-setup/role-center.md).
*   Creates [IPC category](./ipc-category.md) (Named **SYSTEM**) including creation of [IPC activities](../all-tables/ipc-activity.md):
    *   **CLOCK-IN**
    *   **CLOCK-OUT**
    *   **BREAK**
    *   **TEAM START**
    *   **TEAM STOP**
    *   **WAITJOB**
    *   **CANCEL**
    *   **PICK VALUE**
*   Default values are set for [User Interface](../other-setup/jobmanager-user-interface.md).
*   Web Services for the JobManager established **without** activation.
*   Standard options are created in [Pay Export Types](../payroll-setup/pay-export-type.md).
*   Standard options are created in [Custom Fields](../advanced-setup/custom-fields.md).
*   Standard options are created in [Code Hooks](../advanced-setup/code-hooks.md).
*   Standard options are created in [Comments Setup](../other-setup/comments-setup.md).

## See also

[Get started guide](../get-started-guide/README.md)  
[Role Center](../other-setup/role-center.md)
