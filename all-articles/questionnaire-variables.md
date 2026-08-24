# Questionnaire Variables

By entering `[[ ]]` in the field, a value from a related table can be inserted.

Syntex is `[[Table Number, Field Number]]`.

Eg. `[[18,9]]` indicates table **18** (Customer) and field **9** (Phone No.).

Below is a table of possible tables in different scenarios.

| Table Number | Tablename | Active for Ref.Type | Answered via JobManager Job | Answered via Stamp Journal Line |
| :-: | :-- | :-: | :-: | :-: |
| 6182601 | JobManager job | All | X | X |
| 6182623 | Stamp Journal Line | All |  | X |
| 5405 | Production Order | Production | X | X |
| 5406 | Prod.ordrelinje | Production | X | X |
| 5409 | Prod. Order Routing Line | Production | X | X |
| 167 | Job | Job | X | X |
| 1001 | Job Task | Job | X | X |
| 1003 | Job Planning Line | Job | X | X |
| 5900 | Service Header | Service | X | X |
| 5901 | Service Item Line | Service | X | X |
| 5902 | Service Line | Service | X | X |
| 5940 | Service Item | Service | X _(from 01.27)_ | X _(from 01.27)_ |
| 900 | Assembly Header | Assembly | X _(from 01.28)_ | X _(from 01.28)_ |
| 901 | Assembly Line | Assembly | X _(from 01.28)_ | X _(from 01.28)_ |
| 18 | Customer | Job, Service | X | X |
| 27 | Item | Production, Service, Assembly | X | X |
| 99000754 | Work Center | Production | X _(from 01.30)_ | X _(from 01.30)_ |
| 99000758 | Machine Center | Production | X _(from 01.30)_ | X _(from 01.30)_ |
| 152 | Resource Group | Job, Service, Assembly | X _(from 01.30)_ | X _(from 01.30)_ |
| 156 | Resource | Job, Service, Assembly | X _(from 01.30)_ | X _(from 01.30)_ |
| 5200 | Employee | All |  | X |
| 6182311 | JobManager Employee | All |  | X |
| 7500 (X) | Item Attribute (X) | All | X | X |

**(X) Item Attribute**

*   Supported from NAV 2017 and later
*   _Field Number_ is replaced with the name of the attribute. Eg. `[[7500,Depth]]` or `[[7500,Description of equipment]]`

## See also

[Questionnaire](../daily-use/questionnaire.md)  
[Questionnaire Variables](./questionnaire-variables.md)
