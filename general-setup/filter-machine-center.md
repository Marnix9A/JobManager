# Filter Machine Center

The filter fields below are used for showing jobs in pages:

*   [JobManager – Registration Cockpit](../daily-use/registration-cockpit.md)
*   [JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)
*   [JobManager - Time Sheet](../daily-use/jobmanager-time-sheet.md)
*   [JobManager - Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md)

The filters also applies to both [JobManager Mobile](../daily-use/mobile-role-center.md) and the deprecated [Mobile Registration Client App](../mobile-registration-client-app/README.md).

The following fields could be used:

[JobManager Employee table](./jobmanager-employee.md)

*   Filter Option
*   Filter IPC Category
*   Filter IPC Activity
*   Filter Resource Group
*   Filter Resource
*   Filter Work Center
*   Filter Machine Center

[JobManager User Interface table](../other-setup/jobmanager-user-interface.md)

*   Filter IPC Category
*   Filter IPC Activity
*   Filter Resource Group
*   Filter Resource
*   Filter Work Center
*   Filter Machine Center

**Read [here](../all-articles/filter-input.md) to learn about the _syntax_ for filters.**

_IPC Category_ and _IPC Activity_ are used for [Jobs](./jobmanager-job.md) of Type _IPC_. _Resource Group_ and _Resource_ are used for [Jobs](./jobmanager-job.md) from Job and Service. _Work Center_ and _Machine Center_ are used for [Jobs](./jobmanager-job.md) from Production.

**Before** selection of Employee in _JobManager - Registration Client_ the filters from _JobManager User Interface_ are used.

**When** Employee _is_ selected in _JobManager - Registration Client_, the _Filter Option_ on _JobManager Employee table_ determines the use of filters:

*   _From Employee_
    *   The filters are fixed to the filter values from _JobManager Employee Table_
*   _Last Work Center / Resource Group_
    *   The _Work Center_ and _Resource Group_ filters are set to the values from the employees last registration.
*   _Last Machine Center / Resource_
    *   The _Work Center_, _Machine Center_, _Resource Group_ og _Resource_ filters are set to the values from the employees last registration.

In addition the [JobManager User Interface tabellen](../other-setup/jobmanager-user-interface.md) have 4 fields to hide change of filters. If a given change of filter are _hidden_, any associated filter value on _JobManager User Interface_ will be applied.

## See also

[Filter input](../all-articles/filter-input.md)  
[Registration Cockpit](../daily-use/registration-cockpit.md)  
[JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)  
[JobManager - Time Sheet](../daily-use/jobmanager-time-sheet.md)  
[JobManager - Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md)  
[Mobile Role Center](../daily-use/mobile-role-center.md)  
[Mobile Registration Client App](../mobile-registration-client-app/README.md)
