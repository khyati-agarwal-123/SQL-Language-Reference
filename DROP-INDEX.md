[Previous](DROP-HIERARCHY.md) [Next](DROP-INDEXTYPE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP INDEX

## DROP INDEX

Purpose

Use the `DROP` `INDEX` statement to remove an index or domain index from the
database.

When you drop a global partitioned index, a range-partitioned index, or a
hash-partitioned index, all the index partitions are also dropped. If you drop
a composite-partitioned index, then all the index partitions and subpartitions
are also dropped.

In addition, when you drop a domain index:

  * Oracle Database invokes the appropriate routine. 

  * If any statistics are associated with the domain index, then Oracle Database disassociates the statistics types with the `FORCE` clause and removes the user-defined statistics collected with the statistics type. 

See Also:

    * [Oracle Database Data Cartridge Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADDCI4200) for information on the routines 

    * [CREATE INDEX](CREATE-INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE) and [ALTER INDEX](ALTER-INDEX.md#GUID-D8F648E7-8C07-4C89-BB71-862512536558) for information on creating and modifying an index 

    * The `domain_index_clause` of [CREATE INDEX](CREATE-INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE) for more information on domain indexes 

    * [ASSOCIATE STATISTICS](ASSOCIATE-STATISTICS.md#GUID-BD02BA6A-32A7-4093-A6B6-BAE860C0F834) and [DISASSOCIATE STATISTICS](DISASSOCIATE-STATISTICS.md#GUID-6E9A7D93-E28A-469D-97AB-2BECC2EF3C43) for more information on statistics type associations 

Prerequisites

The index must be in your own schema or you must have the `DROP` `ANY` `INDEX`
system privilege.

Syntax

drop_index::=

![Description of drop_index.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_index.gif)  
[Description of the illustration drop_index.eps](img_text/drop_index.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the index. If you omit `schema`, then Oracle
Database assumes the index is in your own schema.

index

Specify the name of the index to be dropped. When the index is dropped, all
data blocks allocated to the index are returned to the tablespace that
contained the index.

ONLINE

Specify `ONLINE` to indicate that DML operations on the table or partition
will be allowed while dropping the index.

FORCE

`FORCE` applies only to domain indexes. This clause drops the domain index
even if the indextype routine invocation returns an error or the index is
marked `IN` `PROGRESS`. Without `FORCE`, you cannot drop a domain index if its
indextype routine invocation returns an error or the index is marked `IN`
`PROGRESS`.

Note:

When dropping a domain index with `FORCE` option, the index will be dropped
regardless of any errors happening in the indextype routine. The errors raised
by the indextype routine are not reported.

Only use the `FORCE` option when the index or index partitions are marked `IN
PROGRESS` or when `DROP INDEX` has already failed.

{ DEFERRED | IMMEDIATE } INVALIDATION

This clause lets you control when the database invalidates dependent cursors
while dropping the index. It has the same semantics here as for the `ALTER`
`INDEX` statement, with the following addition: When you drop an index with
`DEFERRED` `INVALIDATION`, Oracle database will immediately invalidate any DML
statement or query that references the dropped index in its plan.

See [{ DEFERRED | IMMEDIATE } INVALIDATION](ALTER-INDEX.md#GUID-D8F648E7-8C07-4C89-BB71-862512536558__DEFERREDIMMEDIATEINVALIDATION-42A7C77E) in the documentation on `ALTER` `INDEX` for the full semantics of this clause. 

Restrictions on Dropping Indexes

The following restrictions apply to dropping indexes:

  * You cannot drop a domain index if the index or any of its index partitions is marked `IN_PROGRESS`. 

  * You cannot specify the `ONLINE` clause when dropping a domain index, a cluster index, or an index on a queue table. 

Examples

Dropping an Index: Example

This statement drops an index named `ord_customer_ix_demo`, which was created
in "[Compressing an Index: Example](CREATE-
INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE__I2129467)":

    
    
    DROP INDEX ord_customer_ix_demo;


[← Previous](DROP-HIERARCHY.md)

[Next →](DROP-INDEXTYPE.md)
