##  EXP {#GUID-414FB4AE-03B5-41AD-AE33-E3755EFED0A0} 

Syntax 

![Description of exp.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/exp.gif)[ Description of the illustration exp.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/exp.md)

Purpose 

` EXP ` returns ` e ` raised to the *n* th power, where ` e ` = 2.71828183... . The function returns a value of the same type as the argument. 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is ` BINARY_FLOAT ` , then the function returns ` BINARY_DOUBLE ` . Otherwise the function returns the same numeric data type as the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns ` e ` to the 4th power: 
    
    
    ```
    SELECT EXP(4) "e to the 4th power"
      FROM DUAL;
    
    e to the 4th power
    ------------------
              54.59815 
    ```
