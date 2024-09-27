[Previous](ASCIISTR.md) [Next](ATAN.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ASIN 

## ASIN

Syntax

![Description of asin.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/asin.gif)  
[Description of the illustration asin.eps](img_text/asin.md)

Purpose

`ASIN` returns the arc sine of `n`. The argument `n` must be in the range of
-1 to 1, and the function returns a value in the range of -pi/2 to pi/2,
expressed in radians.

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

The following example returns the arc sine of .3:

    
    
    SELECT ASIN(.3) "Arc_Sine"
      FROM DUAL;
    
     Arc_Sine
    ----------
    .304692654


[← Previous](ASCIISTR.md)

[Next →](ATAN.md)
