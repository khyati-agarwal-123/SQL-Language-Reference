##  POWER {#GUID-D280B322-D2C3-46D0-8076-C88F16CBEDC2} 

Syntax 

![Description of power.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/power.gif)[ Description of the illustration power.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/power.md)

Purpose 

` POWER ` returns *n2* raised to the *n1* power. The base *n2* and the exponent *n1* can be any numbers, but if *n2* is negative, then *n1* must be an integer. 

This function takes as arguments any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If any argument is ` BINARY_FLOAT ` or ` BINARY_DOUBLE ` , then the function returns ` BINARY_DOUBLE ` . Otherwise, the function returns ` NUMBER ` . 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns 3 squared: 
    
    
    ```
    SELECT POWER(3,2) "Raised"
      FROM DUAL;
    
        Raised
    ----------
             9
    ```
