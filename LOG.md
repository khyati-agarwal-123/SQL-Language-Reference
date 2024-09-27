[Previous](LOCALTIMESTAMP.md) [Next](LOWER.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. LOG 

## LOG

Syntax

![Description of log.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/log.gif)  
[Description of the illustration log.eps](img_text/log.md)

Purpose

`LOG` returns the logarithm, base `n2`, of `n1`. The base `n2` can be any
positive value other than 0 or 1 and `n1` can be any positive value.

This function takes as arguments any numeric data type or any nonnumeric data
type that can be implicitly converted to a numeric data type. If any argument
is `BINARY_FLOAT` or `BINARY_DOUBLE`, then the function returns
`BINARY_DOUBLE`. Otherwise the function returns `NUMBER`.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion

Examples

The following example returns the log of 100:

    
    
    SELECT LOG(10,100) "Log base 10 of 100"
      FROM DUAL;
    
    Log base 10 of 100
    ------------------
                     2 


[← Previous](LOCALTIMESTAMP.md)

[Next →](LOWER.md)
