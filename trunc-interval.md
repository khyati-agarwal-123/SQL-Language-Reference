[Previous](TRUNC-date.md) [Next](TRUNC-number.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. TRUNC (interval)

## TRUNC (interval)

Syntax

![Description of trunc_interval.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/trunc_interval.gif)  
[Description of the illustration
trunc_interval.eps](img_text/trunc_interval.md)

Purpose

`TRUNC(interval)` returns the interval rounded down to the unit specified by
the second argument `fmt`, the format model .

The absolute value of `TRUNC(interval)` is never greater than the absolute
value of `interval`. The result precision is the same as the input precision,
since there is no overflow issue for `TRUNC(interval)`.

For `INTERVAL YEAR TO MONTH`, `fmt` can only be year. The default `fmt` is
year.

For `INTERVAL DAY TO SECOND`, `fmt` can be day, hour and minute. The default
`fmt` is day. Note that `fmt` does not support second.

See Also:

Refer to [CEIL, FLOOR, ROUND, and TRUNC Date Functions](ROUND-and-TRUNC-Date-
Functions.md#GUID-8E10AB76-21DA-490F-A389-023B648DDEF8) for the permitted
format models to use in `fmt`.

Examples

    
    
    SELECT TRUNC(INTERVAL '+123-06' YEAR(3) TO MONTH) AS year_trunc;
    
    YEAR_TRUNC
    ----------
    +123-00
    
    
    SELECT TRUNC(INTERVAL '+99-11' YEAR(2) TO MONTH, 'YEAR') AS year_trunc;
    
    YEAR_TRUNC
    ----------
    +99-00
    
    
    SELECT TRUNC(INTERVAL '+4 12:42:10.222' DAY(2) TO SECOND(3), 'DD') AS day_trunc;
    
    DAY_TRUNC
    -------------------
    +04 00:00:00.000000


[← Previous](TRUNC-date.md)

[Next →](TRUNC-number.md)
