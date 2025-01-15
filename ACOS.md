##  ACOS {#GUID-B4C70DD5-B908-4130-975A-6CFD5C1AC1F9} 

Syntax 

![Description of acos.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/acos.gif)[ Description of the illustration acos.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/acos.md)

Purpose 

` ACOS ` returns the arc cosine of *n* . The argument *n* must be in the range of -1 to 1, and the function returns a value in the range of 0 to *pi* , expressed in radians. 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is ` BINARY_FLOAT ` , then the function returns ` BINARY_DOUBLE ` . Otherwise the function returns the same numeric data type as the argument. 

> **note:** See Also: 

[ Table 2-9 ](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937) for more information on implicit conversion 

Examples 

The following example returns the arc cosine of .3: 
    
    
    ```
    SELECT ACOS(.3)"Arc_Cosine"
      FROM DUAL;
    
    Arc_Cosine
    ----------
    1.26610367
    ```
