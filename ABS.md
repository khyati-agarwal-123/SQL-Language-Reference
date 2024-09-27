[Previous](Single-Row-Functions.md) [Next](ACOS.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ABS 

## ABS

Syntax

![Description of abs.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/abs.gif)  
[Description of the illustration abs.eps](img_text/abs.md)

Purpose

`ABS` returns the absolute value of `n`.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. The
function returns the same data type as the numeric data type of the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

Examples

The following example returns the absolute value of -15:

    
    
    SELECT ABS(-15) "Absolute"
      FROM DUAL;
    
      Absolute
    ----------
            15


[← Previous](Single-Row-Functions.md)

[Next →](ACOS.md)
