# Sort Order

This field indicates whether the lines in the file should be summed, and at what level.

One or more fields can be specified, separated by `,` (comma). The fields are specified with their BC/NAV system name _(overview at the bottom of this help)_.

### Example 1 (daily summation per Pay Type)

ExpEmployeeNo,Date,ExpPayTypeNo

The summation is per Employee, per Date and per Pay Type.

Rate is the average of the summation. For example `2025-12-19` where there are `6` hours with different rates. The total amount is `1000`, which is why the rate is `1000 / 6` = `166.67`

###### Pay Events

| Employee | Date | Pay Type | Qty | Rate | Amount | |---|---|---|---|---|---| | AH | 2025-12-19 | 1234 | 3 | 100 | 300 | | AH | 2025-12-19 | 1234 | 1 | 100 | 100 | | AH | 2025-12-19 | 1234 | 2 | 300 | 600 | | AH | 2025-12-20 | 1234 | 8 | 100 | 800 | ##### Result | Employee | Date | Pay Type | Qty | Rate | Amount | |---|---|---|---|---| | AH | 2025-12-19 | 1234 | 6 | 166.67 | 1000 | | AH | 2025-12-20 | 1234 | 8 | 100 | 800 |

### Example 2 (daily summation per wage type and multiple lines if different rate)

ExpEmployeeNo,Date,ExpPayTypeNo,Rate

The summation per employee, per date, per wage type and per rate

Therefore, there will be 2 lines for `2025-12-19` on wage type `1234`.

##### Pay Events

| Employee | Date | Pay Type | Qty | Rate | Amount | |---|---|---|---|---|---| | AH | 2025-12-19 | 1234 | 3 | 100 | 300 | | AH | 2025-12-19 | 1234 | 1 | 100 | 100 | | AH | 2025-12-19 | 1234 | 2 | 300 | 600 | | AH | 2025-12-20 | 1234 | 8 | 100 | 800 | ##### Result | Employee | Date | Pay Type | Qty | Rate | Amount | |---|---|---|---|---|---| | AH | 2025-12-19 | 1234 | 4 | 100 | 400 | | AH | 2025-12-19 | 1234 | 2 | 300 | 600 | | AH | 2025-12-20 | 1234 | 8 | 100 | 800 |

### Example 3 (summation for the entire pay period per pay type)

ExpEmployeeNo,ExpPayTypeNo

The summation per employee and per pay type.

Therefore, there will only be one line for `2025-12-19` (first date) on pay type `1234`.

Rate will be the average of the summation. The amount is the sum of `1800` and `14` hours, so the rate will be `1800 / 14` = `128.57`

#### Pay Events

| Employee | Date | Pay Type | Qty | Rate | Amount | |---|---|---|---|---| | AH | 2025-12-19 | 1234 | 3 | 100 | 300 | | AH | 2025-12-19 | 1234 | 1 | 100 | 100 | | AH | 2025-12-19 | 1234 | 2 | 300 | 600 | | AH | 2025-12-20 | 1234 | 8 | 100 | 800 | ##### Result | Employee | Date | Pay Type | Qty | Rate | Amount | |---|---|---|---|---| | AH | 2025-12-19 | 1234 | 14 | 128.57 | 1400 |

### Field overview

*   `Date` for _Date_
*   `ExpEmployeeNo` for _Employee External No._
*   `OrgEmployeeNo` for _Employee_
*   `ExpPayTypeNo` for _Pay Type External No._
*   `OrgPayTypeNo` for _Pay Type_
*   `Qty` for _Qty_
*   `Rate` for _Rate_
*   `Amount` for _Amount_
*   `ExternalType` for _External Type_
*   `ExternalUnit` for _External Unit_
*   `Dim01`..`Dim20` for dimension fields 1 to 20
