##  TAN {#GUID-473E2008-5951-4FC8-A356-14D3D085B8AA} 

Syntax 

![Description of tan.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/tan.gif)[ Description of the illustration tan.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/tan.md)

Purpose 

` TAN ` returns the tangent of *n* (an angle expressed in radians). 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is ` BINARY_FLOAT ` , then the function returns ` BINARY_DOUBLE ` . Otherwise the function returns the same numeric data type as the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the tangent of 135 degrees: 
    
    
    ```
    SELECT TAN(135 * 3.14159265359/180)
       "Tangent of 135 degrees"  FROM DUAL;
    
    Tangent of 135 degrees
    ----------------------
                       - 1
    ```
