[Previous](TAN.md) [Next](TIMESTAMP_TO_SCN.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TANH 

## TANH

Syntax

![Description of tanh.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/tanh.gif)  
[Description of the illustration tanh.eps](img_text/tanh.md)

Purpose

`TANH` returns the hyperbolic tangent of `n`.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. If the
argument is `BINARY_FLOAT`, then the function returns `BINARY_DOUBLE`.
Otherwise the function returns the same numeric data type as the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

Examples

The following example returns the hyperbolic tangent of .5:

    
    
    SELECT TANH(.5) "Hyperbolic tangent of .5" 
       FROM DUAL;
    
    Hyperbolic tangent of .5
    ------------------------
                  .462117157 


[← Previous](TAN.md)

[Next →](TIMESTAMP_TO_SCN.md)
