# Pay Export to Huldt & Lillevik

Below is special information for the norwegian payroll system Huldt & Lillevik. General information is available [here](../daily-use/export-payroll.md).

### Summation

This file should sum the lines for the entire selected period, if they have the same _Pay Type_ and _Rate_.

### File format

*   The file contains the following fields: `Employee, Paycode, Quantity, UnitPrice, TotalValue`
*   Decimal fields are specified _without_ a thousand separator, with 2 decimal places and with _comma_ as decimal point.

### Advanced setup

```
STANDARD,QUANTITY,UNITPRICE,TOTALVALUE
D5132,QUANTITY,UNITPRICE
```

#### Explanation

*   `STANDARD,QUANTITY,UNITPRICE,TOTALVALUE` All Pay Types are exported with both Quantity, UnitPrice and TotalValue.
*   `D5152,` The Pay Type _D5152_ are exported only the Quantity and UnitPrice fields.

## See also

[Export Payroll](../daily-use/export-payroll.md)
