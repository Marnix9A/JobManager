# Paty Export to Standard CSV file

This payroll file is a generic standard payroll file with all fields. General information can be found [here](../daily-use/export-payroll.md).

### File Format

*   The file contains column headings in the first line. These will be translated into the language in which BC/NAV is executed.
*   The file contains the following fields _(here in English)_: `Pay Date;Employee;Employee External No.;Pay Type;Pay Type External No.;Qty;Rate;Amount;External Type;External Unit;Dim 1;Dim 2;Dim 3;Dim 4;Dim 5;Dim 6;Dim 7;Dim 8;Dim 9;Dim 10;Dim 11;Dim 12;Dim 13;Dim 14;Dim 15;Dim 16;Dim 17;Dim 18;Dim 19;Dim 20`
    
*   _Pay Date_ is the date from the Pay Event.
*   _Employee_ is the employee from the Pay Event.
*   _Employee External No._ where the content of this field is set up [here](../daily-use/number.md).
*   _Pay Type_ is the Pay Type from the Pay Event.
*   _Pay Type External No._ where the content of this field is set up [here](../payroll-setup/external-no.md).
*   _Qty_ is the number from the Pay Event. The value can be summed (see later).
*   _Rate_ is the rate from the Pay Event. The value can be an average if summation (see later).
*   _Amount_ is `Quantity X Rate`.
*   _External Type_ where the content of this field is set up [here](../payroll-setup/external-type.md).
*   _External Unit_ where the content of this field is set up [here](../payroll-setup/external-unit.md).
*   _Dim ##_ are 20 special fields. These fields are very customer-specific, and a small piece of code must therefore be created that can specify the values. The values ​​are set with [OnTable\_JobManPayEntry\_ExternalDimension20](../advanced-setup/code-customization.md)  
      
    
*   The file uses `;` as a separator.
*   Commas are specified _without_ a thousand separator, with 2 decimals and a period as a decimal point.
*   Dates are specified as `YYYY-MM-DD`.
    

### Summarization

The file can be summed if this is set up in the field [Sort Order](../payroll-setup/sort-order.md) for this export in [Pay Export Type](../payroll-setup/pay-export-type.md).

### Advanced setup

Setup whether the fields _Qty_, _Rate_ and _Amount_ should contain a value in the file. Some salary systems require that, for example, _Rate_ is hidden for certain salary types.

STANDARD,QTY,RATE,AMOUNT 1234,QTY,AMOUNT

In the above example, the _Rate_ field will be empty for Pay Type `1234`. The rest will follow the top `STANDARD` line and content in fields.

_Qty_ can be specified with the following syntax: `QTY`, `QUANTITY`, `ANTAL` or `ENHEDER`.  
_Rate_ can be specified with the following syntax: `RATE` or `SATS`.  
_Amount_ can be specified with the following syntax: `AMOUNT` or `BELØB`.  

_Alternatively, it can be abbreviated to the first 3 letters of the word. `QUO` for `QUANTITY`._

## See also

[Paty Export to Standard CSV file](./paty-export-to-standard-csv-file.md)
