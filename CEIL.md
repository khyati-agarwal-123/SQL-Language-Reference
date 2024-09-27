[Previous](ceil-interval.md) [Next](CHARTOROWID.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CEIL (number)

## CEIL (number)

Syntax

![Description of ceil.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ceil.gif)  
[Description of the illustration ceil.eps](img_text/ceil.md)

Purpose

`CEIL` returns the smallest integer that is greater than or equal to `n`. The
number `n` can always be written as the difference of an integer `k` and a
positive fraction `f` such that 0 <= `f` < 1 and `n` = `k` \- `f`. The value
of `CEIL` is the integer `k`. Thus, the value of `CEIL` is `n` itself if and
only if `n` is precisely an integer.

This function takes as an argument any numeric data type or any nonnumeric
data type that can be implicitly converted to a numeric data type. The
function returns the same data type as the numeric data type of the argument.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion and [FLOOR
(number)](FLOOR.md#GUID-67F61AC7-C097-4397-A122-213157BF584F)

Examples

The following example returns the smallest integer greater than or equal to
the order total of a specified order:

    
    
    SELECT order_total, CEIL(order_total)
      FROM orders
      WHERE order_id = 2434;
    
    ORDER_TOTAL CEIL(ORDER_TOTAL)
    ----------- -----------------
       268651.8            268652


[← Previous](ceil-interval.md)

[Next →](CHARTOROWID.md)
