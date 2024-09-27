[Previous](floor-interval.md) [Next](FROM_TZ.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. FLOOR (number) 

## FLOOR (number)

Syntax

![Description of floor.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/floor.gif)  
[Description of the illustration floor.eps](img_text/floor.md)

Purpose

`FLOOR` returns the largest integer equal to or less than `n`. The number `n`
can always be written as the sum of an integer `k` and a positive fraction `f`
such that 0 <= `f` < 1 and `n` = `k` \+ `f`. The value of `FLOOR` is the
integer `k`. Thus, the value of `FLOOR` is `n` itself if and only if `n` is
precisely an integer.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. The
function returns the same data type as the numeric data type of the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion and [CEIL
(number)](CEIL.md#GUID-6DCC9AFB-9B80-4C27-AF63-5AA3B1E43660)

Examples

The following example returns the largest integer equal to or less than 15.7:

    
    
    SELECT FLOOR(15.7) "Floor"
      FROM DUAL;
    
         Floor
    ----------
            15


[← Previous](floor-interval.md)

[Next →](FROM_TZ.md)
