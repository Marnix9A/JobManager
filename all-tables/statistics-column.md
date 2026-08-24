# Statistics Column

In _Statistic Column_ it is able to make "your own" Columns, which can be used for e.g. [Registration Approval](T_6182765.htm), _Time and Payment Specifications_, _Registration Cockpit - Statistic_ etc.

(from version 01.40, it is possible to export/import the whole setup (all related tables) and formulas for Statistics Column)

The Column can be setup for these functions:

| Function ID | Description | Function |
| :-- | :-- | :-- |
| BreakGrossTime \* | Break (Gross Time) | Gross Time between Breakstart and BreakStop |
| BreakTimePeriods \* | Break (Time Periods) | Shows Break Periods |
| Clock-inClock-outGrossTime \* | Clock-in & Clock-out (Gross Time | Gross Time between Clock-in and Clock-out |
| Clock-inClock-out Time Periods_|Clock-in & Clock (Time Periods)|Shows Clock-in and Clock-out Periods | |Date |Date |Date, weekday, weeknumber etc. | |Fieldvalue |Fieldvalue |Show selected field(s) from related tables. | |List - Work type |Work type List |Shows a "list" of work types used that day | |List - Absence |Absence List |Shows a "list" of the absence that day or period| |List - Assembly |Assembly List |Shows a "list" of assembly orders the employee has been working on| |List - IPCActivity |IPC Activity List |Shows a "list" of IPC activity the employee has been working on| |List - Job |Job List |Shows a "list" of Jobs(Projects) the employee has been working on| |List - Mileage |Mileage List |Shows a total amount of Miles or KM. e.g. "15 Miles" | |List - Production |Production List |Shows a "list" of Production order the employee has been working on. | |List - RegistrationAdd-on |Registration add-on List |Shows a "list" of used Add-ons. | |List - Service |Service List |Shows a "list" of Serviceordres the employee has been working on. | |List - Trigger |Job List |Shows a "list" of Jobs (Projects) the employee has been working on| |Paytype |Formula Pay Type |Shows the results of the **formula** |Sum-Hours |Sum Hours (Time Sheet) |Shows a total amount of registered_ hours\* in the Timesheet. |
| TimeCounter | Formula Time Counters | Shows the results of the **formula** |

## Formula

\*It is not possible to make a formula of this function.

**Date**  
The _date_ can be shown in different ways (Date, weekday, weeknumber etc.)  
A formula kan e.g. contain: `U<Week> <Weekday Text>`  
Read more [here](https://learn.microsoft.com/en-us/dynamics-nav/format-property).

**Fieldvalue**  
Select field(s) from _Employee Stamp Sum_ and/or related tables. Sample for showing _Resource No._ from the _Employee_ table use the formula: `[[5200,38]]`. More fields can be added to same formula: `[[156,2]] - [[152,2]]`.  
Fields from the following table are supported:

*   [JobManager Stamp Sum](./employee-stamp-sum.md).
*   JobManager Employee
*   Employee
*   Resource
*   Resource Group

**List Absence, IPC and Trigger**  
You can use: \* |  
With _IPC List_ it deselects [Triggers](T6182441_20.htm) and _Absence_  
With _Trigger List_ it deselects _"General" IPC_ and _Absence_.

**List Mileage**  
If you only use _Miles_ then the formula can be empty. It you create "Bridge" or others, then a filter can be used.

**List Assembly, Production/Jobs(Project)/Service**  
Can filter on ordernumber.  
You can use: \* |

**List Registration Add-on**  
Can filter on Add-ons.  
You can use: \* |

**Paytype**  
\[ \] = Per. day  
{ } = Period (The Period can be specified on the _Paytype_ - [Statistics Period](T_6182551_35.htm))  
E.g. \[Paytype\_X\] + \[Paytype\_Y\]  
E.g. {Paytype} el. {Paytype\_X} + {Paytype\_Y}  
Find more inspiration for formula [her](./condition.md)

**Time Counter**  
\[ \] = Per. day  
{ } = Period (On the _TimeCounter_)  
E.g. \[TimeCounter\_X\] + \[TimeCounter\_Y\]  
E.g. {TimeCounter} el. {TimeCounter\_X} + {TimeCounter\_Y}  
Find more inspiration for formula [her](./condition.md)

## Condition - Style

There can be created several conditions, which can change [Style](./style.md) depending on the condition setup.  
There are 3 opportunities for Conditions.

**Clock-in/Clock-out & Break Periods** This is compared with the number of _zones_.  
E.g. ">2" can be coloured if the employee has clock-in/Clock-out multiple times.

**Jobs (IPC, Absence, Prod. Jobs (Project) etc.)**  
This is compared with the _amount_ on the list  
E.g. ">2" can be coloured if the employee more that 2 _lines_.

**TimeCounter**  
It is possible to use multiple Time Counters. It is also Possible to use an other Time Counter, then the one in the _formula_ to be coloured.

E.g. If you want multiple "warnings", if the employee has more then X amount of hours in overtime.:

Formula: \[Weekly hours\]  
Condition - Style 1: > 11,5 - Colour 1  
Condition - Style 2: > 9,5 - Colour 2  
Condition - Style 3: > 7,5 - Colour 3  
The largest condition must be first, as "the search" stops when the condition has "met".

An other example is:  
If you want a "warning" if the employee hasn't achieved hers/his std. hours.  
The setup can be like this:

Formula: \[Weekly hours\]  
Condition - Style 1: => 7,5 - Colour i green  
Condition - Style 2: < 7,5 - Colour is red  

_The Pages and reports with Statistics is from version 01.41 now able to show totals. This is to be activated on each column setup_

[Column ID](./column-id.md)  
[Description](./description-2.md)  
[Caption](./caption.md)  
[Function ID](./function-id.md)  
[Show zero](./show-zero.md)  
[Rounding Precision](./rounding-precision.md)  
[Round type](./round-type.md)  
[h:min](./h-min.md)  
[Show Totals](./show-totals.md)  
[Exists](./exists.md)  
[NOT found](./not-found.md)  
[Report Alignment](./report-alignment.md)  
[Presentation Unit of Measure](./presentation-unit-of-measure.md)  
[Style1](./style1.md)  
[Style2](./style2.md)  
[Style3](./style3.md)  

## See also

[Registration approval](../daily-use/registration-approval.md)
