# API (Registration)

JobManager offers an API (Application Programming Interface) which can be used to communicate with JobManager from other programs via Web Services.

## Introduction

The solution offers functionality to communicate with JobManager for:

*   Register realtime
    *   Clock-In/-Out
    *   Start/Stop registration
    *   Start/Stop break
*   Register daily in journals
*   Register Item Consumption
*   Register Output Quantity
*   Register Absence

## Prerequisites

The solution support BC14 and above on both On-Premise and SaaS.

From within the _Web Service_ page in standard BC, create an entry for _Codeunit_ with _Object ID_ `6182999` _JobManApiRegistration_. Select a _Service Name_ to use from the external application.

## Common understanding and description of parameters

Below is a description of common parameters for many of the functions.

Some of them are related to functionality within JobManager. Please seek guidance from a consultant who knows the concepts in JobManager.

*   `ApiId`
    *   All functions include a first parameter which should be a _name_ for the external solution. The value is passed through to programmable events with in the JobManager solution, which could be used to _extend_ or _change the behavor_ for certain calls.
    *   Sample `TULIP`.
*   `EmployeeId`
    *   This is the unique identifier for the Employee to register. This could be all values allowed within JobManager:
        *   [Employee Number](../general-setup/employee.md)
        *   [Alternative identification](../general-setup/alternative-identification.md)
        *   [Employee IDs](../all-tables/employee-ids.md)
*   `UserInterfaceRelation`
    *   This could be left blank or a value of an [JobManager User Interface](T_6182351) of _Type_ **API**.
    *   Default User Interface for _All_ is used if blank value.
    *   User Interface for individual Employees could be setup witin JobManager. The API would respect that.
    *   Some behavior of the functions could be controlled with JobManager User Interface.  
        Examples:
        *   Filters on lists of JobManager jobs (Resource, Work Center, Date etc.)
        *   Filters on lists of absence.
        *   Max records to return i list of Items.
        *   Whether absence is required.
        *   [Default Stop-code](./stop-code.md) for registrations.
*   `SearchText` could be used to make server site search in list of jobs. The server search for the value in the following fields:
    *   JobNo
    *   Description
    *   RefNo
    *   RefSubNo
*   `TimeOffsetUTC`
    *   Functions that should transfer a _DateTime_ should also send the _Time Zone_. This value should be send as +/- **minuts** from UTC. That is `120` for _GMT+2_.
*   `JobNo`
    *   Unique number of every entry within the [JobManager Jobs](../general-setup/jobmanager-job.md) table.
*   `StampJournalLineSequence`
    *   Unique number for every _time registration line_ in JobManager called [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md) within JobManager.
    *   The value is used whenever calling functions for an time registration. That could be:
        *   ItemConsumption, JobStop, JobFinish, JobQtyGood, JobQtyScrap etc.
    *   The value could be obtain from either
        *   GetFirstActiveJobLineSequence

## Description of functions

Functions that need to return a _complex_ list (typical Subfixed with `_Soap`) as they return using Soap/XML.

For register _realtime_ (equals to a _Punch Clock_ or _Time Clock_) use the functions: `SignIn, SignOut, BreakStart, BreakStop, JobStart, JobFinish, JobQtyGood, JobQtyScrap`.

For register _asynchronous_ in a _JobManager Journal_ use the functions: `RegAddSignIn, RegAddSignOut, RegAddBreak, RegInsert, RegModify, REgDelete, RegTotal`.

The other functions should be common for the two scenarios.

### Functions

#### `GetJob_Soap(_ApiId : Code[10];_JobNo : Code[20];VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get the fields with information for one [JobManager Job](../general-setup/jobmanager-job.md).

Parameters:

*   \_ApiId _See common description above_.
*   \_JobNo is the job to lookup. _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListAbsence_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible absences. Could be used for picking a _JobNo_ to use as parameter _JobNoAbsence_ to the functions _SignIn_ or _SignOut_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListIpc_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _IPC_.

Filters on the list will be filled in automatically according to setup within BC for the given Employee and/or the given User Interface.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListIpcFilter_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_FilterCategoryNo : Text;_FilterActivityNo : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _IPC_.

Filters could be appliesd with the two \*\_Filter...\* parameters.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_FilterCategoryNo could be used to apply filters on _IPC Categories_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_FilterActivityNo could be used to apply filters on _IPC Activities_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListIpcTopX_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _IPC_.

This will show the latest _X_ used Jobs according to [this](../other-setup/filter-top-x.md).

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListProduction_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Production_. Thats jobs related to the Production module of BC.

Filters on the list will be filled in automatically according to setup within BC for the given Employee and/or the given User Interface.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListProductionFilter_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_FilterWorkCenter : Text;_FilterMachineCenter : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Production_. Thats jobs related to the Production module of BC.

Filters could be appliesd with the two \*\_Filter...\* parameters.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_FilterWorkCenter could be used to apply filters on _Work Centers_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_FilterMachineCenter could be used to apply filters on _Machine Centers_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListProductionTopX_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Production_. Thats jobs related to the Production module of BC.

This will show the latest _X_ used Jobs according to [this](../other-setup/filter-top-x.md).

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListJob_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Job_. Thats jobs related to the Job/Project module of BC.

Filters on the list will be filled in automatically according to setup within BC for the given Employee and/or the given User Interface.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListJobFilter_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_FilterResourceGroupNo : Text;_FilterResourceNo : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Job_. Thats jobs related to the Job/Project module of BC.

Filters could be appliesd with the two \*\_Filter...\* parameters.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_FilterResourceGroupNo could be used to apply filters on _Resource Groups_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_FilterResourceNo could be used to apply filters on _Resources_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListJobTopX_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Job_. Thats jobs related to the Job/Project module of BC.

This will show the latest _X_ used Jobs according to [this](../other-setup/filter-top-x.md).

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListService_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Service_. Thats jobs related to the Service module of BC.

Filters on the list will be filled in automatically according to setup within BC for the given Employee and/or the given User Interface.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListServiceFilter_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_FilterResourceGroupNo : Text;_FilterResourceNo : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Service_. Thats jobs related to the Service module of BC.

Filters could be appliesd with the two \*\_Filter...\* parameters.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_FilterResourceGroupNo could be used to apply filters on _Resource Groups_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_FilterResourceNo could be used to apply filters on _Resources_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListServiceTopX_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Service_. Thats jobs related to the Service module of BC.

This will show the latest _X_ used Jobs according to [this](../other-setup/filter-top-x.md).

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListAssembly_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Assembly_. Thats jobs related to the Assembly Order module of BC.

Filters on the list will be filled in automatically according to setup within BC for the given Employee and/or the given User Interface.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListAssemblyFilter_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_FilterWorkCenter : Text;_FilterMachineCenter : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Assembly_. Thats jobs related to the Assembly Order module of BC.

Filters could be appliesd with the two \*\_Filter...\* parameters.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_FilterResourceGroupNo could be used to apply filters on _Resource Groups_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_FilterResourceNo could be used to apply filters on _Resources_. The syntax is standard BC filters (eq. `@ * |` etc.)
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetJobListAssemblyTopX_Soap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_JobManJob : XMLport JobManApi_JobManJob)`

Get a list of possible [JobManager Jobs](../general-setup/jobmanager-job.md) of [Type](../general-setup/ref-type.md) _Assembly_. Thats jobs related to the Assembly Order module of BC.

This will show the latest _X_ used Jobs according to [this](../other-setup/filter-top-x.md).

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText _See common description above_.
*   \_JobManApi\_JobManJob is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetListItem(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_SearchText : Text;VAR _JobManApi_Item : XMLport JobManApi_Item)`

Get a list of _Items_ from the standard BC _Items table_. The _Items_ marked as _Blocked_ within BC is _excluded_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_SearchText could be used to make server site search in list of Items. The server search for the value in the following _No._ and _Description_ fields.
*   \_JobManApi\_Item is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetListItemVariant(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ItemNo : Code[20];VAR _JobManApi_ItemVariant : XMLport JobManApi_ItemVariant)`

Get a list of _Item Variants_ from the standard BC _Item Variant table_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ItemNo for the related _Item Number_.
*   \_JobManApi\_ItemVariant is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetListLocation(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ItemNo : Code[20];_VariantCode : Code[10];VAR _JobManApi_Location : XMLport JobManApi_Location)`

Get a list of _Locations_ from the standard BC _Location table_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ItemNo for the related _Item Number_.
*   \_VariantCode for the related _Item Variant_.
*   \_JobManApi\_Location is not realy a parameter, but the way BC indicates the fields to be returned.

#### `GetListBin(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ItemNo : Code[20];_VariantCode : Code[10];_LocationCode : Code[10];VAR _JobManApi_Bin : XMLport JobManApi_Bin)`

Get a list of _Bins_ from the standard BC _Bins table_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ItemNo for the related _Item Number_.
*   \_VariantCode for the related _Item Variant_.
*   \_LocationCode for the related _Location_.
*   \_JobManApi\_Bin is not realy a parameter, but the way BC indicates the fields to be returned.

#### `ItemConsumptionGetList(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_StampJournalLineSequence : Integer;VAR _JobManApi_ItemConsumption : XMLport JobManApi_ItemConsumption)`

Get a list of _Items_ that is _planned_ or _actual_ used for the associated [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md). For _Productions_ thats the _Component List_, for _Job/Project_ thats _planned item comsumption_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_StampJournalLineSequence _See common description above_.
*   \_JobManApi\_ItemConsumption is not realy a parameter, but the way BC indicates the fields to be returned.

#### `ItemConsumptionAdd(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;StampJournalLineSequence : Integer;_ItemNo : Code[20];_ItemQty : Decimal;_ItemVariantCode : Code[10];_ItemSerialNo : Code[50];_ItemLotNo : Code[50];_ItemLocationCode : Code[10];_ItemBinCode : Code[20];_ItemPackageNo : Code[50])`

Add a new item consumption for the associated [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md). It's inserted as and [Stamp Event](../all-tables/stamp-events.md) for [posting](../daily-use/post-to-nav-bc.md).

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. This could be left blank. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_StampJournalLineSequence _See common description above_.
*   \_ItemNo to use.
*   \_ItemQty to use.
*   \_ItemVariantCode to use (optional).
*   \_ItemSerialNo to use (optional).
*   \_ItemLotNo to use (optional).
*   \_ItemLocationCode to use (optional).
*   \_ItemBinCode to use (optional).
*   \_ItemPackageNo to use (optional).
*   \_JobManApi\_ItemConsumption is not realy a parameter, but the way BC indicates the fields to be returned.

#### `ItemConsumptionFieldsEnabled(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ItemNo : Code[20]) RetText : Text`

_Optional_ this functions _can_ be used to indicate for the users which fields could be filled in for the _ItemConsumptionAdd_ function above.

The function returns a text with _Yes_/_No_ for each of the optional parameters for _ItemConsumptionAdd_.

Sample return value `variant=yes;serial=no;lot=no;location=yes;bin=no;package=no`

#### `GetFirstActiveJobLineSequence(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;VAR _ReturnStampJournalLineSequence : Integer)`

Get the current _active_ [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md) for the specified Employee.

If working on more than _one_ job, this function will return the first. If by any change the Employee are allowed to work on several jobs, known as [Bundle](../other-setup/bundle-allocation.md), it's recommended to use the the `GetListActiveJobs` function as shown below.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ReturnStampJournalLineSequence is the returnvalue from the function. _See common description for StampJournalLineSequence above_.

The \*\_ReturnStampJournalLineSequence\* equals to the _StampJournalLineSequence_ which should be used as parameters to other functions.

#### `GetListActiveJobs(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;VAR _JobManApi_JobManStampJournalLn : XMLport JobManApi_JobManStampJournalLn)`

Get the current _active_ [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md) for the specified Employee.

If always working on only _one_ job at the time, the `GetFirstActiveJobLineSequence` function could be used for more easy access to the StampJournalLineSequence.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_JobManApi\_JobManStampJournalLn is not realy a parameter, but the way BC indicates the fields to be returned.

The _LineSequence_ field within the returned list equals to the _StampJournalLineSequence_ which should be used as parameters to other functions.

#### `GetAbsenceRequired(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer) : Integer`

Use this function to determine whether Absence should or could be applied upon _SignIn_ and _SignOut_ functions below.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_TimeoffsetUTC _See common description above_.

The return value:

*   `0` for Never
*   `1` for Optional
*   `2` for Force

#### `SignIn(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer;_JobNoAbsence : Code[20])`

Use this function to Clock-In an Employee in realtime.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_TimeoffsetUTC _See common description above_.
*   \_JobNoAbsence is an optional cause of Absence.
    *   That is a reason to _Clock-In_ to late.
    *   Use the _GetAbsenceRequired_ function to determine whether an Absence should be included.
    *   Use the _GetJobListAbsence\_Soap_ function to pick the cause of Absence to send as parameter to this.

#### `SignOut(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer;_JobNoAbsence : Code[20])`

Use this function to Clock-Out an Employee in realtime.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_TimeoffsetUTC _See common description above_.
*   \_JobNoAbsence is an optional cause of Absence.
    *   That is a reason to _Clock-Out_ to early.
    *   Use the _GetAbsenceRequired_ function to determine whether an Absence should be included.
    *   Use the _GetJobListAbsence\_Soap_ function to pick the cause of Absence to send as parameter to this.

#### `BreakStart(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer)`

Use this function to start a break in realtime.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_TimeoffsetUTC _See common description above_.

#### `BreakStop(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text)`

Use this function to stop a break in realtime.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.

#### `JobStart(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer;_JobNo : Code[20];_BundleContinue : Boolean)`

Use this function to start a [JobManager Job](../general-setup/jobmanager-job.md) in realtime.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_TimeoffsetUTC _See common description above_.
*   \_JobNo is the JobManager job to start. This is the _JobNo_ from one of the _GetJobListXxx_ functions.
*   \_BundleContinue
    *   True to start the job, and still keep working on the on already started.
    *   False to start the job. The _active_ jobs shoul either
        *   stopped with functions _JobStop_ or _JobFinish_.
        *   stopped automatically using the [Default Stop-code](../other-setup/default-stop-code.md).

#### `JobStop(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_StampJournalLineSequence : Integer)`

Use this function to _stop_ a [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md) in realtime.

_Stop_ means _stop the time but keep the JobManager Job open for later registration_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_StampJournalLineSequence _See common description above_.

#### `JobFinish(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_StampJournalLineSequence : Integer)`

Use this function to report _finish_ a [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md) in realtime.

_Finish_ means _stop the time AND report the JobManager Job as finished_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_StampJournalLineSequence _See common description above_.

#### `JobQtyGood(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_StampJournalLineSequence : Integer;_QtyGood : Decimal)`

Use this function to report _Output Quantity_ for Production Orders or Assembly Orders related to a [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md) in realtime.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_StampJournalLineSequence _See common description above_.
*   \_ QtyGood is the Quantity to report.

#### `JobQtyScrap(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_StampJournalLineSequence : Integer;_QtyScrap : Decimal)`

Use this function to report _Scrap Quantity_ for Production Orders related to a [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md) in realtime.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_StampJournalLineSequence _See common description above_.
*   \_ QtyScrap is the scrap Quantity to report.

#### `RegAddSignIn(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ProfileDate : Date;_TimeOffsetUTC : Integer;_RegDateTime : DateTime) NewJournalLineSequence : Integer`

Use this function to insert a Clock-In registration in the JobManager Journal.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ProfileDate is the _Profiledate_ to hold the registration.
*   \_TimeoffsetUTC _See common description above_.
*   \_RegDateTime is the actual time to register the Clock-In.

The function returns the _StampJournalLineSequence_ for the new line. _See common description above_.

#### `RegAddSignOut(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ProfileDate : Date;_TimeOffsetUTC : Integer;_RegDateTime : DateTime) NewJournalLineSequence : Integer`

Use this function to insert a Clock-Out registration in the JobManager Journal.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ProfileDate is the _Profiledate_ to hold the registration.
*   \_TimeoffsetUTC _See common description above_.
*   \_RegDateTime is the actual time to register the Clock-Out.

The function returns the _StampJournalLineSequence_ for the new line. _See common description above_.

#### `RegAddBreak(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ProfileDate : Date;_TimeOffsetUTC : Integer;_StartDateTime : DateTime;_StopDateTime : DateTime;_RegHours : Decimal) NewJournalLineSequence : Integer`

Use this function to insert a Break registration in the JobManager Journal.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ProfileDate is the _Profiledate_ to hold the registration.
*   \_TimeoffsetUTC _See common description above_.
*   \_StartDateTime is the actual time to register start of the break
*   \_StopDateTime is the actual time to register start of the break. The value should be the same as \_StarteDateTime if \*\_RegHours\* below is used.
*   \_RegHours is optional, but should be used if enabled with the [Use Hours](../other-setup/use-hours.md) on the [JobManager User Interface](../other-setup/jobmanager-user-interface.md).

The function returns the _StampJournalLineSequence_ for the new line. _See common description above_.

#### `RegInsert(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ProfileDate : Date;_TimeOffsetUTC : Integer;_StartDateTime : DateTime;_StopDateTime : DateTime;_JobNo : Code[20];_RegHours : Decimal;_WorkTypeCode : Code[10];_PostingDescription1 : Text;_PostingDescription2 : Text) NewJournalLineSequence : Integer`

Use this function to insert working on a [JobManager Job](../general-setup/jobmanager-job.md) in the JobManager Journal.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ProfileDate is the _Profiledate_ to hold the registration.
*   \_TimeoffsetUTC _See common description above_.
*   \_StartDateTime is the actual time to register start of the break
*   \_StopDateTime is the actual time to register start of the break. The value should be the same as \_StarteDateTime if \*\_RegHours\* below is used.
*   \_JobNo is the JobManager job to register. This is the _JobNo_ from one of the _GetJobListXxx_ functions.
*   \_RegHours is optional, but should be used if enabled with the [Use Hours](../other-setup/use-hours.md) on the [JobManager User Interface](../other-setup/jobmanager-user-interface.md).
*   \_WorkTypeCode is optional.
*   \_PostingDescription1 is optional.
*   \_PostingDescription2 is optional.

The function returns the _StampJournalLineSequence_ for the new line. _See common description above_.

#### `RegModify(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_LineSequence : Integer;_ProfileDate : Date;_TimeOffsetUTC : Integer;_StartDateTime : DateTime;_StopDateTime : DateTime;_JobNo : Code[20];_RegHours : Decimal;_WorkTypeCode : Code[10];_PostingDescription1 : Text;_PostingDescription2 : Text) : Boolean`

Use this function to _modify_ an existing registration in the JobManager Journal.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_LineSequence equals to th _StampJournalLineSequence_ for the line to modify. _See common description above_.
*   \_ProfileDate is the _Profiledate_ to hold the registration.
*   \_TimeoffsetUTC _See common description above_.
*   \_StartDateTime is the actual time to register start of the break
*   \_StopDateTime is the actual time to register start of the break. The value should be the same as \_StarteDateTime if \*\_RegHours\* below is used.
*   \_JobNo is the JobManager job to register. This is the _JobNo_ from one of the _GetJobListXxx_ functions.
*   \_RegHours is optional, but should be used if enabled with the [Use Hours](../other-setup/use-hours.md) on the [JobManager User Interface](../other-setup/jobmanager-user-interface.md).
*   \_WorkTypeCode is optional.
*   \_PostingDescription1 is optional.
*   \_PostingDescription2 is optional.

#### `RegDelete(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_LineSequence : Integer) : Boolean`

Use this function to _remove_ an existing registration in the JobManager Journal.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_LineSequence equals to th _StampJournalLineSequence_ for the line to modify. _See common description above_.

#### `RegTotal(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_ProfileDate : Date) ReturnText : Text`

The function returns a text holding the totals for the lines in the JobManager Journal. Could be used to show the Employee totals for inserted lines.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_ProfileDate is the _Profiledate_ to sum registrations.

#### `IsSignedIn(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text) : Boolean`

Use this function determine wheter an Employee is currently Clocked-In (SignIn) or not.

This function could be used to hide/show Clock-In/-Out buttons:

*   Only show Clock-In if this function is _False_.
*   Only show Clock-Out if this function is _True_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.

#### `IsPilot(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text) : Boolean`

Use this function determine wheter an Employee is currently an _Pilot_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.

#### `IsAssistantTo(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text) : Code[20]`

Use this function determine wheter an Employee is currently an _Assistant_ in a _Team_. The function return the _Employee No_ for the _Pilot_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.

#### `GetTeam(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text) CurrentTeam : Text`

If the Employee is currently register as part of a Team, this function will return a list of all Employees in the Team.

The result is returned as a simple _semi colon_ string: `AH;MD;TS`.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.

#### `TeamStart(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer;_PilotNo : Code[20])`

This function will start a Teams registration within JobManager. This means the given Employees registrations will _follow_ the registrations of the _Pilot_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_PilotNo is the Employee to _follow_.

#### `TeamStop(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer)`

This will stop the current _Team_ registration for this Employee.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.

#### `TeamChangePilot(_ApiId : Code[10];_EmployeeId : Text;_UserInterfaceRelation : Text;_TimeOffsetUTC : Integer;_PilotNo : Code[20])`

This function will change the _Pilot_ witin a _Team_ to one of the others in the current running _Team_.

Parameters:

*   \_ApiId _See common description above_.
*   \_EmplooyeeId is the current Employee. _See common description above_.
*   \_UserInterfaceRelation _See common description above_.
*   \_PilotNo is the _new_ Employee to _follow_.

## See also

[Code customization](./code-customization.md)
