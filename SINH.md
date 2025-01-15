##  SINH {#GUID-1EB8626B-4D84-4EAD-BD23-1A97F186FD4A} 

Syntax 

![Description of sinh.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sinh.gif)[ Description of the illustration sinh.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/sinh.md)

Purpose 

` SINH ` returns the hyperbolic sine of *n* . 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is ` BINARY_FLOAT ` , then the function returns ` BINARY_DOUBLE ` . Otherwise the function returns the same numeric data type as the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the hyperbolic sine of 1: 
    
    
    ```
    SELECT SINH(1) "Hyperbolic sine of 1" FROM DUAL;
    
    Hyperbolic sine of 1
    --------------------
              1.17520119
    ```
