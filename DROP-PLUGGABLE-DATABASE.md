[Previous](DROP-PACKAGE.md) [Next](drop-pmem-filestore.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP PLUGGABLE DATABASE

## DROP PLUGGABLE DATABASE

Purpose

Use the `DROP` `PLUGGABLE` `DATABASE` statement to drop a pluggable database
(PDB). The PDB can be a traditional PDB, an application container, an
application seed, or an application PDB.

When you drop a PDB, the control file of the multitenant container database
(CDB) is modified to remove all references to the dropped PDB and its data
files. Archived logs and backups associated with the dropped PDB are not
deleted. You can delete them using Oracle Recovery Manager (RMAN), or you can
retain them in case you subsequently want to perform point-in-time recovery of
the PDB.

Caution:

You cannot roll back a `DROP` `PLUGGABLE` `DATABASE` statement.

Prerequisites

You must be connected to a CDB.

To drop a traditional PDB or an application container, the current container
must be the root, you must be authenticated `AS` `SYSDBA` or `AS` `SYSOPER`,
and the `SYSDBA` or `SYSOPER` privilege must be either granted to you
commonly, or granted to you locally in the root and locally in traditional PDB
or application container you want to drop. The application container must be
empty, that is, it must not contain an application seed or any application
PDBs.

To drop an application seed, the current container must be the root or the
application root, you must be authenticated `AS` `SYSDBA` or `AS` `SYSOPER`,
and the `SYSDBA` or `SYSOPER` privilege must be either granted to you
commonly, or granted to you locally in the root or application root.

To drop an application PDB, the current container must be the root or the
application root, you must be authenticated `AS` `SYSDBA` or `AS` `SYSOPER`,
and the `SYSDBA` or `SYSOPER` privilege must be either granted to you
commonly, or granted to you locally in the root or application root, and
locally in the application PDB you want to drop.

To specify `KEEP` `DATAFILES` (the default), the PDB you want to drop must be
unplugged.

To specify `INCLUDING` `DATAFILES`, the PDB you want to drop must be in
mounted mode or it must be unplugged.

Syntax

drop_pluggable_database::=

![Description of drop_pluggable_database.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_pluggable_database.gif)  
[Description of the illustration
drop_pluggable_database.eps](img_text/drop_pluggable_database.md)

Semantics

pdb_name

Specify the name of the PDB you want to drop. You cannot drop the seed
(`PDB$SEED`). However, you can drop an application seed.

FORCE

Use `FORCE` to drop an orphaned application root container.

`FORCE` requires the following condition: the `APP_ROOT_CLONE` must be closed,
and the `APP_CDB` must be open.

To close the `APP_ROOT_CLONE`, you must set the variable `_ORACLE_SCRIPT"` to
true using `ALTER SESSION`.

Keeping `APP_CDB` open follow the instructions to close the `APP_ROOT_CLONE`:

    
    
    ALTER SESSION SET _ORACLE_SCRIPT"=true ;
    ALTER PLUGGABLE DATABASE APP_ROOT_CLONE CLOSE;
    DROP PLUGGABLE DATABASE APP_ROOT_CLONE FORCE INCLUDING DATAFILES;   

See Also:

[Removing a PDB](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=MULTI-GUID-AE0FC673-3D8C-417E-B671-B2CE465E8DC3)

KEEP DATAFILES

Specify `KEEP` `DATAFILES` to retain the data files associated with the PDB
after the PDB is dropped. The temp file for the PDB is deleted because it is
no longer needed. This is the default.

Keeping data files may be useful in scenarios where a PDB that is unplugged
from one CDB is plugged into another CDB, with both CDBs sharing storage
devices.

INCLUDING DATAFILES

Specify `INCLUDING` `DATAFILES` to delete the data files associated with the
PDB being dropped. The temp file for the PDB is also deleted.

Restriction on Dropping SNAPSHOT COPY PDBs

If a PDB was created with the `SNAPSHOT` `COPY` clause, then you must specify
`INCLUDING` `DATAFILES` when you drop the PDB.

Examples

Dropping a PDB: Example

The following statement drops the PDB `pdb1` and its associated data files:

    
    
    DROP PLUGGABLE DATABASE pdb1
      INCLUDING DATAFILES;


[← Previous](DROP-PACKAGE.md)

[Next →](drop-pmem-filestore.md)
