# Code customization

JobManager can be customized with _Events_ or use some of the special options for setup calls to _Codeunits_. See below at the bottom **See also** for complete list for using Codeunits.

Codeunit _6182705 JobManNavEventPublisher_ has a complete list of _Events_ publisered by JobManager. Some of these are described in the list below.

**The installation package for JobManager contains some examples.**

*   **OnDuration2HoursMin**
    *   Override how time is displayed as _x h y min_.
*   **OnDuration2HoursMin\_CaptionExt**
    *   Override caption for fields regarding the above.
*   **OnDecideInsertUpdateIpcActivity2JobManJob**
    *   Can be used to _skip_ create jobs in [JobManager Jobs](../general-setup/jobmanager-job.md).
*   **OnDecideInsertUpdateProdOrderRoutingLine2JobManJob**
    *   Can be used to _skip_ create jobs in [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   _From JobManager 01.28 and NAV 2018, this can often be replaced by a filter set up in the JobManager Setup page._
*   **OnDecideInsertUpdateJobPlanningLine2JobManJob**
    *   Can be used to _skip_ create jobs in [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   _From JobManager 01.28 and NAV 2018, this can often be replaced by a filter set up in the JobManager Setup page._
*   **OnDecideInsertUpdateServiceLine2JobManJob**
    *   Can be used to _skip_ create jobs in [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   _From JobManager 01.28 and NAV 2018, this can often be replaced by a filter set up in the JobManager Setup page._
*   **OnDecideInsertUpdateServiceOrderAllocation2JobManJob**
    *   Can be used to _skip_ create jobs in [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   _From JobManager 01.28 and NAV 2018, this can often be replaced by a filter set up in the JobManager Setup page._
*   **OnDecideInsertUpdateAssemblyLine2JobManJob**
    *   Can be used to _skip_ create jobs in [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   _From JobManager 01.28 and NAV 2018, this can often be replaced by a filter set up in the JobManager Setup page._
*   **OnAfterInsertUpdateIpcActivity2JobManJob**
    *   Can be used to change/assign field values when creating [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   Eg. used in combination with [Custom Fields](./code-hooks.md).
    *   Remember `_JobManJob.MODIFY(TRUE)`
*   **OnAfterInsertUpdateProdOrderRoutingLine2JobManJob**
    *   Can be used to change/assign field values when creating [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   Eg. used in combination with [Custom Fields](./code-hooks.md).
    *   Remember `_JobManJob.MODIFY(TRUE)`
*   **OnAfterInsertUpdateJobPlanningLine2JobManJob**
    *   Can be used to change/assign field values when creating [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   Eg. used in combination with [Custom Fields](./code-hooks.md).
    *   Remember `_JobManJob.MODIFY(TRUE)`
*   **OnAfterInsertUpdateServiceLine2JobManJob**
    *   Can be used to change/assign field values when creating [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   Eg. used in combination with [Custom Fields](./code-hooks.md).
    *   Remember `_JobManJob.MODIFY(TRUE)`
*   **OnAfterInsertUpdateServiceOrderAllocation2JobManJob**
    *   Can be used to change/assign field values when creating [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   Eg. used in combination with [Custom Fields](./code-hooks.md).
    *   Remember `_JobManJob.MODIFY(TRUE)`
*   **OnAfterInsertUpdateAssemblyLine2JobManJob**
    *   Can be used to change/assign field values when creating [JobManager Jobs](../general-setup/jobmanager-job.md).
    *   Eg. used in combination with [Custom Fields](./code-hooks.md).
    *   Remember `_JobManJob.MODIFY(TRUE)`
*   **OnDecideCopyRegJournalLine**
    *   Can be used to define which jobs are to be copied.
*   **OnAfterCopyRegJournalLine**
    *   Can be used to postprocess the copied lines.
*   **JobManJob\_OnReportedFinishedCheck**
    *   Can be used to expand check if the job is completed.
*   **JobManJobBundle\_OnBefore\_AddJob**
    *   Used in job registration.
    *   Can manipulate [Job Id](../general-setup/job-id-2.md) before using the value.
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **JobManJobBundle\_OnAfter\_MakeRegistrations**
    *   Used after make registrations, where extra functionality can be added.
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnBeforeCalcalculate**
    *   Used in connection with [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md) where it is called just _before_ Time Calculation.
*   **OnAfterCalcalculate**
    *   Used in connection with [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md) where it is called just _after_ Time Calculation.
*   **OnBeforeApprove**
    *   Used in connection with [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md) where it is called just _before_ Approval.
*   **OnAfterApprove**
    *   Used in connection with [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md) where it is called just _after_ Approval.
*   **OnBeforeJobManReportItemLoad**
    *   Used to integrate with the JobManager Item Consumption page - _before_ standard insert items.
*   **OnAfterJobManReportItemLoad**
    *   Used to integrate with the JobManager Item Consumption page - _after_ standard insert items.
*   **OnBeforeJobManReportItemSave**
    *   Used to integrate with the JobManager Item Consumption page - _before_ standard commits the items.
*   **OnAfterJobManReportItemSave**
    *   Used to integrate with the JobManager Item Consumption page - _before_ standard commits the items.
*   **OnBeforeJobManNavPostOutputJournalInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert line.
*   **OnAfterJobManNavPostOutputJournalInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ insert line.
*   **OnBeforeJobManNavPostOutputJournalInsertOverhead**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert line.
*   **OnAfterJobManNavPostOutputJournalInsertOverhead**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ insert line.
*   **OnBeforeJobManNavPostOutputJournalInsertCalcLine**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert (from JobManStampCalcLine) line.
*   **OnBeforeJobManNavPostOutputJournalRunPost**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ calling for posting.
*   **OnAfterJobManNavPostOutputJournalRunPost**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ calling for posting.
*   **OnBeforeJobManNavPostProductionJournalInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert line.
*   **OnAfterJobManNavPostProductionJournalInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ insert line.
*   **OnBeforeJobManNavPostProductionJournalRunPost**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ calling for posting.
*   **OnAfterJobManNavPostProductionJournalRunPost**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ calling for posting.
*   **OnBeforeJobManNavPostJobJournalValidateType**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ validate the _Type_ field.
*   **OnBeforeJobManNavPostJobJournalInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert line.
*   **OnAfterJobManNavPostJobJournalInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ insert line.
*   **OnBeforeJobManNavPostJobJournalInsertCalcLine**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert (from JobManStampCalcLine) line.
*   **OnBeforeJobManNavPostJobJournalRunPost**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ calling for posting.
*   **OnAfterJobManNavPostJobJournalRunPost**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ calling for posting.
*   **OnCheckJobManNavPostServiceLineAllowRepost**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV.
    *   Can be used to change whether _re_posting is allowed. For example, when approving again after revoking approval. This can be useful if customer customization is made that allows posting of negative lines (when revoking approval).
*   **OnBeforeJobManNavPostServiceLineInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert line.
*   **OnAfterJobManNavPostServiceLineInsert**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ insert line.
*   **OnBeforeJobManNavPostServiceLineInsertCalcLine**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _before_ insert (from JobManStampCalcLine) line.
*   **OnAfterJobManNavPostServiceLineRun**
    *   Used in [posting](../daily-use/post-to-nav-bc.md) to NAV - _after_ insert ALL lines.
*   **OnTimeCalcEmployee\_CalcUpdateJournalLine**
    *   Used in connection with [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md) for copying relevant information regarding automatic inserted lines caused by _Wait Jobs_.
*   **OnAfterJobManPayEntry2JobJournal**
    *   Used in _Post Pay to Job_ - _before_ insert line.
*   **OnPayCalcEmployee**
    *   Used in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnFontMgtInit**
    *   _Discontinued!_
*   **OnJobManParameter\_Discover**
    *   Used when inserting new parameters in the common JobManager Parameter table.
*   **OnJobManParameter\_GetGroupDescription**
    *   Used for naming the group for new parameters in the common JobManager Parameter table.
*   **OnJobManPayAPI\_Discover**
    *   Used by a [Pay API](../all-tables/pay-api.md) to _create_ this in NAV/BC.
*   **OnJobManPayAPI\_DefaultParmText**
    *   Used by a [Pay API](../all-tables/pay-api.md) to set its default parameters.
*   **OnJobManPayAPIHandler\_GetEmployeeSeniorityDate**
    *   Used by a [Pay API](../all-tables/pay-api.md) to override the the field [Seniority Date](../general-setup/seniority-date.md) on JobManager Employee.
*   **OnJobManPayAPIHandler\_PickPayTypeExternalNo**
    *   Used by a [Pay API](../all-tables/pay-api.md) for _table lookup_ in the field [External No.](../payroll-setup/external-no.md).
    *   Easiest way to add options is to insert them in the temporary table with `_JobManTmpList.AddCodeDescription('V1', 'First value')` and _only_ set `_HandledList: = TRUE`.
*   **OnJobManPayAPIHandler\_PayExp\_Init**, **OnJobManPayAPIHandler\_PayExp\_Dialog**, **OnJobManPayAPIHandler\_PayExp\_PreRun**, **OnJobManPayAPIHandler\_PayExp\_PayLine**, **OnJobManPayAPIHandler\_PayExp\_AbsenceLine** and **OnJobManPayAPIHandler\_PayExp\_PostRun**
    *   Used by the _generic_ [Pay Export Type](../payroll-setup/pay-export-type.md) _API transfer Pay_, which handles exports in combination with [Pay API](../all-tables/pay-api.md).
    *   If the functions \_Init, \_Dialog, \_PreRun, \_PayLine, \_AbsenceLine and \_PostRun are to have global variables, Subscriber Codeunit must be declared as _SingleInstance_.
*   **OnJobManPayExport\_Discover**
    *   Used by a [Pay Export Type](../payroll-setup/pay-export-type.md) to _create_ this in NAV/BC.
*   **OnComment\_OpenAttachment**
    *   Used when new special setup is added to [Comments Setup](../other-setup/comments-setup.md).
*   **OnComment\_AddAttachment**
    *   Used when new special setup is added to [Comments Setup](../other-setup/comments-setup.md).
*   **OnComment\_LoadBigTextFromAttachment**
    *   Used when new special setup is added to [Comments Setup](../other-setup/comments-setup.md).
*   **OnCodeunit\_JobManSystemSetup\_Pre** and **OnCodeunit\_JobManSystemSetup\_Post**
    *   Called respectively _before_ and _after_ other actions i [JobManager Foundation Setup Guide](../general-setup/jobmanager-foundation-setup-guide.md)
*   **OnCodeunit\_JobManStampHeaderUpdate\_RunFromRoleCenter**
    *   Use it to diable refresh data in _Employee Stamp Sum_ upon refresh role centers. See also [Update Employee Stamp Sum](../general-setup/update-employee-stamp-sum.md).
*   **OnCodeunit\_JobManRegComFunc\_AbsReqSetFilterJobManPlannedJobs**
    *   Can apply extra filter on the page showing the employees [planned absence](../all-pages/planned-absence.md).
*   **OnCodeunit\_JobManRegComFunc\_AbsReqSetFilterJobManJob**
    *   Can apply extra filter on the page showing the list of absences, when employee request new [planned absence](../all-pages/planned-absence.md).
*   **OnCodeunit\_JobManRegComFunc\_EmployeeChangePassword**
    *   Can be used to validate new PIN-Code or override the change.
*   **OnCodeunit\_JobManRegJournalFunctions\_GetJournalTotals**
    *   Override the text presented as _total_ on the [JobManager Time Sheet](../daily-use/jobmanager-time-sheet.md) page.
*   **OnCodeunit\_JobManAssemblyOrderPost\_After\_UpdateHeaderPre** and **OnCodeunit\_JobManAssemblyOrderPost\_Before\_UpdateHeaderPost**
    *   Used when JobManager manipulate lines upon posting af Assembly Order.
*   **OnCodeunit\_JobManNavPost\_DeleteOldQueues**
*   Override how and when the automatic deleting of Job Queue Entries and logs is performed.
*   **OnCodeunit\_JobManRegJobBundleFunctions\_JobListText**
    *   Used to override the color/style for jobs in the [Registration Cockpit](../daily-use/registration-cockpit.md) and [Registration Client](../daily-use/jobmanager-registration-client.md).
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnCodeunit\_JobManPaySpecificationPDFemail\_Addresses**
    *   Override/add mail addresses in [PDF - Specification of Time and Payment (E-Mail)](../payroll-setup/pay-export-type.md).
*   **OnCodeunit\_JobManMobTmpBrickJobManJob\_UpdateFilters**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the lists of JobManager Jobs.
    *   Set extra filters to the list.
*   **OnCodeunit\_JobManMobTmpBrickItemConsump\_ActionQtyAdd\_Before** og **OnCodeunit\_JobManMobTmpBrickItemConsump\_ActionQtyAdd\_After**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the list for Item Consumption.
    *   Insert options in the _#_ menu.
*   **OnCodeunit\_JobManMobTmpBrickItemConsump\_ActionNew**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the list for Item Consumption.
    *   Control the initial pick item page.
*   **OnCodeunit\_JobManMobTmpBrickItem\_InitFilters**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the list for pick/show items.
    *   Apply filters.
    *   Mark items and only show those.
*   **OnCodeunit\_JobManMobTmpBrickItem\_ApplyFilterMyItems**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the list for pick/show items.
    *   Insert items in the _Filter My Items_ list.
*   **OnCodeunit\_JobManMobTmpBrickItem\_ApplyFilterLocationBin**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the list for pick/show items.
    *   Insert items in the _Filter Location/Bin_ list.
*   **OnCodeunit\_JobManMobTmpBrickItem\_ApplyFilterJobLedgerEntry**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the list for pick/show items.
    *   Insert items in the _Filter Job Ledger Entries_ list.
*   **OnCodeunit\_JobManMobTmpBrickItem\_ApplyFilterServideItemComponent**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the list for pick/show items.
    *   Insert items in the _Filter Service Item Components_ list.
*   **OnOnCodeunit\_JobManQuestionnaireRelationMgt\_HandleRelation**
    *   Used upon [auto creation of Answer Collections](../daily-use/jobmanager-questionnaire-relation.md).
    *   Insert additional Answer Collections and/or abort following automatic.
*   **OnOnCodeunit\_JobManQuestionnaireRelationMgt\_HandleRelation\_InsertCheck**
    *   Used upon [auto creation of answercollections](../daily-use/jobmanager-questionnaire-relation.md).
    *   For each Questionnaire set if it should be inserted as Answer Collection..
*   **OnPage\_JobManStampJournalLineListPart\_StyleTextAttention**
    *   Used to override the color/style in the list of registrations upon [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md).
*   **OnPage\_JobManRegLauncher\_LaunchPage**
    *   Use it to override the page called.
*   **OnPage\_JobManRegResource\_UpdateFilter**
    *   Set extra filters in [Registration Cockpit](../daily-use/registration-cockpit.md) and [Registration Client](../daily-use/jobmanager-registration-client.md).
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnPage\_JobManRegResource\_ScanJobNo**
    *   Used when scanning jobs in [Registration Client](../daily-use/jobmanager-registration-client.md).
    *   Can manipulate [Job Id](../general-setup/job-id-2.md) before using the value.
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnPage\_JobManRegSigning\_ScanJobNo**
    *   Used when scanning jobs in [Registration Cockpit](../daily-use/registration-cockpit.md).
    *   Can manipulate [Job Id](../general-setup/job-id-2.md) before using the value.
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
    *   See also _OnPage\_JobManRegSigning\_ScanJobNo\_WithJobLists_ below for function with more parameters and called earlier.
*   **OnPage\_JobManRegSigning\_ScanJobNo\_Before**
    *   Used when scanning jobs in [Registration Cockpit](../daily-use/registration-cockpit.md).
    *   Can manipulate [Job Id](../general-setup/job-id-2.md) before using the value.
    *   Can further manipulate with the filters on the Job Lists
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnPage\_JobManRegSigning\_JobList\_OnDrillDown\_Before**
    *   Called when an Employee is selecting the stack, which calls the _Job List_ sub-pages in the [Registration Cockpit](../daily-use/registration-cockpit.md) page.
    *   Executed _before_ the sub-pages is opened.
*   **OnPage\_JobManRegSigning\_JobList\_OnDrillDown\_After**
    *   Called when an Employee is selecting the stack, which calls the _Job List_ sub-pages in the [Registration Cockpit](../daily-use/registration-cockpit.md) page.
    *   Executed _after_ the sub-pages is closed.
*   **OnPage\_JobManRegSigning\_ActiveJobs\_OnDrillDown\_Before**
    *   Called when an Employee is selecting the stack, which calls the _Active Jobs_ sub-pages in the [Registration Cockpit](../daily-use/registration-cockpit.md) page.
    *   Executed _before_ the sub-pages is opened.
*   **OnPage\_JobManRegSigning\_ActiveJobs\_OnDrillDown\_After**
    *   Called when an Employee is selecting the stack, which calls the _Active Jobs_ sub-pages in the [Registration Cockpit](../daily-use/registration-cockpit.md) page.
    *   Executed _after_ the sub-pages is closed.
*   **OnPage\_JobManRegJobList\_ScanJobNo**
    *   Used when scanning jobs in the _Job List_ sub-pages in the [Registration Cockpit](../daily-use/registration-cockpit.md) page.
    *   Can manipulate [Job Id](../general-setup/job-id-2.md) before using the value.
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnPage\_JobManRegJournal\_OnCommitDay**
    *   Used when calling _Commit_ in [Time Sheet](../daily-use/jobmanager-time-sheet.md).
    *   Can be used to validate content of the day.
*   **OnPage\_JobManRegWeek\_EmployeeChanged**
    *   Used in [Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md) when Employee is changed. Use for extra checks and/or chage the starting day to view.
*   **OnPage\_JobManRegWeekMatrix\_FindOrInsertSignIn** and **OnPage\_JobManRegWeekMatrix\_FindOrInsertSignOut**
    *   Used in [Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md) to control the auto inserted Clock-In/-Out registratios.
*   **OnPage\_JobManRegPickJob\_UpdateFilter**
    *   Apply extra filters on the _Select Job_ page.
*   **OnPage\_JobManWorkTypePick\_ApplyFilter**
    *   Apply extra filers when selecting _Work Type_.
*   **OnPage\_JobManPreApproveJournalLine\_EditLine**
    *   Used to override the action on _Edit_ in [Pre-Approval](../other-features/pre-approval.md).
*   **OnPage\_JobManMobRegSigning\_ScanJobNo**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the page _Registration_.
    *   Used when scanning jobs.
    *   Can manipulate [Job Id](../general-setup/job-id-2.md) before using the value.
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnPage\_JobManMobRegSigning\_JobList\_UpdateFilter**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the page _Registration_.
    *   Benyttes til at sætte ekstra filtre på joblisterne.
    *   Se `Codeunit 60002 JobManDemoFuncJobProduction` for eksempel på hvordan der opnås tilgang til `JobManJobBundle`.
    *   Set extra filters for the lists of jobs.
    *   See `Codeunit 60002 JobManDemoFuncJobProduction` for how to get access to `JobManJobBundle`.
*   **OnPage\_JobManMobRegSigning\_JobList\_OnDrillDown\_Before**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the page _Registration_.
    *   Called when an Employee is selecting the stack, which calls the _Job List_ sub-pages.
    *   Executed _before_ the sub-pages is opened.
*   **OnPage\_JobManMobRegSigning\_JobList\_OnDrillDown\_After**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the page _Registration_.
    *   Called when an Employee is selecting the stack, which calls the _Job List_ sub-pages.
    *   Executed _after_ the sub-pages is closed.
*   **OnPage\_JobManMobRegSigning\_ActiveJobs\_OnDrillDown\_Before**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the page _Registration_.
    *   Called when an Employee is selecting the stack, which calls the _Active Jobs_ sub-pages.
    *   Executed _before_ the sub-pages is opened.
*   **OnPage\_JobManMobRegSigning\_ActiveJobs\_OnDrillDown\_After**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the page _Registration_.
    *   Called when an Employee is selecting the stack, which calls the _Active Jobs_ sub-pages.
    *   Executed _after_ the sub-pages is closed.
*   **OnPage\_JobManMobHistory\_UpdateSum**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) within the _History_ page.
    *   Can manipulate the totals shown in the page.
*   **OnTable\_JobManEmployee\_StatusText**
    *   Override the _status_ (text), which could be shown in the JobManager Emplyee List.
*   **OnTable\_JobManEmployee\_GetAbsenceRequired**
    *   Override if absence should be requirede when employee is Clocking-in/-out.
*   **OnTable\_JobManEmployee\_GetTriggerRequired**
    *   Override if trigger should be requirede when employee is Clocking-in/-out.
*   **OnTable\_JobManEmployee\_GetFilter\_ResourceGroup\_Resource**
    *   Used to override [these filters](../general-setup/filter-option.md).
*   **OnTable\_JobManEmployee\_GetFilter\_WorkCenter\_MachineCenter**
    *   Used to override [these filters](../general-setup/filter-option.md).
*   **OnTable\_JobManEmployee\_GetFilter\_Category\_Activity**
    *   Used to override [these filters](../general-setup/filter-option.md).
*   **OnTable\_JobManEmployeeGroup\_GetFilter\_ResponsibleUserID**
    *   Used to override which [Calculation Groups](./calculate-group.md) or [Approval Groups](./calculate-group.md) the User is responsible for.
*   **OnTable\_JobManEmployeeGroup\_GetFilter\_LimitUserID**
    *   Used to override which [Calculation Groups](./calculate-group.md) or [Approval Groups](./calculate-group.md) the User is restricted to see.
*   **OnTable\_JobManEmployee\_TwoFactorCodeInit**
    *   Used to override generate the code for [2FA (Two-factor authentication)](../other-setup/2fa-two-factor-authentication.md).
*   **OnTable\_JobManEmployee\_TwoFactorCodeSend**
    *   Used to override sending the code for [2FA (Two-factor authentication)](../other-setup/2fa-two-factor-authentication.md).
*   **OnTable\_JobManEmployee\_TwoFactorCodeCheck**
    *   Used to override validate the code for [2FA (Two-factor authentication)](../other-setup/2fa-two-factor-authentication.md).
*   **OnTable\_JobManPreApprove\_StampJournalLineApprover**
    *   Used to override the Pre-Approver for a Stamp Journal Line.
*   **OnTable\_JobManCustomField\_GetFieldCaption**
    *   Used to create very special captions for fields in [Custom fields](./code-hooks.md).
*   **OnTable\_JobManAgreementLine\_SkipRec**
    *   Used for extra possibility to _skip_ lines from [Agreement Setup](../all-tables/agreement-setup.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckWeekday**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckSeniority**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckQualification**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckRateType**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckWorkTypeCode**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckSubConditions**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckJobNo**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManAgreementCounter\_CheckCommon**
    *   Used for extra limitations of [Time Counters](../jobmanager-calculations/time-counters.md) when calculating [Agreement Pay Counters](../all-tables/agreement-pay-counters.md) in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManPayTypeRate\_GetRate**
    *   Used for override [Pay Type Rate](../all-tables/pay-type-rate.md) eg. in connection with [Create Pay Transactions](../daily-use/create-pay-transactions.md).
*   **OnTable\_JobManPayEntry\_ExternalDimension20**
    *   Used for finding dimensions for [Pay Events](../all-tables/pay-events.md).
    *   Used within some [Pay Export Types](../payroll-setup/pay-export-type.md) eg. [365Løn](../all-articles/pay-export-to-365l-n.md).
*   **OnTable\_JobManStampHeader\_InsertProfileDateRecords**
    *   Used when initiating records in [Employee Stamp Sum](../all-tables/employee-stamp-sum.md) for use in [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md).
    *   Used to override the color/style in the list of employees upon [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md).
*   **OnTable\_JobManStampHeader\_FirstErrorStyleText**
    *   Used to override the color/style in pages [Registration approval](../daily-use/registration-approval.md) and [Time Calculation and Approval](../all-pages/time-calculation-and-approval.md).
*   **OnTable\_JobManStampJournalLine\_StopJob**
    *   Used for validation when stop time registration of a job in [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md).
*   **OnTable\_JobManStampJournalLine\_OnSumActualTimeForPosting**
    *   Used to manipulate the _Time Comsump_ that is inserted in [Stamp Events](../all-tables/stamp-events.md) for later [posting](../daily-use/post-to-nav-bc.md).
*   **OnTable\_JobManStampMileage\_SetDefaultVehicleId**
    *   Used to set default value for _License Plate (VehicleId)_ upon [mileage registration](../all-tables/mileage.md).
*   **OnTable\_JobManBlobStorage\_ViewFile**
    *   Used when files from _JobManager Attachment_ is opened.
*   **OnTable\_JobManBlobStorage\_ReplaceText**
    *   Used when using _variables_ in texts for _JobManager Attachment_.
*   **OnTable\_JobManTmpWeekJournal\_OnWeekJournalInsertJobs**
    *   Used to add/override default lines in the [JobManager Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md) page.
*   **OnTable\_JobManTmpWeekJournal\_OnValidate\_Favorite**
    *   Used to handle changes of _Favorite_ value in the [JobManager Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md) page.
*   **OnTable\_JobManTmpWeekJournal\_CellData**
    *   Used to change the value for a cell in the [JobManager Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md) page.
*   **OnTable\_JobManTmpWeekJournal\_CellClick**
    *   Used to override _OnDrillDown_ for a cell in the [JobManager Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md) page.
*   **OnTable\_JobManTmpWeekJournal\_CellStyle**
    *   Used to override _StyleExpr_ for a cell in the [JobManager Time Sheet (Week)](../daily-use/jobmanager-time-sheet-week.md) page.
*   **OnTable\_JobManTmpMessageRecipient\_FillTableLimited**
    *   Used to insert extra possible recipients for new [Messages](../all-pages/message.md) from within the job registration pages.
*   **OnTable\_JobManTmpMessageRecipient\_FillTableFull**
    *   Used to insert extra possible recipients for new [Messages](../all-pages/message.md) from within the _Messages_ Cue Indicator.
*   **OnTable\_JobManMobTmpBrick\_AddFromRecRef\_SpecialFunction**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) for setup [Mobile Pages](../all-tables/mobile-pages.md).
    *   With this _virtual_ fields can be inserted, whose value comes from a customized _function_.
*   **OnTable\_JobManMobTmpBrick\_AddFromRecRef\_DoAdd**
    *   Used in [JobManager Mobile](../daily-use/mobile-role-center.md) for setup [Mobile Pages](../all-tables/mobile-pages.md).
    *   Can limit which records end up being inserted into the lists.
    *   Works both with and without search.
*   **OnTable\_JobManCue\_DrilldownMissingCalculate**
    *   Used on _drilldown_ for _Calculation missing_ on JobManager Role Centers.
    *   Can change filters for the page to open.
    *   Can change _which_ page to open.
    *   Can entire change the _drilldown_ behavior.
*   **OnTable\_JobManCue\_DrilldownMissingApprove**
    *   Used on _drilldown_ for _Approvement missing_ on JobManager Role Centers.
    *   Can change filters for the page to open.
    *   Can change _which_ page to open.
    *   Can entire change the _drilldown_ behavior.
*   **OnTable\_JobManQuestionnaire\_CreateAnswerCollection**
    *   Called immediately after the creation of a [JobManager Answer Collection](../daily-use/jobmanager-answer-collection.md) and its questions.
*   **OnTable\_JobManAnswerCollection\_InitFromStampJournalLine**
    *   Called immediately after creating each [Question](../all-tables/jobmanager-answer-collection-line.md) for a [JobManager Answer Collection](../daily-use/jobmanager-answer-collection.md). _If created from a [Stamp Journal Line](../all-tables/stamp-journal-lines-2.md)._
*   **OnTable\_JobManAnswerCollection\_InitFromJobManJob**
    *   Called immediately after creating each [Question](../all-tables/jobmanager-answer-collection-line.md) for a [JobManager Answer Collection](../daily-use/jobmanager-answer-collection.md). _If created from a [JobManager Job](../general-setup/jobmanager-job.md)._
*   **OnTable\_JobManAnswerCollection\_CallReportWithPick\_Mark**
    *   Called upon select report for printing. Use this to add reports to the pick list.
*   **OnTable\_JobManAnswerCollectionLine\_ReplaceText**
    *   Used to insert variables into Questions if these go beyond the [default options](../all-articles/questionnaire-variables.md).
*   **OnTable\_JobManAnswerCollectionLine\_ValidationHint**
    *   Used to override the _hint_ upon answering a [Question](../all-tables/jobmanager-answer-collection-line.md).
*   **OnTable\_JobManAnswerCollectionLine\_ValidateAnswerErrorText**
    *   Used to override the [Question](../all-tables/jobmanager-answer-collection-line.md) validation.
*   **OnTable\_JobManAnswerCollectionLine\_ValidateAnswerErrorTextPictureRequired**
    *   Used to override the [Picture Required](T_6183023_41.htm) validation on the [Question](../all-tables/jobmanager-answer-collection-line.md).
*   **OnXML\_JobManWS\_Item\_OnBeforePassVariable\_Description**
    *   Override the Item Description when selecting new items for item consumption from [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **OnXML\_JobManWS\_ItemConsumption\_OnAfterGetRecord**
    *   Override the Item Description shown in the list of existing item consumption in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **OnXML\_JobManWS\_JobManStampJournalLin\_OnAfterGetRecord**
    *   Override Posting Description for existing lines in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **OnXML\_JobManWS\_AttachmentList\_DisplayText**
    *   Used by [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **OnXML\_ExpPay\_ExternalPayrollNo**
    *   Used for override _External Payroll number_ in relevant pay exports.
*   **OnXML\_ExpPay\_ExternalPayrollSubNo**
    *   Used for override _External Payroll subnumber_ in relevant pay exports.
*   **WS\_AboutText**
    *   Manipulate the About (debug) text for the APP.
*   **WS\_UploadLinkPath**
    *   Used to manipulate Path in connection with uploading images from [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_UploadLinkFilename**
    *   Used to manipulate Filename in connection with uploading images from [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetListWorkCenter**
    *   Used for manipulating filters for selecting Work Center in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetListMachineCenter**
    *   Used for manipulating filters for selecting Machine Center in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetListResourceGroup**
    *   Used for manipulating filters for selecting Resource Group in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetListResource**
    *   Used for manipulating filters for selecting Resource in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetListWorkType**
    *   Used for manipulating filters for selecting Work Type in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetListJobManAddon**
    *   Used for manipulating filters for selecting Registration add-on in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetJobList**
    *   Used for manipulating filters for selecting JobManager Jobs in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetItem**
    *   Used for manipulating filters for selecting Items for item consumption in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetItemVariant**
    *   Used for manipulating filters for selecting Variants for item consumption in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetLocation**
    *   Used for manipulating filters for selecting Location for item consumption in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_GetBin**
    *   Used for manipulating filters for selecting Bin for item consumption in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_RegInsert**
    *   Used for manipulation values before insert from Time Sheet in [Mobile registration Client App](../mobile-registration-client-app/README.md).  
        
*   **WS\_RegModify**
    *   Used for manipulation values before modify from Time Sheet in [Mobile registration Client App](../mobile-registration-client-app/README.md).
*   **WS\_RegDelete**
    *   Used for manipulation values before delete from Time Sheet in [Mobile registration Client App](../mobile-registration-client-app/README.md).

**Partners can contact _support@jobmanager.dk_ if there are suggestions for new events.**

## See also

[API (Registration)](./api-registration.md)
