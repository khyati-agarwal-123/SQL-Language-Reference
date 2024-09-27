[Previous](DROP-LOCKDOWN-PROFILE.md) [Next](DROP-MATERIALIZED-VIEW-LOG.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP MATERIALIZED VIEW

## DROP MATERIALIZED VIEW

Purpose

Use the `DROP` `MATERIALIZED` `VIEW` statement to remove an existing
materialized view from the database.

When you drop a materialized view, Oracle Database does not place it in the
recycle bin. Therefore, you cannot subsequently either purge or undrop the
materialized view.

Note:

The keyword `SNAPSHOT` is supported in place of `MATERIALIZED` `VIEW` for
backward compatibility.

See Also:

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) for more information on the various types of materialized views 

  * [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233) for information on modifying a materialized view 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-A422B474-4BED-4A60-AEDB-E93630746083) for information on materialized views in a replication environment 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG008) for information on materialized views in a data warehousing environment 

Prerequisites

The materialized view must be in your own schema or you must have the `DROP`
`ANY` `MATERIALIZED` `VIEW` system privilege. You must also have the
privileges to drop the internal table, views, and index that the database uses
to maintain the materialized view data.

See Also:

[DROP TABLE](DROP-TABLE.md#GUID-39D89EDC-155D-4A24-837E-D45DDA757B45), [DROP
VIEW](DROP-VIEW.md#GUID-1A1BD841-66B9-47E4-896F-D36E075AE296), and [DROP
INDEX](DROP-INDEX.md#GUID-F60F75DF-2866-4F93-BB7F-8FCE64BF67B6) for
information on privileges required to drop objects that the database uses to
maintain the materialized view

Syntax

drop_materialized_view::=

![Description of drop_materialized_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_materialized_view.gif)  
[Description of the illustration
drop_materialized_view.eps](img_text/drop_materialized_view.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the materialized view. If you omit `schema`,
then Oracle Database assumes the materialized view is in your own schema.

materialized_view

Specify the name of the existing materialized view to be dropped.

  * If you drop a simple materialized view that is the least recently refreshed materialized view of a master table, then the database automatically purges from the master table materialized view log only the rows needed to refresh the dropped materialized view. 

  * If you drop a materialized view that was created on a prebuilt table, then the database drops the materialized view, and the prebuilt table reverts to its identity as a table.

  * When you drop a master table, the database does not automatically drop materialized views based on the table. However, the database returns an error when it tries to refresh a materialized view based on a master table that has been dropped. 

  * If you drop a materialized view, then any compiled requests that were rewritten to use the materialized view will be invalidated and recompiled automatically. If the materialized view was prebuilt on a table, then the table is not dropped, but it can no longer be maintained by the materialized view refresh mechanism.

PRESERVE TABLE Clause

This clause lets you retain the materialized view container table and its
contents after the materialized view object is dropped. The resulting table
has the same name as the dropped materialized view.

Oracle Database removes all metadata associated with the materialized view.
However, indexes created on the container table automatically during creation
of the materialized view are preserved, with one exception: the index created
during the creation of a rowid materialized view is dropped. Also, if the
materialized view has any nested table columns, then the storage tables for
those columns are preserved, along with their metadata.

Restriction on the PRESERVE TABLE Clause

This clause is not valid for materialized views that have been imported from
releases earlier than Oracle9i, when these objects were called "snapshots".

Examples

Dropping a Materialized View: Examples

The following statement drops the materialized view `emp_data` in the sample
schema `hr`:

    
    
    DROP MATERIALIZED VIEW emp_data; 
    

The following statement drops the `sales_by_month_by_state` materialized view
and the underlying table of the materialized view, unless the underlying table
was registered in the `CREATE` `MATERIALIZED` `VIEW` statement with the `ON`
`PREBUILT` `TABLE` clause:

    
    
    DROP MATERIALIZED VIEW sales_by_month_by_state;


[← Previous](DROP-LOCKDOWN-PROFILE.md)

[Next →](DROP-MATERIALIZED-VIEW-LOG.md)
