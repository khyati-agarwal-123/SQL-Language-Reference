[Previous](DROP-TABLESPACE.md) [Next](DROP-TRIGGER.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: DROP TABLE to LOCK TABLE](SQL-Statements-DROP-TABLE-to-LOCK-TABLE.md)
  3. DROP TABLESPACE SET

## DROP TABLESPACE SET

Note:

This SQL statement is valid only if you are using Oracle Sharding. For more
information on Oracle Sharding, refer to [Oracle Database Administratorâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-DE8AF949-9F68-4C0C-9B5A-45401EF3C3D1).

Purpose

Use the `DROP` `TABLESPACE` `SET` statement to drop a tablespace set from a
shardgroup.

When you drop a tablespace set, Oracle Database does not place it in the
recycle bin. Therefore, you cannot subsequently either purge or undrop the
tablespace set.

See Also:

[CREATE TABLESPACE SET](CREATE-TABLESPACE-
SET.md#GUID-877951F1-B2A5-4907-9F0F-EF4F1884E8C4) and [ALTER TABLESPACE
SET](ALTER-TABLESPACE-SET.md#GUID-63FEDE73-C1F1-4B7A-98ED-8C34C4073549)

Prerequisites

You must be connected to a shard catalog database as an SDB user.

You must have the `DROP` `TABLESPACE` system privilege. You cannot drop a
tablespace set if its tablespaces contain any rollback segments holding active
transactions.

Syntax

drop_tablespace_set::=

![Description of drop_tablespace_set.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_tablespace_set.gif)  
[Description of the illustration
drop_tablespace_set.eps](img_text/drop_tablespace_set.md)

Semantics

tablespace_set

Specify the name of the tablespace set to be dropped.

INCLUDING CONTENTS

This clause lets you specify how the database manages objects and datafiles
associated with the tablespaces in the tablespace set during the drop
operation. The `INCLUDING` `CONTENTS` clause has the same semantics here as
for the `DROP` `TABLESPACE` statement. See [INCLUDING CONTENTS](DROP-
TABLESPACE.md#GUID-C91F3E94-4503-48DE-9BCA-42E495E6BE11__INCLUDINGCONTENTSINCLUDINGCONTENTSC-44AF7912)
for the full semantics of this clause.

Examples

Dropping a Tablespace Set: Example

The following statement drops the tablespace set `ts1`:

    
    
    DROP TABLESPACE SET ts1;


[← Previous](DROP-TABLESPACE.md)

[Next →](DROP-TRIGGER.md)
