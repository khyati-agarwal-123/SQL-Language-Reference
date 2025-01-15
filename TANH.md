##  TANH {#GUID-8DD0B75F-1BDB-4E41-8C6D-FB5B2908AF80} 

Syntax 

![Description of tanh.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/tanh.gif)[ Description of the illustration tanh.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/tanh.md)

Purpose 

` TANH ` returns the hyperbolic tangent of *n* . 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is ` BINARY_FLOAT ` , then the function returns ` BINARY_DOUBLE ` . Otherwise the function returns the same numeric data type as the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the hyperbolic tangent of .5: 
    
    
    ```
    SELECT TANH(.5) "Hyperbolic tangent of .5" 
       FROM DUAL;
    
    Hyperbolic tangent of .5
    ------------------------
                  .462117157 
    ```
