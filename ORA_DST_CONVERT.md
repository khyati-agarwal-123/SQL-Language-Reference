[Previous](ORA_DST_AFFECTED.md) [Next](ORA_DST_ERROR.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. ORA_DST_CONVERT 

## ORA_DST_CONVERT

Syntax

![Description of ora_dst_convert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/ora_dst_convert.gif)  
[Description of the illustration
ora_dst_convert.eps](img_text/ora_dst_convert.md)

Purpose

`ORA_DST_CONVERT` is useful when you are changing the time zone data file for
your database. The function lets you specify error handling for a specified
datetime expression.

  * For `datetime_expr`, specify a datetime expression that resolves to a `TIMESTAMP` `WITH` `TIME` `ZONE` value or a `VARRAY` object that contains `TIMESTAMP` `WITH` `TIME` `ZONE` values. 

  * The optional second argument specifies handling of "duplicate time" errors. Specify `0` (false) to suppress the error by returning the source datetime value. This is the default. Specify `1` (true) to allow the database to return the duplicate time error. 

  * The optional third argument specifies handling of "nonexisting time" errors. Specify `0` (false) to suppress the error by returning the source datetime value. This is the default. Specify `1` (true) to allow the database to return the nonexisting time error. 

If no error occurs, this function returns a value of the same data type as
`datetime_expr` (a `TIMESTAMP` `WITH` `TIME` `ZONE` value or a `VARRAY` object
that contains `TIMESTAMP` `WITH` `TIME` `ZONE` values). The returned datetime
value when interpreted with the new time zone file corresponds to
`datetime_expr` interpreted with the old time zone file.

This function can be issued only when changing the time zone data file of the
database and upgrading the timestamp with the time zone data, and only between
the execution of the `DBMS_DST`.`BEGIN_UPGRADE` and the
`DBMS_DST`.`END_UPGRADE` procedures.

See Also:

[Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG259) for more information on time zone data files
and on how Oracle Database handles daylight saving time, and [Oracle Database
PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS234) for information on the `DBMS_DST` package


[← Previous](ORA_DST_AFFECTED.md)

[Next →](ORA_DST_ERROR.md)
