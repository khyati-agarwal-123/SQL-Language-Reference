[Previous](floor-datetime.md) [Next](FLOOR.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. FLOOR (interval)

## FLOOR (interval)

Syntax

![Description of floor_interval.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/floor_interval.gif)  
[Description of the illustration
floor_interval.eps](img_text/floor_interval.md)

Purpose

`FLOOR(interval)` returns the interval rounded down to the unit specified by
the second argument `fmt`, the format model .

The result of `FLOOR(interval)` is never larger than `interval` . The result
precision for year and day is the input precision for year plus one and day
plus one, since `FLOOR(interval)` can have overflow . If an interval already
has the maximum precision for year and day, the statement compiles but errors
at runtime.

For `INTERVAL YEAR TO MONTH`, `fmt` can only be year. The default `fmt` is
year.

For `INTERVAL DAY TO SECOND`, `fmt` can be day, hour and minute. The default
`fmt` is day. Note that `fmt` does not support second.

`FLOOR(interval)` supports the format models of `ROUND` and `TRUNC`.

See Also:

Refer to [CEIL, FLOOR, ROUND, and TRUNC Date Functions](ROUND-and-TRUNC-Date-
Functions.md#GUID-8E10AB76-21DA-490F-A389-023B648DDEF8) for the permitted
format models to use in `fmt`.

Examples

    
    
    SELECT FLOOR(INTERVAL '+123-5' YEAR(3) TO MONTH) as year_floor;
    
    YEAR_FLOOR
    ---------------------------------------------------------------------------
    +000000123-00
    
    
    SELECT FLOOR(INTERVAL '+99-11' YEAR(2) TO MONTH, 'YEAR') as year_floor;
    
    YEAR_FLOOR
    ---------------------------------------------------------------------------
    +000000099-00
    
    
    SELECT FLOOR(INTERVAL '+4 12:42:10.222' DAY(2) TO SECOND(3), 'DD') as year_floor;
    
    YEAR_FLOOR
    ---------------------------------------------------------------------------
    +000000004 00:00:00.000000000
    


[← Previous](floor-datetime.md)

[Next →](FLOOR.md)
