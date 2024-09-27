[Previous](LISTAGG.md) [Next](LNNVL.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. LN 

## LN

Syntax

![Description of ln.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ln.gif)  
[Description of the illustration ln.eps](img_text/ln.md)

Purpose

`LN` returns the natural logarithm of `n`, where `n` is greater than 0.

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

The following example returns the natural logarithm of 95:

    
    
    SELECT LN(95) "Natural log of 95"
      FROM DUAL;
    
    Natural log of 95
    -----------------
           4.55387689


[← Previous](LISTAGG.md)

[Next →](LNNVL.md)
