##  ABS {#GUID-D8D3489A-44EA-4FEC-A6F0-B5E312FFC231} 

Syntax 

![Description of abs.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/abs.gif)[ Description of the illustration abs.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/abs.md)

Purpose 

` ABS ` returns the absolute value of *n* . 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. The function returns the same data type as the numeric data type of the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the absolute value of -15: 
    
    
    ```
    SELECT ABS(-15) "Absolute"
      FROM DUAL;
    
      Absolute
    ----------
            15
    ```
