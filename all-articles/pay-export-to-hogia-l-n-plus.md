# Pay Export to Hogia Løn Plus

Below is special information for the swedish payroll system Hogia Plus. General information is available [here](../daily-use/export-payroll.md).

The _Postidentifierare_ should be set in the [External Payroll number](../general-setup/external-payroll-number.md) in [JobManager setup](../general-setup/jobmanager-setup.md) table.

### Summation

A runtime parameter indicates whether this file should sum the lines for the entire selected period, if they have the same _Pay Type_ and _Rate_.

### File format

*   The file contains the following fields: `Postidentifierare, Anstallningsnummer, Loneartsnummer, Dummy, Belopp, Dummy, FraDatum, TilDatum`
    
    *   `Postidentifierare` 6 characters at position 1-6
    *   `Anstallningsnummer` 10 characters at (left-aligned) at position 7-16
    *   `Loneartsnummer` 3 characters at position 17-19
    *   `Dummy` 14 characters at position 20-33
    *   `Belopp` 14 characters at position 34-47
    *   `Dummy` 27 characters at position 48-74
    *   `FraDatum` 6 characters at position 75-80
    *   `TilDatum` 6 characters at position 81-88  
          
        
*   Decimal fields are specified _without_ a thousand separator, with 2 decimal places and _without a decimal point_. That is 12.34 would be `1234` . The number has leading `0` (zeros).
*   The 2 _Dummy_ fields are filled with `0`.
*   Dates are specified as \`YYMMDD'.
    

### Advanced setup

No further setup.

## See also

[Export Payroll](../daily-use/export-payroll.md)
