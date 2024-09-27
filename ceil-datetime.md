[Previous](CAST.md) [Next](ceil-interval.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CEIL (datetime)

## CEIL (datetime)

Syntax

  

![Description of ceil_datetimes.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ceil_datetimes.gif)  
[Description of the illustration
ceil_datetimes.eps](img_text/ceil_datetimes.md)

  

Purpose

`CEIL(datetime)` returns the date or the timestamp rounded up to the unit
specified by the second argument `fmt`, the format model. If the input value
is already truncated to the specified unit, then the return value is the same
as the input. That is, if `datetime` = `TRUNC(datetime, fmt)`, then
`CEIL(datetime, fmt)` = `datetime`. For example, `CEIL(DATE '2023-02-01',
'MONTH')` returns February 1 2023.

This function is not sensitive to the `NLS_CALENDAR` session parameter. It
operates according to the rules of the Gregorian calendar. The value returned
is always of data type `DATE`, even if you specify a different datetime data
type for the argument. If you do not specify the second argument, the default
format model '`DD`' is used.

See Also:

Refer to [CEIL, FLOOR, ROUND, and TRUNC Date Functions](ROUND-and-TRUNC-Date-
Functions.md#GUID-8E10AB76-21DA-490F-A389-023B648DDEF8) for the permitted
format models to use in `fmt`.

Examples

For these examples `NLS_DATE_FORMAT` is set:

    
    
    ALTER SESSION SET NLS_DATE_FORMAT = 'DD-MON-YYYY HH24:MI:SS';
    
    
    SELECT CEIL(TO_DATE ('28-FEB-2023','DD-MON-YYYY'), 'MM') AS month_ceiling;
    
    MONTH_CEILING
    --------------------
    01-MAR-2023 00:00:00
    
    
    
    SELECT CEIL(TO_TIMESTAMP ('28-FEB-2023 14:10:10','DD-MON-YYYY HH24:MI:SS'),'HH24') AS hour_ceiling;
    
    HOUR_CEILING
    --------------------
    28-FEB-2023 15:00:00
    


[← Previous](CAST.md)

[Next →](ceil-interval.md)
