[Previous](ORA_DM_PARTITION_NAME.md) [Next](ORA_DST_CONVERT.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ORA_DST_AFFECTED 

## ORA_DST_AFFECTED

Syntax

![Description of ora_dst_affected.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ora_dst_affected.gif)  
[Description of the illustration
ora_dst_affected.eps](img_text/ora_dst_affected.md)

Purpose

`ORA_DST_AFFECTED` is useful when you are changing the time zone data file for
your database. The function takes as an argument a datetime expression that
resolves to a `TIMESTAMP` `WITH` `TIME` `ZONE` value or a `VARRAY` object that
contains `TIMESTAMP` `WITH` `TIME` `ZONE` values. The function returns `1` if
the datetime value is affected by or will result in a "nonexisting time" or
"duplicate time" error with the new time zone data. Otherwise, it returns 0.

This function can be issued only when changing the time zone data file of the
database and upgrading the timestamp with the time zone data, and only between
the execution of the `DBMS_DST`.`BEGIN_PREPARE` and the
`DBMS_DST`.`END_PREPARE` procedures or between the execution of the
`DBMS_DST`.`BEGIN_UPGRADE` and the `DBMS_DST`.`END_UPGRADE` procedures.

See Also:

[Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG259) for more information on time zone data files
and on how Oracle Database handles daylight saving time, and [Oracle Database
PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS234) for information on the `DBMS_DST` package


[← Previous](ORA_DM_PARTITION_NAME.md)

[Next →](ORA_DST_CONVERT.md)
