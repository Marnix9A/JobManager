# Condition

If [Type](./type-3.md) of **Job Id (present)** the following applies:

*   Fill in [Job Id](../general-setup/job-id-2.md). Can be further narrowed by [Filter Stamp Journal](./filter-stamp-journal.md).

If [Type](./type-3.md) of **Time Counter (condition)** the following applies:

*   Fill in condition, eg.:
    
    ```
    [OT1]>0
    ```
    
    or
    
    ```
    [OT1]<(-10)
    ```
    
    or
    
    ```
    ([OT2]=0) AND (([LON-06]>0) OR ([LON-07]>0))
    ```
    
*   Syntax
    *   Time Counters writes with **\[ \]**
    *   Use **\+ - \* /**
    *   Use **( )**
    *   Use **\= > < >= <=**
    *   Use **AND OR && || OG ELLER**
*   The logical _parser_ has certain limitations:
    
    *   A formula **can't** start with **\-** _minus_. Can be resolved by using parentheses **( )**.
    *   Two operators **can't** stand next to each other:
        *   `[OT1]<-10` solved by using **( )** parentheses: `[OT1]<(-10)`
        *   `20*-10` solved by using **( )** parentheses: `20*(-10)`
