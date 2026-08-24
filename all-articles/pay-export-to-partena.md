# Pay Export to Partena

Below is special information for this export format. General information is available [here](../daily-use/export-payroll.md).

The field _CustomerFile_ is retrieved from the field [External Payroll number](../general-setup/external-payroll-number.md) in the [JobManager Setup](../general-setup/jobmanager-setup.md) table.

The field _Prestatype_ is always `D`.

### Summation

A runtime parameter indicates whether this file should sum the lines for the entire selected period, if they have the same _Pay Type_ and _Rate_.

### File format

*   The file contains the following fields: `CustomerFile, WorkerNo, Daydate, Prestatype, Code, Minutes_day`
*   _Minutes\_day_ field are specified as minutes length 5 (00000).
*   Dates are specified as \`DD-MM-YYYY'.

### Advanced setup

```
 STANDARD,QTY
 A0050_1, 
```

#### Explanation

*   `STANDARDS,QTY` All Pay Types are exported with _Minuts\_day_.
*   `D5152,` The Pay Type _D5152_ are exported **without** _Minuts\_day_.

## See also

[Export Payroll](../daily-use/export-payroll.md)
