[Previous](trunc-interval.md) [Next](TZ_OFFSET.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TRUNC (number) 

## TRUNC (number)

Syntax

trunc_number::=

![Description of trunc_number.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/trunc_number.gif)  
[Description of the illustration trunc_number.eps](img_text/trunc_number.md)

Purpose

The `TRUNC` (number) function returns `n1` truncated to `n2` decimal places.
If `n2` is omitted, then `n1` is truncated to 0 places. `n2` can be negative
to truncate (make zero) `n2` digits left of the decimal point.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. If you omit
`n2`, then the function returns the same data type as the numeric data type of
the argument. If you include `n2`, then the function returns `NUMBER`.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

Examples

The following examples truncate numbers:

    
    
    SELECT TRUNC(15.79,1) "Truncate" FROM DUAL;
    
      Truncate
    ----------
          15.7
    
    SELECT TRUNC(15.79,-1) "Truncate" FROM DUAL;
    
      Truncate
    ----------
            10


[← Previous](trunc-interval.md)

[Next →](TZ_OFFSET.md)
