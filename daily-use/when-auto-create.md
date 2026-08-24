# When (Auto Create)

An empty _Answer Collection_ for this _Questionnaire_ can be created automatically, so that it is ready for answering.

Also note the field [Mandatory Answer](./mandatory-answering.md), which can force you to answer this.

The two fields **When (Auto Create)** and **Where (Auto Create)** have an influence on this:

| When | Where = Job | Where = Registration |
| :-- | :-: | :-: |
| Create Job | Creates empty _Answer Collection_ related to the _JobManager Job_ when a _JobManager Job_ is created. | n/a |
| Create Registration | Creates an empty _Answer Collection_ related to the _JobManager Job_ when there is a registration on the job. | Creates an empty _Answer Collection_ related to the _JobManager Stamp Journal Line_ when there is a registration on the job. |
| Reporting Good | Creates an empty _Answer Collection_ related to the _JobManager Jobs_ when _Qty Good_ is reported. | Creates an empty _Answer Collection_ related to the _JobManager Stamp Journal Line_ when _Qty Qood_ is reported. |
| Reporting Scrap | Creates an empty _Answer Collection_ related to the _JobManager Job_ when _Qty Scrap_ is reported. | Creates an empty _Answer Collection_ related to the _JobManager Stamp Journal Line_ when _Qty Scrap_ is reported. |

Note that the column _Where = Registration_ is only intended for _stamping_ (that is JobManager Time Sheets excepted).

Create can be limited with the field [Only once (Auto Create)](./once-only-auto-create.md).

For productions, also limit with the fields [Production Setup Time (Auto Create)](./production-setup-time-auto-create.md), [Production Run Time (Auto Create)](./production-run-time-auto-create.md), [Production Wait Time (Auto Create)](./production-wait-time-auto-create.md) and [Production Move time (Auto Create)](./production-move-time-auto-create.md).

## See also

[Registration Cockpit](../all-pages/registration-cockpit.md)
