[Previous](CREATE-MATERIALIZED-VIEW.md) [Next](CREATE-MATERIALIZED-
ZONEMAP.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE MATERIALIZED VIEW LOG 

## CREATE MATERIALIZED VIEW LOG

Purpose

Use the `CREATE` `MATERIALIZED` `VIEW` `LOG` statement to create a
materialized view log, which is a table associated with the master table of a
materialized view.

Note:

The keyword `SNAPSHOT` is supported in place of `MATERIALIZED` `VIEW` for
backward compatibility.

Materialized view logs are used for two types of materialized view refreshes:
fast refresh and synchronous refresh.

Fast refresh uses a conventional materialized view log. During a fast refresh
(also called an incremental refresh), when DML changes are made to master
table data, Oracle Database stores rows describing those changes in the
materialized view log and then uses the materialized view log to refresh
materialized views based on the master table.

Synchronous refresh uses a special type of materialized view log called a
staging log. During a synchronous refresh, DML changes are first described in
the staging log and then applied to the master tables and the materialized
views simultaneously. This guarantees that the master table data and
materialized view data are in sync throughout the refresh process. This
refresh method is useful in data warehousing environments.

Without a materialized view log, Oracle Database must reexecute the
materialized view query to refresh the materialized view. This process is
called a complete refresh. Usually, a complete refresh takes more time to
complete than a fast refresh or a synchronous refresh.

A materialized view log is located in the master database in the same schema
as the master table. A master table can have only one materialized view log
defined on it.

To fast refresh or synchronous refresh a materialized join view, you must
create a materialized view log for each of the tables referenced by the
materialized view.

Fast refresh supports two types of materialized view logs: timestamp-based
materialized view logs and commit SCN-based materialized view logs. Timestamp-
based materialized view logs use timestamps and require some setup operations
when preparing to refresh the materialized view. Commit SCN-based materialized
view logs use commit SCN data rather than timestamps, which removes the need
for the setup operations and thus can improve the speed of the materialized
view refresh. If you specify the `COMMIT` `SCN` clause, then a commit SCN-
based materialized view log is created. Otherwise, a time-stamp based
materialized view log is created. Note that only new materialized view logs
can take advantage of `COMMIT` `SCN`. Existing materialized view logs cannot
be altered to add `COMMIT` `SCN` unless they are dropped and recreated. Refer
to [Oracle Database Data Warehousing
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG0319) for more information.

Synchronous refresh supports only timestamp-based staging logs.

See Also:

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B), [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233), [Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT411), [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG008), and [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-A422B474-4BED-4A60-AEDB-E93630746083) for information on materialized views in general 

  * [ALTER MATERIALIZED VIEW LOG](ALTER-MATERIALIZED-VIEW-LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627) for information on modifying a materialized view log 

  * [DROP MATERIALIZED VIEW LOG](DROP-MATERIALIZED-VIEW-LOG.md#GUID-878A08F7-CB95-4911-BE2E-9FEED8861410) for information on dropping a materialized view log 

  * [Oracle Database Utilities](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SUTIL003) for information on using direct loader logs 

Prerequisites

The privileges required to create a materialized view log directly relate to
the privileges necessary to create the underlying objects associated with a
materialized view log.

  * If you own the master table, then you can create an associated materialized view log if you have the `CREATE` `TABLE` privilege. 

  * If you are creating a materialized view log for a table in another user's schema, then you must have the `CREATE` `ANY` `TABLE` and `COMMENT` `ANY` `TABLE` system privileges, as well as either the `READ` or `SELECT` object privilege on the master table or the `READ` `ANY` `TABLE` or `SELECT` `ANY` `TABLE` system privilege. 

In either case, the owner of the materialized view log must have sufficient
quota in the tablespace intended to hold the materialized view log or must
have the `UNLIMITED` `TABLESPACE` system privilege.

See Also:

[Oracle Database Data Warehousing
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG008) for more information about the prerequisites
for creating a materialized view log

Restrictions

The statement `CREATE MATERIALIZED VIEW LOG` does not support the following
columns in the Master Table:

  * Hidden columns

  * Identity columns

  * `BFILE` columns 

  * Temporal validity columns

Syntax

create_materialized_vw_log::=

![Description of create_materialized_vw_log.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_materialized_vw_log.gif)  
[Description of the illustration
create_materialized_vw_log.eps](img_text/create_materialized_vw_log.md)

([physical_attributes_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116626), [logging_clause::=](CREATE-
MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2117068),
[parallel_clause::=](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2116510),
[table_partitioning_clauses::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2129707) (in `CREATE`
`TABLE`), [new_values_clause::=](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2117146),
[mv_log_purge_clause::=](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__CACBGACI),
[for_refresh_clause::=](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__CCHGAFBA).)

physical_attributes_clause::=

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB)``)

logging_clause::=

![Description of logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logging_clause.gif)  
[Description of the illustration
logging_clause.eps](img_text/logging_clause.md)

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

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

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the materialized view log does not exist, a new materialized view log is created at the end of the statement.

  * If the materialized view log exists, this is the materialized view log you have at the end of the statement. A new one is not created because the older materialized view log is detected.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement.`

schema

Specify the schema containing the materialized view log master table. If you
omit `schema`, then Oracle Database assumes the master table is contained in
your own schema. Oracle Database creates the materialized view log in the
schema of its master table. You cannot create a materialized view log for a
table in the schema of the user `SYS`.

table

Specify the name of the master table for which the materialized view log is to
be created. Oracle Database encrypts any columns in the materialized view log
that are encrypted in the master table, using the same encryption algorithm.

Restrictions on Master Tables of Materialized View Logs

The following restrictions apply to master tables of materialized view logs:

  * You cannot create a materialized view log for a temporary table or for a view. 

  * You cannot create a materialized view log for a master table with a virtual column.

See Also:

"[Creating a Materialized View Log for Fast Refresh: Examples](CREATE-
MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2098404)"

SHARING

Use the sharing clause if you want to create the object in an application root
in the context of an application maintenance. This type of object is called an
application common object and it can be shared with the application PDBs that
belong to the application root.

You can specify how the object is shared using one of the following sharing
attributes:

  * `METADATA` \- A metadata link shares the metadata, but its data is unique to each container. This type of object is referred to as a metadata-linked application common object. 

  * `NONE` \- The object is not shared and can only be accessed in the application root. 

physical_attributes_clause

Use the `physical_attributes_clause` to define physical and storage
characteristics for the materialized view log.

See Also:

[physical_attributes_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393)
and
[storage_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393__I1026834)
for a complete description these clauses, including default values

TABLESPACE Clause

Specify the tablespace in which the materialized view log is to be created. If
you omit this clause, then the database creates the materialized view log in
the default tablespace of the schema of the materialized view log.

logging_clause

Specify either `LOGGING` or `NOLOGGING` to establish the logging
characteristics for the materialized view log. The default is the logging
characteristic of the tablespace in which the materialized view log resides.

See Also:

[logging_clause](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E)
for a full description of this clause

CACHE | NOCACHE

For data that will be accessed frequently, `CACHE` specifies that the blocks
retrieved for this log are placed at the most recently used end of the least
recently used (LRU) list in the buffer cache when a full table scan is
performed. This attribute is useful for small lookup tables.

`NOCACHE` specifies that the blocks are placed at the least recently used end
of the LRU list. The default is `NOCACHE`.

Note:

`NOCACHE` has no effect on materialized view logs for which you specify `KEEP`
in the `storage_clause`.

See Also:

[CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6)
for information about specifying `CACHE` or `NOCACHE`

parallel_clause

The `parallel_clause` lets you indicate whether parallel operations will be
supported for the materialized view log.

For complete information on this clause, refer to [parallel_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) in the
documentation on `CREATE` `TABLE`.

table_partitioning_clauses

Use the `table_partitioning_clauses` to indicate that the materialized view
log is partitioned on specified ranges of values or on a hash function.
Partitioning of materialized view logs is the same as partitioning of tables.

See Also:

[table_partitioning_clauses](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2215406) in the `CREATE
TABLE` documentation

WITH Clause

Use the `WITH` clause to indicate whether the materialized view log should
record the primary key, rowid, object ID, or a combination of these row
identifiers when rows in the master are changed. You can also use this clause
to add a sequence to the materialized view log to provide additional ordering
information for its records.

This clause also specifies whether the materialized view log records
additional columns that might be referenced as filter columns, which are non-
primary-key columns referenced by subquery materialized views, or join
columns, which are non-primary-key columns that define a join in the subquery
`WHERE` clause.

If you omit this clause, or if you specify the clause without `PRIMARY` `KEY`,
`ROWID`, or `OBJECT` `ID`, then the database stores primary key values by
default. However, the database does not store primary key values implicitly if
you specify only `OBJECT` `ID` or `ROWID` at create time. A primary key log,
created either explicitly or by default, performs additional checking on the
primary key constraint.

OBJECT ID

Specify `OBJECT` `ID` to indicate that the system-generated or user-defined
object identifier of every modified row should be recorded in the materialized
view log.

Restriction on OBJECT ID

You can specify `OBJECT` `ID` only when creating a log on an object table, and
you cannot specify it for storage tables.

PRIMARY KEY

Specify `PRIMARY` `KEY` to indicate that the primary key of all rows changed
should be recorded in the materialized view log.

ROWID

Specify `ROWID` to indicate that the rowid of all rows changed should be
recorded in the materialized view log.

SEQUENCE

Specify `SEQUENCE` to indicate that a sequence value providing additional
ordering information should be recorded in the materialized view log. Sequence
numbers are necessary to support fast refresh after some update scenarios.

See Also:

[Oracle Database Data Warehousing
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG008) for more information on the use of sequence
numbers in materialized view logs and for examples that use this clause

COMMIT SCN

Without the `COMMIT` `SCN` clause, the materialized view log is based on
timestamps and requires some setup operations when preparing to refresh the
materialized view. Specify `COMMIT` `SCN` to instruct the database to use
commit SCN data rather than timestamps. This setting removes the need for the
setup operations and thus can improve the speed of the materialized view
refresh.

You can create the following types of local materialized views (including both
`ON` `COMMIT` and `ON` `DEMAND`) on master tables with commit SCN-based
materialized view logs:

  * Materialized aggregate views, including materialized aggregate views on a single table

  * Materialized join views

  * Primary-key-based and rowid-based single table materialized views

  * `UNION` `ALL` materialized views, where each `UNION` `ALL` branch is one of the above materialized view types 

You cannot create remote materialized views on master tables with commit SCN-
based materialized view logs.

Restrictions on COMMIT SCN

The following restrictions apply to `COMMIT` `SCN`:

  * Use of `COMMIT` `SCN` on a table with one or more LOB columns is not supported and causes `ORA-32421`. 

  * Creating a materialized view on master tables with different types of materialized view logs (that is, a master table with timestamp-based materialized view logs and a master table with commit SCN-based materialized view logs) is not supported and causes `ORA-32414`. 

  * If you specify `COMMIT` `SCN`, then you cannot specify `FOR` `SYNCHRONOUS` `REFRESH`. 

column

Specify the columns whose values you want to be recorded in the materialized
view log for all rows that are changed. Typically these columns are filter
columns and join columns.

Restrictions on the WITH Clause

This clause is subject to the following restrictions:

  * You can specify only one `PRIMARY` `KEY`, one `ROWID`, one `OBJECT` `ID`, one `SEQUENCE`, and one column list for each materialized view log. 

  * Primary key columns are implicitly recorded in the materialized view log. Therefore, you cannot specify any of the following combinations if `column` contains one of the primary key columns: 
    
        WITH ... PRIMARY KEY ... (column)
    WITH ... (column) ... PRIMARY KEY
    WITH (column)

See Also:

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) for information on explicit and implicit inclusion of materialized view log values 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-EA4C8CD8-51E2-4C3B-8281-210940D8DE01) for more information about filter columns and join columns 

  * "[Specifying Filter Columns for Materialized View Logs: Example](CREATE-MATERIALIZED-VIEW-LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2098358)" and "[Specifying Join Columns for Materialized View Logs: Example](CREATE-MATERIALIZED-VIEW-LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2098379)"

NEW VALUES Clause

The `NEW` `VALUES` clause lets you determine whether Oracle Database saves
both old and new values for update DML operations in the materialized view
log.

See Also:

"[Including New Values in Materialized View Logs: Example](CREATE-
MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2119924)"

INCLUDING

Specify `INCLUDING` to save both new and old values in the log. If this log is
for a table on which you have a single-table materialized aggregate view, and
if you want the materialized view to be eligible for fast refresh, then you
must specify `INCLUDING`.

EXCLUDING

Specify `EXCLUDING` to disable the recording of new values in the log. This is
the default. You can use this clause to avoid the overhead of recording new
values. Do not use this clause if you have a fast-refreshable single-table
materialized aggregate view defined on the master table.

mv_log_purge_clause

Use this clause to specify the purge time for the materialized view log.

  * `IMMEDIATE` `SYNCHRONOUS`: the materialized view log is purged immediately after refresh. This is the default. 

  * `IMMEDIATE` `ASYNCHRONOUS`: the materialized view log is purged in a separate Oracle Scheduler job after the refresh operation. 

  * `START` `WITH`, `NEXT`, and `REPEAT` `INTERVAL` set up a scheduled purge that is independent of the materialized view refresh and is initiated during `CREATE` or `ALTER` `MATERIALIZED` `VIEW` `LOG` statement. This is very similar to scheduled refresh syntax in a `CREATE` or `ALTER` `MATERIALIZED` `VIEW` statement: 

    * The `START` `WITH` datetime expression specifies when the purge starts. 

    * The `NEXT` datetime expression computes the next run time for the purge. 

If you specify `REPEAT` `INTERVAL`, then the next run time will be: `SYSDATE
+` `interval_expr`.

A `CREATE` `MATERIALIZED` `VIEW` `LOG` statement with a scheduled purge
creates an Oracle Scheduler job to perform log purge. The job calls the
`DBMS_SNAPSHOT`.`PURGE_LOG` procedure to purge the materialized view logs.
This process allows you to amortize the purging costs over several
materialized view refreshes.

Restriction on mv_log_purge_clause

This clause is not valid for materialized view logs on temporary tables.

See Also:

[Oracle Database Data Warehousing
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG9302) for more information on purging materialized
view logs

for_refresh_clause

Use this clause to specify the refresh method for which the materialized view
log will be used. You can specify only one refresh method for any given master
table.

FOR SYNCHRONOUS REFRESH

Specify this clause to create a staging log that can be used for synchronous
refresh. Use `staging_log_name` to specify the name of the staging log to be
created. The staging log will be created in the schema in which the master
table resides.

After you create the staging log, you cannot perform DML operations directly
on the master table. You must use the procedures in the `DBMS_SYNC_REFRESH`
package to prepare and execute change data operations.

Restrictions on Synchronous Refresh

The following restrictions apply to synchronous refresh:

  * If you specify `FOR` `SYNCHRONOUS` `REFRESH`, then you cannot specify `COMMIT` `SCN`. 

  * To be eligible for synchronous refresh, the master table must satisfy the following criteria:

    * If the master table is a fact table, then it must be partitioned.

    * The master table must have a key. If the master table is a dimension table, then it must have a primary key defined on it. If the master table is a fact table, then the set of columns that are the foreign keys of the dimension tables joined to the fact table are deemed to be the key.

    * The master table cannot have a non-NULL Virtual Private Database (VPD) policy or a trigger defined on it.

Oracle Database may allow you to create a staging log on a master table even
if all of the preceding criteria are not met. However, the master table will
not be eligible for synchronous refresh.

  * Any existing materialized views on the master table must be refresh-on-demand materialized views. If an existing materialized view is a refresh-on-commit materialized view, then you must change it to a refresh-on-demand materialized view with the [alter_mv_refresh](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226546) clause of `ALTER` `MATERIALIZED` `VIEW` before you create the staging log. 

See Also:

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG029) for the complete steps for using synchronous refresh 

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS73623) for information on the `DBMS_SYNC_REFRESH` package 

FOR FAST REFRESH

Specify this clause to create a materialized view log that can be used for
fast refresh. The materialized view log will be created in the same schema in
which the master table resides. This is the default.

Examples

Creating a Materialized View Log for Fast Refresh: Examples

The following statement creates a materialized view log on the `oe.customers`
table that specifies physical and storage characteristics:

    
    
    CREATE MATERIALIZED VIEW LOG ON customers
       PCTFREE 5 
       TABLESPACE example 
       STORAGE (INITIAL 10K);
    

The materialized view log on `customers` supports fast refresh for primary key
materialized views only.

The following statement creates another version of the materialized view log
with the `ROWID` clause, which enables fast refresh for more types of
materialized views:

    
    
    CREATE MATERIALIZED VIEW LOG ON customers WITH PRIMARY KEY, ROWID;
    

This materialized view log on `customers` makes fast refresh possible for
rowid materialized views and for materialized join views. To provide for fast
refresh of materialized aggregate views, you must also specify the `SEQUENCE`
and `INCLUDING` `NEW` `VALUES` clauses, as shown in the example that follows.

Specify a Purge Repeat Interval for a Materialized View Log: Example

The following statement creates a materialized view log on the `oe.orders`
table. The contents of the log will be purged once every five days, beginning
five days after the creation date of the materialized view log:

    
    
    CREATE MATERIALIZED VIEW LOG ON orders
      PCTFREE 5
      TABLESPACE example
      STORAGE (INITIAL 10K)
      PURGE REPEAT INTERVAL '5' DAY;

Specifying Filter Columns for Materialized View Logs: Example

The following statement creates a materialized view log on the `sh.sales`
table and is used in "[Creating Materialized Aggregate Views: Example](CREATE-
MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2092102)".
It specifies as filter columns all of the columns of the table referenced in
that materialized view.

    
    
    CREATE MATERIALIZED VIEW LOG ON sales 
       WITH ROWID, SEQUENCE(amount_sold, time_id, prod_id)
       INCLUDING NEW VALUES; 

Specifying Join Columns for Materialized View Logs: Example

The following statement creates a materialized view log on the `order_items`
table of the sample `oe` schema. The log records primary keys and
`product_id`, which is used as a join column in "[Creating a Fast Refreshable
Materialized View: Example](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2080820)".

    
    
    CREATE MATERIALIZED VIEW LOG ON order_items WITH (product_id);

Including New Values in Materialized View Logs: Example

The following example creates a materialized view log on the
`oe.product_information` table that specifies `INCLUDING` `NEW` `VALUES`:

    
    
    CREATE MATERIALIZED VIEW LOG ON product_information 
       WITH ROWID, SEQUENCE (list_price, min_price, category_id), PRIMARY KEY
       INCLUDING NEW VALUES;
    

You could create the following materialized aggregate view to use the
`product_information` log:

    
    
    CREATE MATERIALIZED VIEW products_mv 
       REFRESH FAST ON COMMIT
       AS SELECT SUM(list_price - min_price), category_id
             FROM product_information 
             GROUP BY category_id;
    

This materialized view is eligible for fast refresh because the log defined on
its master table includes both old and new values.

Creating a Staging Log for Synchronous Refresh: Example

The following statement creates a staging log on the `sh.sales` fact table.
The staging log is named `mystage_log` and is stored in the `sh` schema. It
can be used for synchronous refresh.

    
    
    CREATE MATERIALIZED VIEW LOG ON sales
       PCTFREE 5 
       TABLESPACE example 
       STORAGE (INITIAL 10K)
       FOR SYNCHRONOUS REFRESH USING mystage_log;
    


[← Previous](CREATE-MATERIALIZED-VIEW.md)

[Next →](CREATE-MATERIALIZED-ZONEMAP.md)
