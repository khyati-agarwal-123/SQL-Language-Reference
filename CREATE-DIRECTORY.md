[Previous](CREATE-DIMENSION.md) [Next](CREATE-DISKGROUP.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE DIRECTORY 

## CREATE DIRECTORY

Purpose

Use the `CREATE` `DIRECTORY` statement to create a directory object. A
directory object specifies an alias for a directory on the server file system
where external binary file LOBs (`BFILE`s) and external table data are
located. You can use directory names when referring to `BFILE`s in your PL/SQL
code and OCI calls, rather than hard coding the operating system path name,
for management flexibility.

All directories are created in a single namespace and are not owned by an
individual schema. You can secure access to the `BFILE`s stored within the
directory structure by granting object privileges on the directories to
specific users.

See Also:

  * "[Large Object (LOB) Data Types](Data-Types.md#GUID-1A71C635-188E-4EC9-B821-1DBEC2B45451)" for more information on `BFILE` objects 

  * [GRANT](GRANT.md#GUID-20B4E2C0-A7F8-4BC8-A5E8-BE61BDC41AC3) for more information on granting object privileges 

  * [external_table_clause::=](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2129649) of `CREATE` `TABLE`

Prerequisites

You must have the `CREATE` `ANY` `DIRECTORY` system privilege to create
directories.

When you create a directory, you are automatically granted the `READ`,
`WRITE`, and `EXECUTE` object privileges on the directory, and you can grant
these privileges to other users and roles. The DBA can also grant these
privileges to other users and roles.

`WRITE` privileges on a directory are useful in connection with external
tables. They let the grantee determine whether the external table agent can
write a log file or a bad file to the directory.

For file storage, you must also create a corresponding operating system
directory, an Oracle Automatic Storage Management (Oracle ASM) disk group, or
a directory within an Oracle ASM disk group. Your system or database
administrator must ensure that the operating system directory has the correct
read and write permissions for Oracle Database processes.

Privileges granted for the directory are created independently of the
permissions defined for the operating system directory, and the two may or may
not correspond exactly. For example, an error occurs if sample user `hr` is
granted `READ` privilege on the directory object but the corresponding
operating system directory does not have `READ` permission defined for Oracle
Database processes.

Restrictions

Symbolic links are not allowed in the directory object paths or filenames when
opening `BFILE` objects. The entire directory path and filename is checked and
the following error is returned if any symbolic link is found:

    
    
    ORA-22288: file or LOB operation FILEOPEN failed soft link in path
    

Workaround

If the database directory object or filename you are trying to open contains
symbolic links, change it to provide the real path and filename.

Syntax

create_directory::=

![Description of create_directory.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_directory.gif)  
[Description of the illustration
create_directory.eps](img_text/create_directory.md)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to re-create the directory database object if it
already exists. You can use this clause to change the definition of an
existing directory without dropping, re-creating, and regranting database
object privileges previously granted on the directory.

Users who had previously been granted privileges on a redefined directory can
still access the directory without being regranted the privileges.

See Also:

[DROP DIRECTORY](DROP-
DIRECTORY.md#GUID-3719950A-7B6A-4284-8467-B3455ECF8516) for information on
removing a directory from the database

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the directory does not exist, a new directory is created at the end of the statement.

  * If the directory exists, this is the directory you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

SHARING

This clause applies only when creating a directory in an application root.
This type of directory is called an application common object and it can be
shared with the application PDBs that belong to the application root. To
determine how the directory is shared, specify one of the following sharing
attributes:

  * `METADATA` \- A metadata link shares the directoryâs metadata, but its data is unique to each container. This type of directory is referred to as a metadata-linked application common object. 

  * `NONE` \- The directory is not shared. 

If you omit this clause, then the database uses the value of the
`DEFAULT_SHARING` initialization parameter to determine the sharing attribute
of the directory. If the `DEFAULT_SHARING` initialization parameter does not
have a value, then the default is `METADATA`.

You cannot change the sharing attribute of a directory after it is created.

See Also:

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN-GUID-15D1391E-7FAB-46A8-9F1F-9F59045B71EC) for more information on the `DEFAULT_SHARING` initialization parameter 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-388FB5AD-A2DE-4951-833B-A98239F99F50) for complete information on creating application common objects 

directory

Specify the name of the directory object to be created. The name must satisfy
the requirements listed in "[Database Object Naming Rules](Database-Object-
Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

Oracle Database does not verify that the directory you specify actually
exists. Therefore, take care that you specify a valid directory in your
operating system. In addition, if your operating system uses case-sensitive
path names, then be sure you specify the directory in the correct format. You
need not include a trailing slash at the end of the path name.

Do not refer to a parent directory in the directory name. For example, the
following syntax is valid:

    
    
    CREATE DIRECTORY mydir AS '/scratch/data/file_data';
    

However, the following syntax is not valid:

    
    
    CREATE DIRECTORY mydir AS '/scratch/../file_data';

path_name

Specify the full path name of the operating system directory of the server
where the files are located. The single quotation marks are required, with the
result that the path name is case sensitive.

Examples

Creating a Directory: Examples

The following statement creates a directory database object that points to a
directory on the server:

    
    
    CREATE DIRECTORY admin AS '/disk1/oracle/admin';
    

The following statement redefines directory database object `bfile_dir` to
enable access to `BFILE`s stored in the operating system directory
/`usr/bin/bfile_dir`:

    
    
    CREATE OR REPLACE DIRECTORY bfile_dir AS '/usr/bin/bfile_dir';


[← Previous](CREATE-DIMENSION.md)

[Next →](CREATE-DISKGROUP.md)
