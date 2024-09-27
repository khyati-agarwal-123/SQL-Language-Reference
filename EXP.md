[Previous](EXISTSNODE.md) [Next](EXTRACT-datetime.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. EXP 

## EXP

Syntax

![Description of exp.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/exp.gif)  
[Description of the illustration exp.eps](img_text/exp.md)

Purpose

`EXP` returns `e` raised to the `n`th power, where `e` = 2.71828183... . The
function returns a value of the same type as the argument.

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

The following example returns `e` to the 4th power:

    
    
    SELECT EXP(4) "e to the 4th power"
      FROM DUAL;
    
    e to the 4th power
    ------------------
              54.59815 


[← Previous](EXISTSNODE.md)

[Next →](EXTRACT-datetime.md)
