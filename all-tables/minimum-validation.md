# Minimum (validation)

The answer can be validated with these rules:

| Type | Validation |
| :-- | :-- |
| Text | Length of the text is within minimum and maximum _(validation)_ |
| Integer | The value is within minimum and maximum _(validation)_ |
| Decimal | The value is within minimum and maximum _(validation)_ |
| Option | The **number of** selected options should be within minimum and maximum _(validation)_ |
| Date | The date is within _today_ shifted by the minimum and _today_ shifted by the maximum. Eg. -1 means _yesterday_ and 2 means _the day after tomorrow_ |
| Time | The time is within the mininum and maximum. Enter the value as a decimal value HH.MM (specify as 24H format, but shown to user as users local format). Eg. 13.20 means 01:20PM |
| Date and time | The date is within _today_ shifted by the minimum and _today_ shifted by the maximum. Eg. -1 means _yesterday_ and 2 means _the day after tomorrow_. For minimum the time 00:00 (00:00AM) is applied and for maximum 23:59:59 (12:00PM) is applied |

If _both_ Minimum and Maximum are _blank_, a question is considered _optional_. This is used by the field [Allow skip optional questions](../daily-use/allow-skip-optional-questions.md) on the [questionnaire](../daily-use/jobmanager-questionnaire.md) table.
