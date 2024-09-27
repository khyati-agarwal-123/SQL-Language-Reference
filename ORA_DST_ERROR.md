[Previous](ORA_DST_CONVERT.md) [Next](ORA_HASH.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ORA_DST_ERROR 

## ORA_DST_ERROR

Syntax

![Description of ora_dst_error.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ora_dst_error.gif)  
[Description of the illustration
ora_dst_error.eps](img_text/ora_dst_error.md)

Purpose

`ORA_DST_ERROR` is useful when you are changing the time zone data file for
your database. The function takes as an argument a datetime expression that
resolves to a `TIMESTAMP` `WITH` `TIME` `ZONE` value or a `VARRAY` object that
contains `TIMESTAMP` `WITH` `TIME` `ZONE` values, and indicates whether the
datetime value will result in an error with the new time zone data. The return
values are:

  * `0`: the datetime value does not result in an error with the new time zone data. 

  * `1878`: the datetime value results in a "nonexisting time" error. 

  * `1883`: the datetime value results in a "duplicate time" error. 

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


[← Previous](ORA_DST_CONVERT.md)

[Next →](ORA_HASH.md)
