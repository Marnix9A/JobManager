# Description (Production)

Use this to write a formula for the _Description_ field on [JobManager Jobs](./jobmanager-job.md). By entering `[[ ]]` in the field, a value from a related table can be inserted.

Syntex is `[[Table Number, Field Number]]`.

Eg. `[[18,9]]` indicates table **18** (Customer) and field **9** (Phone No.).

Any number of tables/fields can be set `[[167,1]] - [[18,9]]`.

Below is a table of possible tables in different scenarios.

| Table Number | Tablename | Active for Ref.Type |
| :-: | :-: | :-: |
| 6182601 | JobManager job | All |
| 5405 | Production Order | Production |
| 5406 | Prod.ordrelinje | Production |
| 5409 | Prod. Order Routing Line | Production |
| 167 | Job | Job |
| 1001 | Job Task | Job |
| 1003 | Job Planning Line | Job |
| 5900 | Service Header | Service |
| 5901 | Service Item Line | Service |
| 5902 | Service Line | Service |
| 5940 | Service Item | Service |
| 900 | Assembly Header | Assembly |
| 901 | Assembly Line | Assembly |
| 18 | Customer | Job, Service |
| 27 | Item | Production, Service, Assembly |
| 5401 | Item Variant | Production |
| 99000754 | Work Center | Production |
| 99000758 | Machine Center | Production |
| 152 | Resource Group | Job, Service, Assembly |
| 156 | Resource | Job, Service, Assembly |
| 7500 (X) | Item Attribute (X) | All |

**(X) Item Attribute**

*   Supported from NAV 2017 and later
*   _Field Number_ is replaced with the name of the attribute. Eg. `[[7500,Depth]]` or `[[7500,Description of equipment]]`

**Note:** Upon update related/used fields the _Description_ field is **NOT** updated (due to performance). Use the Update jobs - either manual or writing a couple of lines of code using:: _Report.JobManJobUpdate.InsertUpdateIpcActivity, InsertUpdateProdOrderRoutingLine, InsertUpdateJobPlanningLine, InsertUpdateServiceItemLine, InsertUpdateServiceOrderAllocation eller InsertUpdateAssemblyLine_.
