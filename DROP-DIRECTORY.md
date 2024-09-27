[Previous](DROP-DIMENSION.md) [Next](DROP-DISKGROUP.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP DIRECTORY 

## DROP DIRECTORY

Purpose

Use the `DROP` `DIRECTORY` statement to remove a directory object from the
database.

See Also:

[CREATE DIRECTORY](CREATE-
DIRECTORY.md#GUID-8E9C569A-1B06-42C4-9586-0EF83437001A) for information on
creating a directory

Prerequisites

To drop a directory, you must have the `DROP` `ANY` `DIRECTORY` system
privilege.

Note:

Do not drop a directory when files in the associated file system are being
accessed by PL/SQL or OCI programs.

Syntax

drop_directory::=

![Description of drop_directory.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_directory.gif)  
[Description of the illustration
drop_directory.eps](img_text/drop_directory.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

directory_name

Specify the name of the directory database object to be dropped.

Oracle Database removes the directory object but does not delete the
associated operating system directory on the server file system.

Examples

Dropping a Directory: Example

The following statement drops the directory object `bfile_dir`:

    
    
    DROP DIRECTORY bfile_dir;

See Also:

"[Creating a Directory: Examples](CREATE-
DIRECTORY.md#GUID-8E9C569A-1B06-42C4-9586-0EF83437001A__I2092417)"


[← Previous](DROP-DIMENSION.md)

[Next →](DROP-DISKGROUP.md)
