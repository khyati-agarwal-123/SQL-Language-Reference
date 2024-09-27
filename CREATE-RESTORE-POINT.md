[Previous](create-property-graph.md) [Next](CREATE-ROLE.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE RESTORE POINT 

## CREATE RESTORE POINT

Purpose

Use the `CREATE` `RESTORE` `POINT` statement to create a restore point, which
is a name associated with a timestamp or an SCN of the database. A restore
point can be used to flash back a table or the database to the time specified
by the restore point without the need to determine the SCN or timestamp.
Restore points are also useful in various RMAN operations, including backups
and database duplication. You can use RMAN to create restore points in the
process of implementing an archival backup.

See Also:

  * Oracle Database Backup and Recovery User's Guide for more information on [creating and using restore points and guaranteed restore points](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV589), for information on [database duplication](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV010), and for information on [archival backups](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV89551)

  * [FLASHBACK DATABASE](FLASHBACK-DATABASE.md#GUID-BE0ACF9A-BC13-4810-B08B-33326440258B), [FLASHBACK TABLE](FLASHBACK-TABLE.md#GUID-FA9AF2FD-2DAD-4387-9E62-14AFC26EA85C), and [DROP RESTORE POINT](DROP-RESTORE-POINT.md#GUID-5FC039A9-46C8-4604-8985-C29CB617798C) for information on using and dropping restore points 

Prerequisites

To create a normal restore point, you must have the `SELECT` `ANY`
`DICTIONARY`, `FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG`
system privilege.

To create a guaranteed restore point, you must fulfill one of the following
conditions:

  * You must connect `AS SYSDBA`, or ` AS SYSBACKUP`, or `AS SYSDG`. 

  * You must have been granted the `SYSDBA` privilege and be using a multitenant database. 

  * You must be running as user `SYS`, and be using a a multitenant database. 

To view or use a restore point, you must have the `SELECT` `ANY` `DICTIONARY`,
`FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege
or the `SELECT_CATALOG_ROLE` role.

You can create a restore point on a primary or standby database. The database
can be open, or mounted but not open. If the database is mounted, then it must
have been shut down consistently before being mounted unless it is a physical
standby database.

You must have created a fast recovery area before creating a guaranteed
restore point. You need not enable flashback database before you create the
guaranteed restore point. The database must be in `ARCHIVELOG` mode if you are
creating a guaranteed restore point.

You need not enable flashback database before you create a normal restore
point, because normal restore points have other applications besides
`FLASHBACK DATABASE`. However, you would need to have enabled flashback
database before you create a normal restore point, if you intend to perform a
`FLASHBACK DATABASE` to that normal restore point.

You can create, use, or view a restore point when connected to a multitenant
container database (CDB) as follows:

  * To create a normal CDB restore point, the current container must be the root and you must have the `SELECT` `ANY` `DICTIONARY` or `FLASHBACK` `ANY` `TABLE` system privilege, either granted commonly or granted locally in the root, or the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly. 

  * To create a guaranteed CDB restore point, the current container must be the root and you must have the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly. 

  * To view a CDB restore point, the current container must be the root and you must have the `SELECT` `ANY` `DICTIONARY` or `FLASHBACK` `ANY` `TABLE` system privilege or the `SELECT_CATALOG_ROLE` role, either granted commonly or granted locally in the root, or the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly, or the current container must be a PDB and you must have the `SELECT` `ANY` `DICTIONARY`, `FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly or granted locally in that PDB. 

  * To use a CDB restore point, you must have the `SELECT` `ANY` `DICTIONARY` or `FLASHBACK` `ANY` `TABLE` system privilege or the `SELECT_CATALOG_ROLE` role, either granted commonly or granted locally in the root, or the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly. 

  * To create a normal PDB restore point, the current container must be the root and you must have the `SELECT` `ANY` `DICTIONARY` or `FLASHBACK` `ANY` `TABLE` system privilege, either granted commonly or granted locally in the root, or the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly, or the current container must be the PDB for which you want to create the restore point and you must have the `SELECT` `ANY` `DICTIONARY`, `FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly or granted locally in that PDB. 

  * To create a guaranteed PDB restore point, the current container must be the root and you must have the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly, or the current container must be the PDB for which you want to create the restore point and you must have the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly or granted locally in that PDB. 

  * To view a PDB restore point, the current container must be the root and you must have the `SELECT` `ANY` `DICTIONARY` or `FLASHBACK` `ANY` `TABLE` system privilege or the `SELECT_CATALOG_ROLE` role, either granted commonly or granted locally in the root, or the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly, or the current container must be the PDB for the restore point and you must have the `SELECT` `ANY` `DICTIONARY`, `FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly or granted locally in that PDB. 

  * To use a PDB restore point, the current container must be the PDB for the restore point and you must have the `SELECT` `ANY` `DICTIONARY`, `FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly or granted locally in that PDB. 

Syntax

create_restore_point::=

![Description of create_restore_point.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_restore_point.gif)  
[Description of the illustration
create_restore_point.eps](img_text/create_restore_point.md)

Semantics

CLEAN

You can specify `CLEAN` only when creating a PDB restore point. The PDB must
use shared undo and must be closed with no outstanding transactions. Flashing
back a PDB using shared undo to a clean PDB restore point does not require
restoring backups or creating a clone instance. Therefore, it is faster than
flashing back a PDB using shared undo to an SCN or other type of restore
point.

restore_point

Specify the name of the restore point. The name must satisfy the requirements
listed in "[Database Object Naming Rules](Database-Object-Names-and-
Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

In a multitenant environment, the CDB and PDBs have their own namespaces for
restore points. Therefore, the CDB and each PDB can have a restore point with
the same name. When you specify a restore point name in a PDB or for a PDB
operation, the name is first interpreted as a PDB restore point for the
concerned PDB. If a PDB restore point with the specified name is not found,
then it is interpreted as a CDB restore point.

The database can retain at least 2048 normal restore points. In a Multitenant
environment, a CDB can retain at least 2048 normal restore points across the
entire CDB, including PDB restore points. Normal restore points are retained
in the database for at least the number of days specified for the
`CONTROL_FILE_RECORD_KEEP_TIME` initialization parameter. The default value of
that parameter is 7 days. Guaranteed restore points are retained in the
database until explicitly dropped by the user.

If you specify neither `PRESERVE` nor `GUARANTEE FLASHBACK DATABASE`, then the
resulting restore point enables you to flash the database back to a restore
point within the time period determined by the `DB_FLASHBACK_RETENTION_TARGET`
initialization parameter. The database automatically manages such restore
points. When the maximum number of restore points is reached, according to the
rules described in `restore_point` above, the database automatically drops the
oldest restore point. Under some circumstances the restore points will be
retained in the RMAN recovery catalog for use in restoring long-term backups.
You can explicitly drop a restore point using the `DROP` `RESTORE` `POINT`
statement.

FOR PLUGGABLE DATABASE

This clause enables you to create a PDB restore point when you are connected
to the root. For `pdb_name`, specify the name of the PDB.

If you are connected to the PDB for which you want to create the restore
point, then it is not necessary to specify this clause. However, if you
specify this clause, then you must specify the name of the PDB to which you
are connected.

AS OF Clause

Use this clause to create a restore point at a specified datetime or SCN in
the past. If you specify `TIMESTAMP`, then `expr` must be a valid datetime
expression resolving to a time in the past. If you specify SCN, then `expr`
must be a valid SCN in the database in the past. In either case, `expr` must
refer to a datetime or SCN in the current incarnation of the database.

PRESERVE

Specify `PRESERVE` to indicate that the restore point must be explicitly
deleted. Such restore points are useful for preserving a flashback database.

GUARANTEE FLASHBACK DATABASE

A guaranteed restore point enables you to flash the database back
deterministically to the restore point regardless of the
`DB_FLASHBACK_RETENTION_TARGET` initialization parameter setting. The
guaranteed ability to flash back depends on sufficient space being available
in the fast recovery area.

Guaranteed restore points guarantee only that the database will maintain
enough flashback logs to flashback the database to the guaranteed restore
point. It does not guarantee that the database will have enough undo to
flashback any table to the same restore point.

Guaranteed restore points are always preserved. They must be dropped
explicitly by the user using the `DROP` `RESTORE` `POINT` statement. They do
not age out. Guaranteed restore points can use considerable space in the fast
recovery area. Therefore, Oracle recommends that you create guaranteed restore
points only after careful consideration.

Examples

Creating and Using a Restore Point: Example

The following example creates a normal restore point, updates a table, and
then flashes back the altered table to the restore point. The example assumes
the user `hr` has the appropriate system privileges to use each of the
statements.

    
    
    CREATE RESTORE POINT good_data;
    
    SELECT salary FROM employees WHERE employee_id = 108;
    
        SALARY
    ----------
         12000
    
    UPDATE employees SET salary = salary*10
       WHERE employee_id = 108;
    
    SELECT salary FROM employees
       WHERE employee_id = 108;
    
        SALARY
    ----------
        120000
    
    COMMIT;
    
    FLASHBACK TABLE employees TO RESTORE POINT good_data;
    
    SELECT salary FROM employees
       WHERE employee_id = 108;
    
        SALARY
    ----------
         12000


[← Previous](create-property-graph.md)

[Next →](CREATE-ROLE.md)
