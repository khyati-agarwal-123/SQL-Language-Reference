[Previous](REPLACE.md) [Next](round-interval.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ROUND (datetime) 

## ROUND (datetime)

Syntax

round_datetime::=

![Description of round_date.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/round_date.gif)  
[Description of the illustration round_date.eps](img_text/round_date.md)

Purpose

`ROUND` returns `datetime` rounded to the unit specified by the format model
`fmt`.

This function is not sensitive to the `NLS_CALENDAR` session parameter. It
operates according to the rules of the Gregorian calendar. The value returned
is always of data type `DATE`, even if you specify a different datetime data
type for `date`. If you omit `fmt`, then `date` is rounded to the nearest day.
The `date` expression must resolve to a `DATE` value.

See Also:

"[CEIL, FLOOR, ROUND, and TRUNC Date Functions](ROUND-and-TRUNC-Date-
Functions.md#GUID-8E10AB76-21DA-490F-A389-023B648DDEF8)" for the permitted
format models to use in `fmt`

Examples

The following example rounds a date to the first day of the following year:

    
    
    SELECT ROUND (TO_DATE ('27-OCT-00'),'YEAR')
       "New Year" FROM DUAL;
     
    New Year
    ---------
    01-JAN-01


[← Previous](REPLACE.md)

[Next →](round-interval.md)
