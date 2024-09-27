[Previous](DROP-INDEXTYPE.md) [Next](DROP-JAVA.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP INMEMORY JOIN GROUP

## DROP INMEMORY JOIN GROUP

Purpose

Use the `DROP` `INMEMORY` `JOIN` `GROUP` statement to remove a join group from
the database.

See Also:

  * [CREATE INMEMORY JOIN GROUP](CREATE-INMEMORY-JOIN-GROUP.md#GUID-87CA7034-4F80-4D46-8EE1-5CC865C2D676) and [ALTER INMEMORY JOIN GROUP](ALTER-INMEMORY-JOIN-GROUP.md#GUID-AF24F413-BB14-4B5D-93BF-9EB31ACFEBEC)

  * [Oracle Database In-Memory Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=INMEM-GUID-3E5491C4-B345-4A8E-8B1B-8DC150C8A797) for more information on join groups 

Prerequisites

If the join group is in another userâs schema, then you must have the `DROP`
`ANY` `TABLE` system privilege.

Syntax

drop_inmemory_join_group::=

![Description of drop_inmemory_join_group.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_inmemory_join_group.gif)  
[Description of the illustration
drop_inmemory_join_group.eps](img_text/drop_inmemory_join_group.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the join group. If you omit `schema`, then the
database assumes the join group is in your own schema.

join_group

Specify the name of the join group to be dropped.

You can view existing join groups by querying the `DBA_JOINGROUPS` or
`USER_JOINGROUPS` data dictionary view. Refer to [Oracle Database
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN-GUID-285814BC-3BE0-47DA-8832-779229D5A93A) for more
information on these views.

Examples

The following statement drops the join group `prod_id1`:

    
    
    DROP INMEMORY JOIN GROUP prod_id1;


[← Previous](DROP-INDEXTYPE.md)

[Next →](DROP-JAVA.md)
