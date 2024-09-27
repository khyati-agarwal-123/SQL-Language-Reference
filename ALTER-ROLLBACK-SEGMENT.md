[Previous](ALTER-ROLE.md) [Next](ALTER-SEQUENCE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER ROLLBACK SEGMENT 

## ALTER ROLLBACK SEGMENT

Note:

Oracle strongly recommends that you run your database in automatic undo
management mode instead of using rollback segments. Do not use rollback
segments unless you must do so for compatibility with earlier versions of
Oracle Database. Refer to [Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN013) for information on automatic undo management.

Purpose

Use the `ALTER ROLLBACK SEGMENT` statement to bring a rollback segment online
or offline, change its storage characteristics, or shrink it to an optimal or
specified size.

This section assumes that your database is running in rollback undo mode (the
`UNDO_MANAGEMENT` initialization parameter is set to `MANUAL` or not set at
all). If your database is running in automatic undo mode (the
`UNDO_MANAGEMENT` initialization parameter is set to `AUTO`, which is the
default), then user-created rollback segments are irrelevant.

See Also:

  * [CREATE ROLLBACK SEGMENT](CREATE-ROLLBACK-SEGMENT.md#GUID-14AE3104-5B33-4E53-8E6F-6B2F037B52E9) for information on creating a rollback segment 

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN10224) for information on the `UNDO_MANAGEMENT` parameter 

Prerequisites

You must have the `ALTER ROLLBACK SEGMENT` system privilege.

Syntax

alter_rollback_segment::=

![Description of alter_rollback_segment.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_rollback_segment.gif)  
[Description of the illustration
alter_rollback_segment.eps](img_text/alter_rollback_segment.md)

([storage_clause](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15),
[size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

Semantics

rollback_segment

Specify the name of an existing rollback segment.

ONLINE

Specify `ONLINE` to bring the rollback segment online. When you create a
rollback segment, it is initially offline and not available for transactions.
This clause brings the rollback segment online, making it available for
transactions by your instance. You can also bring a rollback segment online
when you start your instance with the initialization parameter
`ROLLBACK_SEGMENTS`.

See Also:

"[Bringing a Rollback Segment Online: Example](ALTER-ROLLBACK-
SEGMENT.md#GUID-B25701E3-A074-44C4-9018-C6691BEB2483__CCHHDICB)"

OFFLINE

Specify `OFFLINE` to take the rollback segment offline.

  * If the rollback segment does not contain any information needed to roll back an active transaction, then Oracle Database takes it offline immediately.

  * If the rollback segment does contain information for active transactions, then the database makes the rollback segment unavailable for future transactions and takes it offline after all the active transactions are committed or rolled back.

When the rollback segment is offline, it can be brought online by any
instance.

To see whether a rollback segment is online or offline, query `STATUS` column
of the data dictionary view `DBA_ROLLBACK_SEGS`. Online rollback segments have
a value of `IN_USE`. Offline rollback segments have a value of `AVAILABLE`.

Restriction on Taking Rollback Segments Offline

You cannot take the `SYSTEM` rollback segment offline.

storage_clause

Use the `storage_clause` to change the storage characteristics of the rollback
segment.

Restrictions on Rollback Segment Storage

You cannot change the value of `INITIAL` parameter. If the rollback segment is
in a locally managed tablespace, then the only storage parameter you can
change is `OPTIMAL`. If the rollback segment is in a dictionary-managed
tablespace, then the only storage parameters you can change are `NEXT`,
`MINEXTENTS`, `MAXEXTENTS` and `OPTIMAL`.

See Also:

[storage_clause](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15)
for syntax and additional information

SHRINK Clause

Specify `SHRINK` if you want Oracle Database to attempt to shrink the rollback
segment to an optimal or specified size. The success and amount of shrinkage
depend on the available free space in the rollback segment and how active
transactions are holding space in the rollback segment.

If you do not specify `TO` `size_clause`, then the size defaults to the
`OPTIMAL` value of the `storage_clause` of the `CREATE ROLLBACK SEGMENT`
statement that created the rollback segment. If `OPTIMAL` was not specified,
then the size defaults to the `MINEXTENTS` value of the `storage_clause` of
the `CREATE ROLLBACK SEGMENT` statement.

Regardless of whether you specify `TO` `size_clause`:

  * The value to which Oracle Database shrinks the rollback segment is valid for the execution of the statement. Thereafter, the size reverts to the `OPTIMAL` value of the `CREATE ROLLBACK SEGMENT` statement. 

  * The rollback segment cannot shrink to less than two extents.

To determine the actual size of a rollback segment after attempting to shrink
it, query the `BYTES`, `BLOCKS`, and `EXTENTS` columns of the `DBA_SEGMENTS`
view.

Restriction on Shrinking Rollback Segments

In an Oracle Real Application Clusters environment, you can shrink only
rollback segments that are online to your instance.

See Also:

[size_clause](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517) for
information on that clause, and "[Resizing a Rollback Segment: Example](ALTER-
ROLLBACK-SEGMENT.md#GUID-B25701E3-A074-44C4-9018-C6691BEB2483__CCHDICDB)"

Examples

The following examples use the `rbs_one` rollback segment, which was created
in "[Creating a Rollback Segment: Example](CREATE-ROLLBACK-
SEGMENT.md#GUID-14AE3104-5B33-4E53-8E6F-6B2F037B52E9__CCHIHJDF)".

Bringing a Rollback Segment Online: Example

This statement brings the rollback segment `rbs_one` online:

    
    
    ALTER ROLLBACK SEGMENT rbs_one ONLINE; 

Resizing a Rollback Segment: Example

This statement shrinks the rollback segment `rbs_one`:

    
    
    ALTER ROLLBACK SEGMENT rbs_one 
       SHRINK TO 100M;


[← Previous](ALTER-ROLE.md)

[Next →](ALTER-SEQUENCE.md)
