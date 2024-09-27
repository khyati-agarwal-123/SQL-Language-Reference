[Previous](drop-property-graph.md) [Next](DROP-ROLE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP RESTORE POINT 

## DROP RESTORE POINT

Purpose

Use the `DROP` `RESTORE` `POINT` statement to remove a normal restore point or
a guaranteed restore point from the database.

  * You need not drop normal restore points. The database automatically drops the oldest restore points when necessary, as described in the semantics for [restore_point](CREATE-RESTORE-POINT.md#GUID-AD0FB693-7C28-4908-A870-BA884B320575__BABEBBJC). However, you can drop a normal restore point if you want to reuse the name. 

  * Guaranteed restore points are not dropped automatically. Therefore, if you want to remove a guaranteed restore point from the database, then you must do so explicitly using this statement.

See Also:

[CREATE RESTORE POINT](CREATE-RESTORE-POINT.md#GUID-
AD0FB693-7C28-4908-A870-BA884B320575), [FLASHBACK DATABASE](FLASHBACK-
DATABASE.md#GUID-BE0ACF9A-BC13-4810-B08B-33326440258B), and [FLASHBACK
TABLE](FLASHBACK-TABLE.md#GUID-FA9AF2FD-2DAD-4387-9E62-14AFC26EA85C) for
information on creating and using restore points

Prerequisites

To drop a normal restore point, you must have the `SELECT` `ANY` `DICTIONARY`,
`FLASHBACK` `ANY` `TABLE`, `SYSBACKUP`, or `SYSDG` system privilege.

To drop a guaranteed restore point, you must fulfill one of the following
conditions:

  * You must connect `AS SYSDBA`, or `AS SYSBACKUP`, or `AS SYSDG`. 

  * You must have been granted the `SYSDBA` privilege, and be using a multitenant database. 

  * You must be running as user `SYS`, and be using a a multitenant database. 

You can drop a restore point when connected to a multitenant container
database (CDB) as follows:

  * To drop a normal CDB restore point, the current container must be the root and you must have the `SELECT` `ANY` `DICTIONARY` or `FLASHBACK` `ANY` `TABLE` system privilege, either granted commonly or granted locally in the root, or the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly. 

  * To drop a guaranteed CDB restore point, the current container must be the root and you must have the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege granted commonly. 

  * To drop a normal PDB restore point, the current container must be the root and you must have the `SELECT` `ANY` `DICTIONARY`, `FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly, or the current container must be the PDB in which you want to create the restore point and you must have the `SELECT` `ANY` `DICTIONARY`, `FLASHBACK` `ANY` `TABLE`, `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly or granted locally in that PDB. 

  * To drop a guaranteed PDB restore point, the current container must be the root and you must have the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly, or the current container must be the PDB in which you want to create the restore point and you must have the `SYSDBA`, `SYSBACKUP`, or `SYSDG` system privilege, granted commonly or granted locally in that PDB. 

Syntax

drop_restore_point::=

![Description of drop_restore_point.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_restore_point.gif)  
[Description of the illustration
drop_restore_point.eps](img_text/drop_restore_point.md)

Semantics

restore_point

Specify the name of the restore point you want to drop.

FOR PLUGGABLE DATABASE

This clause enables you to drop a PDB restore point when you are connected to
the root. For `pdb_name`, specify the name of the PDB that contains the
restore point you want to drop.

If you are connected to the PDB from which you want to drop the restore point,
then it is not necessary to specify this clause. However, if you specify this
clause, then you must specify the name of the PDB to which you are connected.

Examples

Dropping a Restore Point: Example

The following example drops the `good_data` restore point, which was created
in "[Creating and Using a Restore Point: Example](CREATE-RESTORE-
POINT.md#GUID-AD0FB693-7C28-4908-A870-BA884B320575__BABCFEEH)":

    
    
    DROP RESTORE POINT good_data;


[← Previous](drop-property-graph.md)

[Next →](DROP-ROLE.md)
