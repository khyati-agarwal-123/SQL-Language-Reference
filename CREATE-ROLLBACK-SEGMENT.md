[Previous](CREATE-ROLE.md) [Next](CREATE-SCHEMA.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE ROLLBACK SEGMENT 

## CREATE ROLLBACK SEGMENT

Note:

Oracle strongly recommends that you run your database in automatic undo
management mode instead of using rollback segments. Do not use rollback
segments unless you must do so for compatibility with earlier versions of
Oracle Database. Refer to [Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN013) for information on automatic undo management.

Purpose

Use the `CREATE ROLLBACK SEGMENT` statement to create a rollback segment,
which is an object that Oracle Database uses to store data necessary to
reverse, or undo, changes made by transactions.

The information in this section assumes that your database is not running in
automatic undo mode (the `UNDO_MANAGEMENT` initialization parameter is set to
`MANUAL` or not set at all). If your database is running in automatic undo
mode (the `UNDO_MANAGEMENT` initialization parameter is set to `AUTO`, which
is the default), then rollback segments are not permitted. However, errors
generated in rollback segment operations are suppressed.

Further, if your database has a locally managed `SYSTEM` tablespace, then you
cannot create rollback segments in any dictionary-managed tablespace. Instead,
you must either use the automatic undo management feature or create locally
managed tablespaces to hold the rollback segments.

Note:

A tablespace can have multiple rollback segments. Generally, multiple rollback
segments improve performance.

  * The tablespace must be online for you to add a rollback segment to it.

  * When you create a rollback segment, it is initially offline. To make it available for transactions by your Oracle Database instance, bring it online using the `ALTER ROLLBACK SEGMENT` statement. To bring it online automatically whenever you start up the database, add the segment name to the value of the `ROLLBACK_SEGMENT` initialization parameter. 

To use objects in a tablespace other than the `SYSTEM` tablespace:

  * If you are using rollback segments for undo, then at least one rollback segment (other than the `SYSTEM` rollback segment) must be online. 

  * If you are running the database in automatic undo mode, then at least one `UNDO` tablespace must be online. 

See Also:

  * [ALTER ROLLBACK SEGMENT](ALTER-ROLLBACK-SEGMENT.md#GUID-B25701E3-A074-44C4-9018-C6691BEB2483) for information on altering a rollback segment 

  * [DROP ROLLBACK SEGMENT](DROP-ROLLBACK-SEGMENT.md#GUID-26B4C9D6-EFB4-4523-B84D-FAD42060D3D4) for information on removing a rollback segment 

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN10224) for information on the `UNDO_MANAGEMENT` parameter 

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN013) for information on automatic undo mode 

Prerequisites

To create a rollback segment, you must have the `CREATE ROLLBACK SEGMENT`
system privilege.

Syntax

create_rollback_segment::=

![Description of create_rollback_segment.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_rollback_segment.gif)  
[Description of the illustration
create_rollback_segment.eps](img_text/create_rollback_segment.md)

([storage_clause](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15))

Semantics

PUBLIC

Specify `PUBLIC` to indicate that the rollback segment is public and is
available to any instance. If you omit this clause, then the rollback segment
is private and is available only to the instance naming it in its
initialization parameter `ROLLBACK_SEGMENTS`.

rollback_segment

Specify the name of the rollback segment to be created. The name must satisfy
the requirements listed in "[Database Object Naming Rules](Database-Object-
Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

TABLESPACE

Use the `TABLESPACE` clause to identify the tablespace in which the rollback
segment is created. If you omit this clause, then the database creates the
rollback segment in the `SYSTEM` tablespace.

Note:

Oracle Database must access rollback segments frequently. Therefore, Oracle
strongly recommends that you do not create rollback segments in the `SYSTEM`
tablespace, either explicitly or implicitly by omitting this clause. In
addition, to avoid high contention for the tablespace containing the rollback
segment, it should not contain other objects such as tables and indexes, and
it should require minimal extent allocation and deallocation.

To achieve these goals, create rollback segments in locally managed
tablespaces with autoallocation disabledâin tablespaces created with the
`EXTENT MANAGEMENT LOCAL` clause with the `UNIFORM` setting. The
`AUTOALLOCATE` setting is not supported.

See Also:

[CREATE TABLESPACE](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9)

storage_clause

The `storage_clause` lets you specify storage characteristics for the rollback
segment.

  * The `OPTIMAL` parameter of the `storage_clause` is of particular interest, because it applies only to rollback segments. 

  * You cannot specify the `PCTINCREASE` parameter of the `storage_clause` with `CREATE ROLLBACK SEGMENT`. 

See Also:

[storage_clause](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15)

Examples

Creating a Rollback Segment: Example

The following statement creates a rollback segment with default storage values
in an appropriately configured tablespace:

    
    
    CREATE TABLESPACE rbs_ts
       DATAFILE 'rbs01.dbf' SIZE 10M
       EXTENT MANAGEMENT LOCAL UNIFORM SIZE 100K;
    
    /* This example and the next will fail if your database is in 
       automatic undo mode.
    */
    CREATE ROLLBACK SEGMENT rbs_one
       TABLESPACE rbs_ts;
    

The preceding statement is equivalent to the following:

    
    
    CREATE ROLLBACK SEGMENT rbs_one
       TABLESPACE rbs_ts
       STORAGE
       ( INITIAL 10K );


[← Previous](CREATE-ROLE.md)

[Next →](CREATE-SCHEMA.md)
