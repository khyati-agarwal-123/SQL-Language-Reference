##  SIN {#GUID-2AF4895F-5D23-4165-89D5-B1D404ED99BF} 

Syntax 

![Description of sin.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sin.gif)[ Description of the illustration sin.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/sin.md)

Purpose 

` SIN ` returns the sine of *n* (an angle expressed in radians). 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is ` BINARY_FLOAT ` , then the function returns ` BINARY_DOUBLE ` . Otherwise the function returns the same numeric data type as the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the sine of 30 degrees: 
    
    
    ```
    SELECT SIN(30 * 3.14159265359/180)
     "Sine of 30 degrees" FROM DUAL;
    
    Sine of 30 degrees
    ------------------
                    .5
    ```
