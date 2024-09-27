[Previous](CORR_A.md) [Next](COSH.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. COS 

## COS

Syntax

![Description of cos.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cos.gif)  
[Description of the illustration cos.eps](img_text/cos.md)

Purpose

`COS` returns the cosine of `n` (an angle expressed in radians).

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

The following example returns the cosine of 180 degrees:

    
    
    SELECT COS(180 * 3.14159265359/180) "Cosine of 180 degrees"
      FROM DUAL;
    
    Cosine of 180 degrees
    ---------------------
                       -1


[← Previous](CORR_A.md)

[Next →](COSH.md)
