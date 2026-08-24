# Comments Setup

**In addition to the information below, please refer to [JobManager Attachments](../all-tables/jobmanager-attachment.md), which makes it possible to save files in the NAV/BC database. This is especially appropriate in newer BC installations, where the possibility of links has been eliminated.**

JobManager offers the opportunity to associate **Comments** and **Links** to [Jobs](../general-setup/jobmanager-job.md).

These will then be available to the employee when registre time.

JobManager offers a standard setup for showing _Comments_ and _Links_ to a range of standard NAV tables. The lines in this table is [automatically created](../general-setup/jobmanager-foundation-setup-guide.md).

These defaults can be [enable/disable](./active.md) as desired.

Reference to other _Comments_ and _Links_ can be set up by creating a new line.

Select [Type](./type-2.md) and fill in [Caption](./caption.md), [Sorting](./sorting.md) and the appropriate fields:

*   Type _Comment_ is used to collect _Comments_ from related tables. Also fill in:
    *   [Reference Table](./reference-table.md)
    *   [Comment Field](./comment-field.md)
    *   Up to 5 filters can be associated with [Field on Reference Table (X)](./field-on-reference-table-1.md), [Field on Job Tabel (X)](./field-on-job-table-1.md) and/or [Constant (X)](./constant-1.md)   
*   Type _Link_ is used to collect _Links_ from related tables. Also fill in:
    *   [Reference Table](./reference-table.md)
    *   Up to 5 filters can be associated with [Field on Reference Table (X)](./field-on-reference-table-1.md), [Field on Job Tabel (X)](./field-on-job-table-1.md) and/or [Constant (X)](./constant-1.md)
*   Type _Codeunit_ is used to add entirely different _Comments_ and/or _Links_. That could be from a new table. \*Also fill in:
    *   [Codeunit](./codeunit.md)

The appearance of [Caption](./caption-style.md) and [Text](./caption-style.md) can be changed for all types.

Field _Drop Empty line_ on Comments, if eg. Caption is not filled in, the line wille be hidden.

The installation package for JobManager contains some examples codeunits.

[Ref. Type](./ref-type.md)  
[Sorting](./sorting.md)  
[Caption](./caption.md)  
[Active](./active.md)  
[Type](./type-2.md)  
[Reference Table](./reference-table.md)  
[Comment Field](./comment-field.md)  
[Codeunit](./codeunit.md)  
[Caption Style](./caption-style.md)  
[Text Style](./text-style.md)  
[Highlight Comments](../daily-use/highlight-comments.md)  
[Add links/image](./add-links-image.md)  
[Status (1)](./status-1.md)  
[Field on Reference Table (1)](./field-on-reference-table-1.md)  
[Field on Job Table (1)](./field-on-job-table-1.md)  
[Constant (1)](./constant-1.md)  
[Status (2)](./status-2.md)  
[Field on Reference Table (2)](./field-on-reference-table-2.md)  
[Field on Job Table (2)](./field-on-job-table-2.md)  
[Constant (2)](./constant-2.md)  
[Status (3)](./status-3.md)  
[Field on Reference Table (3)](./field-on-reference-table-3.md)  
[Field on Job Table (3)](./field-on-job-table-3.md)  
[Constant (3)](./constant-3.md)  
[Status (4)](./status-4.md)  
[Field on Reference Table (4)](./field-on-reference-table-4.md)  
[Field on Job Table (4)](./field-on-job-table-4.md)  
[Constant (4)](./constant-4.md)  
[Status (5)](./status-5.md)  
[Field on Reference Table (5)](./field-on-reference-table-5.md)  
[Field on Job Table (5)](./field-on-job-table-5.md)  
[Constant (5)](./constant-5.md)  

## See also

[JobManager - Registration Client](../daily-use/jobmanager-registration-client.md)  
[JobManager - Time Sheet](../daily-use/jobmanager-time-sheet.md)  
[Mobile Role Center](../daily-use/mobile-role-center.md)  
[Mobile Registration Client App](../mobile-registration-client-app/README.md)  
[JobManager Foundation Setup Guide](../general-setup/jobmanager-foundation-setup-guide.md)  
[Code customization](../advanced-setup/code-customization.md)
