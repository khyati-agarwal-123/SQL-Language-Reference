[Previous](ATAN.md) [Next](AVG.md) JavaScript must be enabled to correctly
display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ATAN2 

## ATAN2

Syntax

![Description of atan2.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/atan2.gif)  
[Description of the illustration atan2.eps](img_text/atan2.md)

Purpose

`ATAN2` returns the arc tangent of `n1` and `n2`. The argument `n1` can be in
an unbounded range and returns a value in the range of -pi to pi, depending on
the signs of `n1` and `n2`, expressed in radians.

This function takes as arguments any numeric data type or any nonnumeric data
type that can be implicitly converted to a numeric data type. If any argument
is `BINARY_FLOAT` or `BINARY_DOUBLE`, then the function returns
`BINARY_DOUBLE`. Otherwise the function returns `NUMBER`.

See Also:

[ATAN](ATAN.md#GUID-12E8F1AA-54D0-4A19-8648-27094946C588) for information on
the `ATAN` function and [Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

Examples

The following example returns the arc tangent of .3 and .2:

    
    
    SELECT ATAN2(.3, .2) "Arc_Tangent2"
      FROM DUAL;
     
    Arc_Tangent2
    ------------
      .982793723


[← Previous](ATAN.md)

[Next →](AVG.md)
