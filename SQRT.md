##  SQRT {#GUID-E28C0B65-AAD8-4077-A82E-2FB4CD261CCA} 

Syntax 

![Description of sqrt.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sqrt.gif)[ Description of the illustration sqrt.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/sqrt.md)

Purpose 

` SQRT ` returns the square root of *n* . 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. The function returns the same data type as the numeric data type of the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

  * If *n* resolves to a ` NUMBER ` , then the value *n* cannot be negative. ` SQRT ` returns a real number. 

  * If *n* resolves to a binary floating-point number ( ` BINARY_FLOAT ` or ` BINARY_DOUBLE ` ): 

    * If *n* >= 0, then the result is positive. 

    * If *n* = -0, then the result is -0. 

    * If *n* < 0, then the result is ` NaN ` . 




Examples 

The following example returns the square root of 26: 
    
    
    ```
    SELECT SQRT(26) "Square root" FROM DUAL;
    
    Square root
    -----------
    5.09901951 
    ```
