# Type

The field states the relation from where the balance should be loaded.

*   **Time Counter** is used to collect balance from [this table](../jobmanager-calculations/time-counters.md).
*   **Pay Type** is used to collect balance from [this table](../payroll-setup/pay-type.md).
*   **Lessor** is used to collect balance from Lessor Payroll.
*   **Codeunit** is used to add other balances from sources of your choice.
*   **Statistics Column** is used to collect balances from Statistics column setup.

By using _Codeunit_ one **avoids** changes to JobManager objects, making updating JobManager versions much easier. _The installation package for JobManager contains some examples._
