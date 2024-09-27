[Previous](DROP-CONTEXT.md) [Next](DROP-DATABASE-LINK.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP DATABASE 

## DROP DATABASE

Purpose

Note:

You cannot roll back a `DROP` `DATABASE` statement.

Use the `DROP` `DATABASE` statement to drop the database. This statement is
useful when you want to drop a test database or drop an old database after
successful migration to a new host.

You can issue `DROP` `DATABASE` on True Cache to delete all the files that
belong to this True Cache. The command only deletes files that belong to this
True Cache. You must have started up the True Cache in mount mode.

See Also:

[Oracle Database Backup and Recovery User's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV89641) for more information on dropping the database

Prerequisites

You must have the `SYSDBA` system privilege to issue this statement. The
database must be mounted in exclusive and restricted mode, and it must be
closed.

Syntax

drop_database::=

![Description of drop_database.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_database.gif)  
[Description of the illustration
drop_database.eps](img_text/drop_database.md)

Semantics

When you issue this statement, Oracle Database drops the database and deletes
all control files and data files listed in the control file. If the database
used a server parameter file (spfile), then the spfile is also deleted.

Archived logs and backups are not removed, but you can use Recovery Manager
(RMAN) to remove them. If the database is on raw disks, then this statement
does not delete the actual raw disk special files.

Drop True Cache

To drop the True Cache using `DROP` `DATABASE` you must mount the database and
set restricted mode as follows:

    
    
    STARTUP MOUNT
    ALTER SYSTEM ENABLE RESTRICTED SESSION;
    DROP DATABASE


[← Previous](DROP-CONTEXT.md)

[Next →](DROP-DATABASE-LINK.md)
