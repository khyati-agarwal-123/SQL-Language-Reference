[Previous](SYS_OP_ZONE_ID.md) [Next](SYS_TYPEID.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. SYS_ROW_ETAG

## SYS_ROW_ETAG

Syntax

  

![Description of sys_row_etag.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/sys_row_etag.gif)  
[Description of the illustration sys_row_etag.eps](img_text/sys_row_etag.md)

  

Purpose

You can use `ETAG`s with table data, for lock-free row updates using SQL. To
do that, use function `SYS_ROW_ETAG`, to obtain the current state of a given
set of columns in a table row as an `ETAG` hash value. Function `SYS_ROW_ETAG`
calculates an etag (128 bits hash value) for a row using the values of a set
of columns in the row that you want the etag to be computed on. You can pass
the function the names of the columns in any order.

Function `SYS_ROW_ETAG` calculates the `ETAG` value for a row using only the
values of those columns in the row: you pass it the names of all columns that
you want to be sure no other session tries to update concurrently. This
includes the columns that the current session intends to update, but also any
other columns on whose value that updating operation logically depends for
your application. (The order in which you pass the columns to `SYS_ROW_ETAG`
as arguments is irrelevant.)

Example

The example below creates table `foo` with columns `c1`, `c2`, and `c3` of
type `NUMBER`, and inserts values into the table. It then passes columns `c2`
and `c1` to `SYS_ROW_ETAG` to get the etag for `c2` and `c1`:

    
    
    CREATE TABLE foo (c1 NUMBER, c2 NUMBER, c3 NUMBER);
    
    Table created.
    
    INSERT INTO foo VALUES (1, 2, 3);
    
    1 row created.
    
    SELECT SYS_ROW_ETAG(c2, c1) FROM foo;
    
    SYS_ROW_ETAG(C2,C1)
    --------------------------------
    3B978191AD0C828DA0E6A53EDF0B278A
    
    ---------------

See Also:

Example 4.18 in the JSON-Relational Duality Developer's Guide [Using Function
SYS_ROW_ETAG To Optimistically Control Concurrent Table
Updates](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=JSNVU-GUID-17DF3DA2-0302-43FC-AF49-78B417E09806)


[← Previous](SYS_OP_ZONE_ID.md)

[Next →](SYS_TYPEID.md)
