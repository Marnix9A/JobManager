# Posting Description Item (Production)

Use this to write a formula for the value of _Post Description_ when [posting](../daily-use/post-to-nav-bc.md). A formula could be set for both _Time_ Consumption and _Item_ Consumption.

By entering `[[ ]]` in the field, a value from a related table can be inserted.

Syntex is `[[Table Number, Field Number]]`.

Eg. `[[18,9]]` indicates table **18** (Customer) and field **9** (Phone No.).

Any number of tables/fields can be set `[[167,1]] - [[18,9]]`.

Beside the tables below, the tables from [this help page](./description-production.md) can be used as well.

| Tabelnummer | Tabelnavn | Bemærkning |
| :-: | :-: | :-: |
| 6182629 | Stamp Event |  |
| 6182623 | Stamp Journal Lines |  |
| 6182601 | JobManager Job |  |
| 6182311 | JobManager Employee |  |
| 5200 | Employee |  |
| 27 | Item | Only for _Item_ consumption |
| 5401 | Vare Variant | Only for _Item_ consumption |

By using the char `#` as **only** value in the field, JobManager \*\*adds\* `JM#1234` at the end of the standard _Posting Description_. Where `1234` would be the _Sequence_ from the _Stamp Journal Line_.  

## See also

[Post to NAV/BC](../daily-use/post-to-nav-bc.md)
