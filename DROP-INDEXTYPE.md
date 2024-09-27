[Previous](DROP-INDEX.md) [Next](DROP-INMEMORY-JOIN-GROUP.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP INDEXTYPE 

## DROP INDEXTYPE

Purpose

Use the `DROP` `INDEXTYPE` statement to drop an indextype as well as any
association with a statistics type.

See Also:

[CREATE INDEXTYPE](CREATE-
INDEXTYPE.md#GUID-4A7BD0EC-B3E5-4D1D-95C5-C8B52D01D8CE) for more information
on indextypes

Prerequisites

The indextype must be in your own schema or you must have the `DROP` `ANY`
`INDEXTYPE` system privilege.

Syntax

drop_indextype::=

![Description of drop_indextype.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_indextype.gif)  
[Description of the illustration
drop_indextype.eps](img_text/drop_indextype.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the indextype. If you omit `schema`, then Oracle
Database assumes the indextype is in your own schema.

indextype

Specify the name of the indextype to be dropped.

If any statistics types have been associated with indextype, then the database
disassociates the statistics type from the indextype and drops any statistics
that have been collected using the statistics type.

See Also:

[ASSOCIATE STATISTICS](ASSOCIATE-STATISTICS.md#GUID-
BD02BA6A-32A7-4093-A6B6-BAE860C0F834) and [DISASSOCIATE
STATISTICS](DISASSOCIATE-
STATISTICS.md#GUID-6E9A7D93-E28A-469D-97AB-2BECC2EF3C43) for more
information on statistics associations

FORCE

Specify `FORCE` to drop the indextype even if the indextype is currently being
referenced by one or more domain indexes. Oracle Database marks those domain
indexes `INVALID`. Without `FORCE`, you cannot drop an indextype if any domain
indexes reference the indextype.

Examples

Dropping an Indextype: Example

The following statement drops the indextype `position_indextype`, created in
"[Using Extensible Indexing](Using-Extensible-Indexing.md#GUID-
BEAC690B-1FA4-4B31-9B28-FEAF45A01665)", and marks `INVALID` any domain indexes
defined on this indextype:

    
    
    DROP INDEXTYPE position_indextype FORCE;


[← Previous](DROP-INDEX.md)

[Next →](DROP-INMEMORY-JOIN-GROUP.md)
