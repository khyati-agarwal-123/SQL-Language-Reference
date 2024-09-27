[Previous](DROP-MATERIALIZED-VIEW.md) [Next](DROP-MATERIALIZED-ZONEMAP.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP MATERIALIZED VIEW LOG 

## DROP MATERIALIZED VIEW LOG

Purpose

Use the `DROP` `MATERIALIZED` `VIEW` `LOG` statement to remove a materialized
view log from the database.

Note:

The keyword `SNAPSHOT` is supported in place of `MATERIALIZED` `VIEW` for
backward compatibility.

See Also:

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) and [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233) for more information on materialized views 

  * [CREATE MATERIALIZED VIEW LOG](CREATE-MATERIALIZED-VIEW-LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B) for information on materialized view logs 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REPLN-GUID-A422B474-4BED-4A60-AEDB-E93630746083) for information on materialized views in a replication environment 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG008) for information on materialized views in a data warehousing environment 

Prerequisites

To drop a materialized view log, you must have the privileges needed to drop a
table.

See Also:

[DROP TABLE](DROP-TABLE.md#GUID-39D89EDC-155D-4A24-837E-D45DDA757B45)

Syntax

drop_materialized_view_log::=

![Description of drop_materialized_view_log.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_materialized_view_log.gif)  
[Description of the illustration
drop_materialized_view_log.eps](img_text/drop_materialized_view_log.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the materialized view log and its master table.
If you omit `schema`, then Oracle Database assumes the materialized view log
and master table are in your own schema.

table

Specify the name of the master table associated with the materialized view log
to be dropped.

After you drop a materialized view log that was created `FOR` `FAST`
`REFRESH`, some materialized views based on the materialized view log master
table can no longer be fast refreshed. These materialized views include rowid
materialized views, primary key materialized views, and subquery materialized
views.

See Also:

[Oracle Database Data Warehousing Guide
](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG008)for a description of these types of materialized
views

After you drop a materialized view log that was created `FOR` `SYNCHRONOUS`
`REFRESH` (a staging log), the materialized views based on the staging log
master table can no longer be synchronous refreshed.

Examples

Dropping a Materialized View Log: Example

The following statement drops the materialized view log on the `oe.customers`
master table:

    
    
    DROP MATERIALIZED VIEW LOG ON customers; 


[← Previous](DROP-MATERIALIZED-VIEW.md)

[Next →](DROP-MATERIALIZED-ZONEMAP.md)
