[Previous](CREATE-LOCKDOWN-PROFILE.md) [Next](CREATE-MATERIALIZED-VIEW.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE LOGICAL PARTITION TRACKING

## CREATE LOGICAL PARTITION TRACKING

Purpose

Use the `CREATE LOGICAL PARTITION TRACKING` statement to define a logical
partitioning scheme on a table for being leveraged by materialized views and
logical partition change tracking. You can define the logical partitions of
your tables independently of any existing or non-existing partitioning schema
of a table.

Syntax

create_logical_partition_tracking::=

  

![Description of create_logical_partition_tracking.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_logical_partition_tracking.gif)  
[Description of the illustration
create_logical_partition_tracking.eps](img_text/create_logical_partition_tracking.md)

  

Semantics

Logical partition tracking is supported on a single key column within the
table. The datatype of the key column can be of the following data types:
`NUMBER`, `DATE`, `CHAR`, `VARCHAR`, `VARCHAR2`, `TIMESTAMP`, `TIMSTAMP WITH
TIME ZONE`.

Only `RANGE` and `INTERVAL` logical partitions are supported on the base
table.

See Also:

  * [Refreshing Materialized Views](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG-GUID-63C94D8F-F9EB-4459-B360-E5231818E50A) of the Data Warehousing Guide. 


[← Previous](CREATE-LOCKDOWN-PROFILE.md)

[Next →](CREATE-MATERIALIZED-VIEW.md)
