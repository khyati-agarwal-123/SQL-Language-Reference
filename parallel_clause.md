[Previous](logging_clause.md) [Next](physical_attributes_clause.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Common SQL DDL Clauses ](Common-SQL-DDL-Clauses.md)
  3. parallel_clause

## parallel_clause

Purpose

The `parallel_clause` lets you parallelize the creation of a database object
and set the default degree of parallelism for subsequent queries of and DML
operations on the object.

You can specify the `parallel_clause` in the following statements:

  * `CREATE` `TABLE`: to set parallelism for the table (see [CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6)). 

  * `ALTER` `TABLE` (see [ALTER TABLE](ALTER-TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877)): 

    * To change parallelism for the table

    * To parallelize the operations of adding, coalescing, exchanging, merging, splitting, truncating, dropping, or moving a table partition

  * `CREATE` `CLUSTER` and `ALTER` `CLUSTER`: to set or alter parallelism for a cluster (see [CREATE CLUSTER](CREATE-CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7) and [ALTER CLUSTER](ALTER-CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D)). 

  * `CREATE` `INDEX`: to set parallelism for the index (see [CREATE INDEX](CREATE-INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE)). 

  * `ALTER` `INDEX` (see [ALTER INDEX](ALTER-INDEX.md#GUID-D8F648E7-8C07-4C89-BB71-862512536558)): 

    * To change parallelism for the index

    * To parallelize the rebuilding of the index or the splitting of an index partition

  * `CREATE` `MATERIALIZED` `VIEW`: to set parallelism for the materialized view (see [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B)). 

  * `ALTER` `MATERIALIZED` `VIEW` (see [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233)): 

    * To change parallelism for the materialized view

    * To parallelize the operations of adding, coalescing, exchanging, merging, splitting, truncating, dropping, or moving a materialized view partition

    * To parallelize the operations of adding or moving materialized view subpartitions

  * `CREATE` `MATERIALIZED` `VIEW` `LOG`: to set parallelism for the materialized view log (see [CREATE MATERIALIZED VIEW LOG](CREATE-MATERIALIZED-VIEW-LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B)). 

  * `ALTER` `MATERIALIZED` `VIEW` `LOG` (see [ALTER MATERIALIZED VIEW LOG](ALTER-MATERIALIZED-VIEW-LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627)): 

    * To change parallelism for the materialized view log

    * To parallelize the operations of adding, coalescing, exchanging, merging, splitting, truncating, dropping, or moving a materialized view log partition

  * `ALTER` `DATABASE` ... `RECOVER`: to recover the database (see [ALTER DATABASE](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986)). 

  * `ALTER` `DATABASE` ... `standby_database_clauses`: to parallelize operations on the standby database (see [ALTER DATABASE](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986)). 

See Also:

[Oracle Database PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS233) for information on the `DBMS_PARALLEL_EXECUTE`
package, which provides methods to apply table changes in chunks of rows.
Changes to each chunk are independently committed when there are no errors.

Syntax

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

Semantics

This section describes the semantics of the `parallel_clause`. For additional
information, refer to the SQL statement in which you set or reset parallelism
for a particular database object or operation.

Note:

The syntax of the `parallel_clause` supersedes syntax appearing in earlier
releases of Oracle. The superseded syntax is still supported for backward
compatibility, but may result in slightly different behavior from that
documented.

The database interprets the `parallel_clause` based on the setting of the
`PARALLEL_DEGREE_POLICY` initialization parameter. When that parameter is set
to `AUTO`, the `parallel_clause` is ignored entirely, and the optimizer
determines the best degree of parallelism for all statements. When
`PARALLEL_DEGREE_POLICY` is set to either `MANUAL` or `LIMITED`, the
`parallel_clause` is interpreted as follows:

NOPARALLEL

Specify `NOPARALLEL` for serial execution. This is the default.

PARALLEL

Specify `PARALLEL` for parallel execution.

  * If `PARALLEL_DEGREE_POLICY` is set to `MANUAL`, then the optimizer calculates a degree of parallelism equal to the number of CPUs available on all participating instances times the value of the `PARALLEL_THREADS_PER_CPU` initialization parameter. 

  * If `PARALLEL_DEGREE_POLICY` is set to `LIMITED`, then the optimizer determines the best degree of parallelism. 

PARALLEL integer

Specification of `integer` indicates the degree of parallelism, which is the
number of parallel threads used in the parallel operation. Each parallel
thread may use one or two parallel execution servers.

Notes on the parallel_clause

The following notes apply to the `parallel_clause`:

  * Parallelism is disabled for DML operations on tables on which you have defined a trigger or referential integrity constraint.

  * Parallelism is not supported for `UPDATE` or `DELETE` operations on index-organized tables. 

  * When you specify the `parallel_clause` during creation of a table, if the table contains any columns of LOB or user-defined object type, then subsequent `INSERT`, `UPDATE`, `DELETE` or `MERGE` operations that modify the LOB or object type column are executed serially without notification. Subsequent queries, however, will be executed in parallel. 

  * A parallel hint overrides the effect of the `parallel_clause`. 

  * DML statements and `CREATE` `TABLE` ... `AS` `SELECT` statements that reference remote objects can run in parallel. However, the remote object must really be on a remote database. The reference cannot loop back to an object on the local database, for example, by way of a synonym on the remote database pointing back to an object on the local database. 

  * DML operations on tables with LOB columns can be parallelized. However, intrapartition parallelism is not supported.

See Also:

[Oracle Database VLDB and Partitioning
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=VLDBG010) for more information on parallelized
operations, and "[Creating a Table: Parallelism Examples](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2153163)"


[← Previous](logging_clause.md)

[Next →](physical_attributes_clause.md)
