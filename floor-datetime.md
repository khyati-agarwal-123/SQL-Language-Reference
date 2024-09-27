[Previous](FIRST_VALUE.md) [Next](floor-interval.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. FLOOR (datetime)

## FLOOR (datetime)

Syntax

  

![Description of floor_datetimes.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/floor_datetimes.gif)  
[Description of the illustration
floor_datetimes.eps](img_text/floor_datetimes.md)

  

Purpose

`FLOOR(datetime)` returns the date or the timestamp rounded down to the unit
specified by the second argument `fmt`, the format model. This function is not
sensitive to the `NLS_CALENDAR` session parameter. It operates according to
the rules of the Gregorian calendar. The value returned is always of data type
`DATE`, even if you specify a different datetime data type for the first
argument. If you do not specify the second argument, the default format model
'`DD`' is used.

The `FLOOR` and `TRUNC` functions are synonymous for dates and timestamps.

See Also:

Refer to [CEIL, FLOOR, ROUND, and TRUNC Date Functions](ROUND-and-TRUNC-Date-
Functions.md#GUID-8E10AB76-21DA-490F-A389-023B648DDEF8) for the permitted
format models to use in `fmt`.

Examples

For these examples `NLS_DATE_FORMAT` is set:

    
    
    ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY HH24:MI:SS';
    
    
    
    SELECT FLOOR(TO_DATE ('28-FEB-2023','DD-MON-YYYY'), 'MM') AS month_floor;
    
    MONTH_FLOOR
    --------------------
    01-FEB-2023 00:00:00
    
    
    SELECT FLOOR(TO_TIMESTAMP ('28-FEB-2023 14:10:10','DD-MON-YYYY HH24:MI:SS'),'HH24') AS hour_floor;
    
    HOUR_FLOOR
    --------------------
    28-FEB-2023 14:00:00
    


[← Previous](FIRST_VALUE.md)

[Next →](floor-interval.md)
