[Previous](COS.html) [Next](COUNT.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. COSH 



## COSH 

Syntax

![Description of cosh.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cosh.gif)[Descriptionof the illustration cosh.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/cosh.md)

Purpose

`COSH` returns the hyperbolic cosine of `n`. 

This function takes as an argument any numeric data type or any nonnumeric data type that can be implicitly converted to a numeric data type. If the argument is `BINARY_FLOAT`, then the function returns `BINARY_DOUBLE`. Otherwise the function returns the same numeric data type as the argument. 

See Also:

[Table 2-9](Data-Type-Comparison-Rules.html#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell indicates implicit conversion of the data types") for more information on implicit conversion 

Examples

The following example returns the hyperbolic cosine of zero:
    
    
    SELECT COSH(0) "Hyperbolic cosine of 0"
      FROM DUAL;
    
    Hyperbolic cosine of 0
    ----------------------
                         1 

[← Previous](COS.md)

[Next →](COUNT.md)
