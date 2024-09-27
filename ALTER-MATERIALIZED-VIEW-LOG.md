[Previous](ALTER-MATERIALIZED-VIEW.md) [Next](ALTER-MATERIALIZED-
ZONEMAP.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER MATERIALIZED VIEW LOG 

## ALTER MATERIALIZED VIEW LOG

Purpose

A materialized view log is a table associated with the master table of a
materialized view. Use the `ALTER` `MATERIALIZED` `VIEW` `LOG` statement to
alter the storage characteristics or type of an existing materialized view
log.

Note:

The keyword `SNAPSHOT` is supported in place of `MATERIALIZED` `VIEW` for
backward compatibility.

See Also:

  * [CREATE MATERIALIZED VIEW LOG](CREATE-MATERIALIZED-VIEW-LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B) for information on creating a materialized view log 

  * [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233) for more information on materialized views, including refreshing them 

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) for a description of the various types of materialized views 

Prerequisites

You must be the owner of the master table, or you must have the `READ` or
`SELECT` privilege on the master table and the `ALTER` privilege on the
materialized view log.

See Also:

[Oracle Database Administratorâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-6F0523A6-D710-46D9-A683-2E692882E2BB) for
detailed information about the prerequisites for `ALTER` `MATERIALIZED` `VIEW`
`LOG`

Syntax

alter_materialized_view_log::=

![Description of alter_materialized_view_log.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_materialized_view_log.gif)  
[Description of the illustration
alter_materialized_view_log.eps](img_text/alter_materialized_view_log.md)

([physical_attributes_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__I2227013),
[add_mv_log_column_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__BGBGEHEA),
[alter_table_partitioning::=](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2087440) (in `ALTER`
`TABLE`), [parallel_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__I2282424),
[logging_clause::=](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E__CJAHABGF),
[allocate_extent_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__I2227029),
[shrink_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__I2283763),
[move_mv_log_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__BGBECHCA),
[mv_log_augmentation::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__BGBBCDCJ),
[mv_log_purge_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__BGBHFAHE),
[for_refresh_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__CCHCDEHJ))

physical_attributes_clause::=

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

[storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB)

add_mv_log_column_clause::=

![Description of add_mv_log_column_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_mv_log_column_clause.gif)  
[Description of the illustration
add_mv_log_column_clause.eps](img_text/add_mv_log_column_clause.md)

allocate_extent_clause::=

![Description of allocate_extent_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/allocate_extent_clause.gif)  
[Description of the illustration
allocate_extent_clause.eps](img_text/allocate_extent_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

shrink_clause::=

![Description of shrink_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/shrink_clause.gif)  
[Description of the illustration
shrink_clause.eps](img_text/shrink_clause.md)

move_mv_log_clause::=

![Description of move_mv_log_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/move_mv_log_clause.gif)  
[Description of the illustration
move_mv_log_clause.eps](img_text/move_mv_log_clause.md)

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

mv_log_augmentation::=

![Description of mv_log_augmentation.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mv_log_augmentation.gif)  
[Description of the illustration
mv_log_augmentation.eps](img_text/mv_log_augmentation.md)

([new_values_clause::=](ALTER-MATERIALIZED-VIEW-
LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__I2227005)

new_values_clause::=

![Description of new_values_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/new_values_clause.gif)  
[Description of the illustration
new_values_clause.eps](img_text/new_values_clause.md)

mv_log_purge_clause::=

![Description of mv_log_purge_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/mv_log_purge_clause.gif)  
[Description of the illustration
mv_log_purge_clause.eps](img_text/mv_log_purge_clause.md)

for_refresh_clause::=

![Description of for_refresh_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/for_refresh_clause.gif)  
[Description of the illustration
for_refresh_clause.eps](img_text/for_refresh_clause.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

FORCE

If you specify `FORCE` and any items specified with the `ADD` clause have
already been specified for the materialized view log, then Oracle Database
does not return an error, but silently ignores the existing elements and adds
to the materialized view log any items that do not already exist in the log.
Likewise, if you specify `INCLUDING` `NEW` `VALUES` and that attribute has
already been specified for the materialized view log, Oracle Database ignores
the redundancy and does not return an error.

schema

Specify the schema containing the master table. If you omit `schema`, then
Oracle Database assumes the materialized view log is in your own schema.

table

Specify the name of the master table associated with the materialized view log
to be altered.

physical_attributes_clause

The `physical_attributes_clause` lets you change the value of the `PCTFREE`,
`PCTUSED`, and `INITRANS` parameters and the storage characteristics for the
materialized view log, the partition, the overflow data segment, or the
default characteristics of a partitioned materialized view log.

Restriction on Materialized View Log Physical Attributes

You cannot use the `storage_clause` to modify extent parameters if the
materialized view log resides in a locally managed tablespace. Refer to
[CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6)
for a description of these parameters.

add_mv_log_column_clause

When you add a column to the master table of the materialized view log, the
database does not automatically add a column to the materialized view log.
Therefore, use this clause to add a column to the materialized view log.
Oracle Database will encrypt the newly added column if the corresponding
column of the master table is encrypted.

alter_table_partitioning

The syntax and general functioning of the partitioning clauses is the same as
described for the `ALTER` `TABLE` statement. Refer to
[alter_table_partitioning](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2085640) in the
documentation on `ALTER` `TABLE`.

Restrictions on Altering Materialized View Log Partitions

Altering materialized view log partitions is subject to the following
restrictions:

  * You cannot use the `LOB_storage_clause` or `modify_LOB_storage_clause` when modifying partitions of a materialized view log. 

  * If you attempt to drop, truncate, or exchange a materialized view log partition, then Oracle Database raises an error.

parallel_clause

The `parallel_clause` lets you specify whether parallel operations will be
supported for the materialized view log.

For complete information on this clause, refer to [parallel_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) in the
documentation on `CREATE` `TABLE`.

logging_clause

Specify the logging attribute of the materialized view log. Refer to the
[logging_clause](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E)
for a full description of this clause.

allocate_extent_clause

Use the `allocate_extent_clause` to explicitly allocate a new extent for the
materialized view log. Refer to
[allocate_extent_clause](allocate_extent_clause.md#GUID-
DA6B3DC2-84B5-4404-AD96-5ABF7341580F) for a full description of this clause.

shrink_clause

Use this clause to compact the materialized view log segments. For complete
information on this clause, refer to [shrink_clause](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2192484) in the
documentation on `CREATE` `TABLE`.

move_mv_log_clause

Use the `MOVE` clause to move the materialized view log table to a different
tablespace, to change other segment or storage attributes of the materialized
view log, or to change the parallelism of the materialized view log.

Restriction on Moving Materialized View Logs

The `ENCRYPT` clause of the `storage_clause` of `segment_attributes` is not
valid for materialized view logs.

CACHE | NOCACHE Clause

For data that will be accessed frequently, `CACHE` specifies that the blocks retrieved for this log are placed at the most recently used end of the LRU list in the buffer cache when a full table scan is performed. This attribute is useful for small lookup tables. `NOCACHE` specifies that the blocks are placed at the least recently used end of the LRU list. Refer to "[CACHE | NOCACHE | CACHE READS](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2215507)" in the documentation on `CREATE` `TABLE` for more information about this clause. 

mv_log_augmentation

Use the `ADD` clause to augment the materialized view log so that it records
the primary key values, rowid values, object ID values, or a sequence when
rows in the materialized view master table are changed. This clause can also
be used to record additional columns.

To stop recording any of this information, you must first drop the
materialized view log and then re-create it. Dropping the materialized view
log and then re-creating it forces a complete refresh for each of the existing
materialized views that depend on the master table on its next refresh.

Restriction on Augmenting Materialized View Logs

You can specify only one `PRIMARY` `KEY`, one `ROWID`, one `OBJECT` `ID`, one
`SEQUENCE`, and each column in the column list once for each materialized view
log. You can specify only a single occurrence of `PRIMARY` `KEY`, `ROWID`,
`OBJECT` `ID`, `SEQUENCE`, and column list within this `ALTER` statement.
Also, if any of these values was specified at create time (either implicitly
or explicitly), you cannot specify that value in this `ALTER` statement unless
you use the `FORCE` option.

OBJECT ID

Specify `OBJECT` `ID` if you want the appropriate object identifier of all
rows that are changed to be recorded in the materialized view log.

Restriction on the OBJECT ID clause

You can specify `OBJECT` `ID` only for logs on object tables, and you cannot
specify it for storage tables.

PRIMARY KEY

Specify `PRIMARY` `KEY` if you want the primary key values of all rows that
are changed to be recorded in the materialized view log.

ROWID

Specify `ROWID` if you want the rowid values of all rows that are changed to
be recorded in the materialized view log.

SEQUENCE

Specify `SEQUENCE` to indicate that a sequence value providing additional
ordering information should be recorded in the materialized view log.

column

Specify the additional columns whose values you want to be recorded in the
materialized view log for all rows that are changed. Typically these columns
are filter columns (non-primary-key columns referenced by subquery
materialized views) and join columns (non-primary-key columns that define a
join in the `WHERE` clause of the subquery).

See Also:

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) for details on explicit and implicit inclusion of materialized view log values 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-EA4C8CD8-51E2-4C3B-8281-210940D8DE01) for more information about filter columns and join columns 

  * "[Rowid Materialized View Log: Example](ALTER-MATERIALIZED-VIEW-LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__I2227231)"

NEW VALUES Clause

The `NEW` `VALUES` clause lets you specify whether Oracle Database saves both
old and new values for update DML operations in the materialized view log. The
value you set in this clause applies to all columns in the log, not only to
columns you may have added in this `ALTER` `MATERIALIZED` `VIEW` `LOG`
statement.

INCLUDING

Specify `INCLUDING` to save both new and old values in the log. If this log is
for a table on which you have a single-table materialized aggregate view, and
if you want the materialized view to be eligible for fast refresh, then you
must specify `INCLUDING`.

EXCLUDING

Specify `EXCLUDING` to disable the recording of new values in the log. You can
use this clause to avoid the overhead of recording new values.

If you have a fast-refreshable single-table materialized aggregate view
defined on this table, then do not specify `EXCLUDING` `NEW` `VALUES` unless
you first change the refresh mode of the materialized view to something other
than `FAST`.

See Also:

"[Materialized View Log EXCLUDING NEW VALUES: Example](ALTER-MATERIALIZED-
VIEW-LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627__I2227235)"

mv_log_purge_clause

Use this clause alter the purge attributes of the materialized view log in the
following ways:

  * Change the purge from `IMMEDIATE` `SYNCHRONOUS` to `IMMEDIATE` `ASYNCHRONOUS` or from `IMMEDIATE` `ASYNCHRONOUS` to `IMMEDIATE` `SYNCHRONOUS`

  * Change the purge from `IMMEDIATE` to scheduled or from scheduled to `IMMEDIATE`

  * Specify a new start time and a new `next` time and `interval`

If you are altering purge from scheduled to `IMMEDIATE`, then the scheduled
purged job associated with that materialized view log is dropped. If you are
altering purge from `IMMEDIATE` to scheduled, then a purge job is created with
the attributes provided. If you are altering scheduled purge attributes, then
only those attributes specified will be changed in the scheduler purge job.

You must specify `FORCE` if you are altering log purge to its current state
(that is, you are not making any change), unless you are changing scheduled
purge attributes.

To learn whether the purge time or interval has already been set for this
materialized view log, query the `*_MVIEW_LOGS` data dictionary views. See the
`CREATE` `MATERIALIZED` `VIEW` `LOG` clause [mv_log_purge_clause](CREATE-
MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__CACCJBFD) for the full
semantics of this clause.

for_refresh_clause

Use this clause to change the refresh method for which the materialized view
log will be used.

FOR SYNCHRONOUS REFRESH

Specify this clause to change from fast refresh to synchronous refresh, or
complete refresh to synchronous refresh. A staging log will be created.

If you are changing from fast refresh, then ensure that the following
conditions are satisfied before using this clause:

  * All changes in the materialized view log have been consumed.

  * Any refresh-on-demand materialized views associated with the master table have been refreshed.

  * Any refresh-on-commit materialized views associated with the master table have been converted to refresh-on-demand materialized views.

After you use this clause, you cannot perform DML operations directly on the
master table. You must use the procedures in the `DBMS_SYNC_REFRESH` package
to prepare and execute change data operations.

FOR FAST REFRESH

Specify this clause to change from synchronous refresh to fast refresh, or
complete refresh to fast refresh. A materialized view log will be created.

If you are changing from synchronous refresh to fast refresh, then ensure that
all changes in the staging log have been consumed before using this clause.

After you use this clause, you can perform DML operations directly on the
master table.

See the `CREATE` `MATERIALIZED` `VIEW` `LOG` clause
[for_refresh_clause](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__CCHIHIEB) for the full
semantics of this clause.

Examples

Rowid Materialized View Log: Example

The following statement alters an existing primary key materialized view log
to also record rowid information:

    
    
    ALTER MATERIALIZED VIEW LOG ON order_items ADD ROWID;

Materialized View Log EXCLUDING NEW VALUES: Example

The following statement alters the materialized view log on `hr.employees` by
adding a filter column and excluding new values. Any materialized aggregate
views that use this log will no longer be fast refreshable. However, if fast
refresh is no longer needed, this action avoids the overhead of recording new
values:

    
    
    ALTER MATERIALIZED VIEW LOG ON employees
       ADD (commission_pct)
       EXCLUDING NEW VALUES;


[← Previous](ALTER-MATERIALIZED-VIEW.md)

[Next →](ALTER-MATERIALIZED-ZONEMAP.md)
