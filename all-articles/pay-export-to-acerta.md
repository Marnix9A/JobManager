# Pay Export to Acerta

This is for the Belgian Payroll System _Acerta_ and the _Acerta Connect_ file.

This export consists of 2 files, which are created separately:

*   Payroll (and Absence)
*   Addon

Below is special information for this export format. General information is available [here](../daily-use/export-payroll.md).

**The _Advanced_ field is _EMPTY_ for these exports!**

The field _External Payroll No_ is retrieved from the field [External Payroll number](../general-setup/external-payroll-number.md) in the [JobManager Setup](../general-setup/jobmanager-setup.md) table.

#### Payroll (and Absence) file

This file includes lines where [External Type](../all-tables/external-type.md) equals _Pay_ and _Absence_.

The field _Line Prefix_ is always `KLX1` (that is fixed value `KLX` followed by `1` for _Update Code_ equals _Active_)

#### Addon file

This file includes lines where [External Type](../all-tables/external-type.md) equals _Addon_.

The field _Line Prefix_ is always `LOMD` (that is fixed value `LOM` followed by `D` (equals _origineel: gegeven wordt toegevoegd bij al dan niet aanwezige lijnen in de afwijkende lonen_).

The fields _Afwerkingsdatum_, _Kostenplaats_ and _Uitbetalingspercentage_ is always empty.

Only one of the fields _Days_ or _Qty_ is used for each row. The _Days_ field is used if [External Unit](../all-tables/external-unit.md) equals _Days_, otherwise the _Qty_ field is used.

### Summation

A runtime parameter indicates whether this file should sum the lines for the entire selected period, if they have the same _Pay Type_ and _Rate_.

If summation, the date on the lines will be set to the first day of the selected period.

### File format

*   The **Payroll file** contains the following fields: `Line Prefix, External Payroll No, Export Empl No, Date, Export Pay Type No, Qty`
    *   `Line Prefix` 4 characters (left-aligned) at position 1-4
    *   `External Payroll No` 7 characters (left-aligned) at position 5-11
    *   `Export Empl No` 20 (17+3) characters (left-aligned) at position 12-31
    *   `Date` 10 characters at position 32-41
    *   `Export Pay Type No` 6 (2+4) characters (right-aligned with leading spaces) at position 42-47
    *   `Qty` 6 (2+4) characters (right-aligned with **2** leading spaces) at position 48-53  
          
        
*   The **Addon file** contains the following fields: `Line Prefix, External Payroll No, Export Empl No, Date, Afwerkingsdatum, Kostenplaats, Export Pay Type No, Days, Qty, Rate, Uitbetalingspercentage, Amount`
    *   `Line Prefix` 4 characters (left-aligned) at position 1-4
    *   `External Payroll No` 7 characters (left-aligned) at position 5-11
    *   `Export Empl No` 20 (17+3) characters (left-aligned) at position 12-31
    *   `Date` 10 characters at position 32-41
    *   `Afwerkingsdatum` 10 characters at position 42-51
    *   `Kostenplaats` 12 characters at position 22-63
    *   `Export Pay Type No` 6 (2+4) characters (right-aligned with leading spaces) at position 64-69
    *   `Days` 8 (2+6) characters (right-aligned with **2** leading spaces) at position 70-77
    *   `Qty` 8 (2+6) characters (right-aligned with **2** leading spaces) at position 78-85
    *   `Rate` 15 (2+13) characters (right-aligned with **2** leading spaces) at position 86-100
    *   `Uitbetalingspercentage` 5 characters at position 101-105
    *   `Amout` 11 (2+13) characters (right-aligned with **2** leading spaces) at position 106-116  
          
        
*   Decimal fields are specified _without_ a thousand separator, with 2 decimal places (exept 5 for _Rate_ field) and _without a decimal point_. That is 12.34 would be `1234` _(with a maximum of 4 digits)_. The number has leading `0` (zeros).
*   Dates are specified as \`DD/MM/YYYY'.

### Sample file (Payroll)

_External Payroll No_: 99999999  
_Employee_: 11  
28/10-2024 with 8 _normal hours_ and 4.25 _overtime_.  
29/10-2024 with 4.75 _normal hours_ and 3.25 _absence_ (Loopbaan Verlof).

```
KLX1999999911                  28/10/2024  0100   800
KLX1999999911                  29/10/2024  0100   475
KLX1999999911                  28/10/2024  0138   425
KLX1999999911                  29/10/2024  2353   325
```

## See also

[Export Payroll](../daily-use/export-payroll.md)
