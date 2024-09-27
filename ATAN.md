[Previous](ASIN.md) [Next](ATAN2.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ATAN 

## ATAN

Syntax

![Description of atan.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/atan.gif)  
[Description of the illustration atan.eps](img_text/atan.md)

Purpose

`ATAN` returns the arc tangent of `n`. The argument `n` can be in an unbounded
range and returns a value in the range of -pi/2 to pi/2, expressed in radians.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. If the
argument is `BINARY_FLOAT`, then the function returns `BINARY_DOUBLE`.
Otherwise the function returns the same numeric data type as the argument.

See Also:

[ATAN2](ATAN2.md#GUID-D34E671B-F3C0-4390-A2D8-ABB702B4B5D3) for information
about the `ATAN2` function and [Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

Examples

The following example returns the arc tangent of .3:

    
    
    SELECT ATAN(.3) "Arc_Tangent"
      FROM DUAL;
    
    Arc_Tangent
    ----------
    .291456794


[← Previous](ASIN.md)

[Next →](ATAN2.md)
