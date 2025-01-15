##  LN {#GUID-DCC9EDAA-D308-4145-8E05-8D06A5EF5F6F} 

Syntax 

![Description of ln.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ln.gif)[ Description of the illustration ln.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/ln.md)

Purpose 

` LN ` returns the natural logarithm of *n* , where *n* is greater than 0. 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is ` BINARY_FLOAT ` , then the function returns ` BINARY_DOUBLE ` . Otherwise the function returns the same numeric data type as the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the natural logarithm of 95: 
    
    
    ```
    SELECT LN(95) "Natural log of 95"
      FROM DUAL;
    
    Natural log of 95
    -----------------
           4.55387689
    ```
