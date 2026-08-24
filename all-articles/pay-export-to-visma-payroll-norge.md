# Pay Export to Visma Payroll Norge

Below is special information for the norwegian Visma payroll system. General information is available [here](../daily-use/export-payroll.md).

### Summation

This file should sum the lines for the entire selected period, if they have the same _Pay Type_ and _Rate_.

### File format

There are 6 special fields ind the file. The customer specific walues are filled in by code with [OnTable\_JobManPayEntry\_ExternalDimension20](../advanced-setup/code-customization.md). _Kostnadsbaerere1_ filled in 1. returnvalue, _Kostnadsbaerere2_ filled in 2. returnvalue etc.

*   The following fields are _empty_:
    *   _Lonnsaar_
    *   _Lonnskjoerenummer_
    *   _Grunnlag_
    *   _Konto_
    *   _Motkonto_
*   The file contains the following fields: `Lonnsaar, Lonnskjoerenummer, Ansattnummer, Lonnsart, Grunnlag, Antall, Sats, Belop, Konto, Motkonto, Kostnadsbaerere1, Kostnadsbaerere2, Kostnadsbaerere3, Kostnadsbaerere4, Kostnadsbaerere5, Kostnadsbaerere6`
*   Decimal fields are specified _without_ a thousand separator, with 2 decimal places and with _dot_ as decimal point.

### Advanced setup

```
STANDARD,ANTALL,SATS,BELOP
D5132,ANTALL,SATS
```

#### Explanation

*   `STANDARD,ANTALL,SATS,BELOP` All Pay Types are exported with both Antall _(Quantity)_, Sats _(Unit price)_ and Belop _(Amount)_.
*   `D5152,ANTAL,SATS` The Pay Type _D5152_ are exported only the Antall _(Quantity)_ and Sats _(Unit price)_ fields.

## See also

[Export Payroll](../daily-use/export-payroll.md)
