[Previous](FLOOR.md) [Next](from_vector.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. FROM_TZ 

## FROM_TZ

Syntax

![Description of from_tz.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/from_tz.gif)  
[Description of the illustration from_tz.eps](img_text/from_tz.md)

Purpose

`FROM_TZ` converts a timestamp value and a time zone to a `TIMESTAMP` `WITH`
`TIME` `ZONE` value. `time_zone_value` is a character string in the format
`'TZH:TZM'` or a character expression that returns a string in `TZR` with
optional `TZD` format.

Examples

The following example returns a timestamp value to `TIMESTAMP` `WITH` `TIME`
`ZONE`:

    
    
    SELECT FROM_TZ(TIMESTAMP '2000-03-28 08:00:00', '3:00') 
      FROM DUAL;
    
    FROM_TZ(TIMESTAMP'2000-03-2808:00:00','3:00')
    ---------------------------------------------------------------
    28-MAR-00 08.00.000000000 AM +03:00


[← Previous](FLOOR.md)

[Next →](from_vector.md)
