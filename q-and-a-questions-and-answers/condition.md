# Condition

Conditions can be defined, to control which pay counters to calculate.

Example: You can setup a Pay Type _1215_ which is only triggered if Pay Counter _ILL\_ABS_ is zero within the relevant period.

Condition is written as a formula:

### Exampel

*   Formula for the above exampel
    
    ```
    [ILL_ABS]=0
    ```
    
*   Advanced formula
    
    ```
    ([OT2]=0) AND (([PAY-06]>0) OR ([PAY-07]>0))
    ```
    

### Syntax

*   Pay Counters writes with **\[ \]**
*   Use **\+ - \* /**
*   Use **( )**
*   Use **\> < >= <= =**
*   Use **AND &&** or **OR ||**

_Your local language equivalent to **AND** and **OR** can be used, if JobManager is translated into your language._

### Limitations

The logical _parser_ has certain limitations:

*   A formula **can't** start with **\-** _minus_. Can be resolved by using parentheses **( )**.
*   Two operators **can't** stand next to each other:
    *   `([ILL_ABS]-[ILL_TEST])<-10` solved by using **( )** parentheses: `([ILL_ABS]-[ILL_TEST])<(-10)`
    *   `20*-10` solved by using **( )** parentheses: `20*(-10)`

### Troubleshooting

See [here](./debug-condition.md).
