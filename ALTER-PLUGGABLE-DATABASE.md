[Previous](ALTER-PACKAGE.md) [Next](alter-pmem-filestore.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER PLUGGABLE DATABASE

## ALTER PLUGGABLE DATABASE

Purpose

Use the `ALTER` `PLUGGABLE` `DATABASE` statement to modify a pluggable
database (PDB). The PDB can be a traditional PDB, an application container, or
an application PDB.

This statement enables you to perform the following tasks:

  * Unplug a PDB from a multitenant container database (CDB) (using the `pdb_unplug_clause`) 

  * Modify the settings of a PDB (using the `pdb_settings_clauses`) 

  * Bring PDB data files online or take them offline (using the `pdb_datafile_clause`) 

  * Back up and recover a PDB (using the `pdb_recovery_clauses`) 

  * Modify the state of a PDB (using the `pdb_change_state` clause) 

  * Modify the state of multiple PDBs within a CDB (using the `pdb_change_state_from_root` clause) 

  * Perform operations on applications in an application container (using the `application_clauses`) 

  * Create and manage PDB snapshots using the `snapshot_clauses`

Note:

You can perform all `ALTER` `PLUGGABLE` `DATABASE` tasks by connecting to a
PDB and running the corresponding `ALTER` `DATABASE` statement. This
functionality is provided to maintain backward compatibility for applications
that have been migrated to a CDB environment. The exception is modifying PDB
storage limits, for which you must use the `pdb_storage_clause` of `ALTER`
`PLUGGABLE` `DATABASE`.

See Also:

[CREATE PLUGGABLE DATABASE](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC) for information on creating PDBs

Prerequisites

You must be connected to a CDB.

To specify the `pdb_unplug_clause`, the current container must be the root or
the application root, you must be authenticated `AS` `SYSDBA` or `AS`
`SYSOPER`, and the `SYSDBA` or `SYSOPER` privilege must be either granted to
you commonly, or granted to you locally in the root and locally in the PDB you
want to unplug.

To specify the `pdb_settings_clauses`, the current container must be the PDB
whose settings you want to modify and you must have the `ALTER` `DATABASE`
privilege, either granted commonly or granted locally in the PDB. To specify
the `pdb_logging_clauses` or the `RENAME` `GLOBAL_NAME` clause, you must also
have the `RESTRICTED` `SESSION` privilege, either granted commonly or granted
locally in the PDB being renamed, and the PDB must be in `READ` `WRITE`
`RESTRICTED` mode.

To specify the `pdb_datafile_clause`, the current container must be the PDB
whose datafiles you want to bring online or take offline and you must have the
`ALTER` `DATABASE` privilege, either granted commonly or granted locally in
the PDB.

To specify the `pdb_recovery_clauses`, the current container must be the PDB
you want to back up or recover and you must have the `ALTER` `DATABASE`
privilege, either granted commonly or granted locally in the PDB.

To specify the `pdb_change_state` clause, the current container must be the
PDB whose state you want to change and you must be authenticated `AS`
`SYSBACKUP`, `AS` `SYSDBA`, `AS` `SYSDG`, or `AS` `SYSOPER`.

To specify the `pdb_change_state_from_root` clause, the current container must
be the root or the application root, you must be authenticated `AS`
`SYSBACKUP`, `AS` `SYSDBA`, `AS` `SYSDG`, or `AS` `SYSOPER`, and the
`SYSBACKUP`, `SYSDBA`, `SYSDG`, or `SYSOPER` privilege must be either granted
to you commonly, or granted to you locally in the root or application root,
and locally in the PDB(s) whose state(s) you want to change.

To specify the `application_clauses`, the current container must be an
application container, you must be authenticated `AS` `SYSBACKUP` or `AS`
`SYSDBA`, and the `SYSBACKUP` or `SYSDBA` privilege must be either granted to
you commonly, or granted to you locally in the application root and locally in
the application PDB(s) in which you want to perform application operations.

Syntax

alter_pluggable_database::=

![Description of alter_pluggable_database.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_pluggable_database.gif)  
[Description of the illustration
alter_pluggable_database.eps](img_text/alter_pluggable_database.md)

([pdb_unplug_clause::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHGFBEG),
[pdb_settings_clauses::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHCEIGC),
[pdb_datafile_clause::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHHEJFH),
[pdb_recovery_clauses](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHDJFHH),
[pdb_change_state::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHJEAIE),
[pdb_change_state_from_root::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHBBCHH),
[application_clauses::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__APPLICATION_CLAUSES-584C52BC))

database_clause::=

![Description of database_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/database_clause.gif)  
[Description of the illustration
database_clause.eps](img_text/database_clause.md)

pdb_unplug_clause::=

![Description of pdb_unplug_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_unplug_clause.gif)  
[Description of the illustration
pdb_unplug_clause.eps](img_text/pdb_unplug_clause.md)

pdb_unplug_encrypt::=

![Description of pdb_unplug_encrypt.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_unplug_encrypt.gif)  
[Description of the illustration
pdb_unplug_encrypt.eps](img_text/pdb_unplug_encrypt.md)

pdb_settings_clauses::=

![Description of pdb_settings_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_settings_clauses.gif)  
[Description of the illustration
pdb_settings_clauses.eps](img_text/pdb_settings_clauses.md)

([set_time_zone_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208406),
[database_file_clauses::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2082829),
[supplemental_db_logging::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208261),
[pdb_storage_clause::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHJICCH),
[pdb_logging_clauses::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__BGBBECGG),
[pdb_refresh_mode_clause::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__PDB_REFRESH_MODE_CLAUSE-532EAA89))

pdb_storage_clause::=

![Description of pdb_storage_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_storage_clause.gif)  
[Description of the illustration
pdb_storage_clause.eps](img_text/pdb_storage_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

pdb_logging_clauses::=

![Description of pdb_logging_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_logging_clauses.gif)  
[Description of the illustration
pdb_logging_clauses.eps](img_text/pdb_logging_clauses.md)

logging_clause::=

![Description of logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logging_clause.gif)  
[Description of the illustration
logging_clause.eps](img_text/logging_clause.md)

pdb_force_logging_clause::=

![Description of pdb_force_logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_force_logging_clause.gif)  
[Description of the illustration
pdb_force_logging_clause.eps](img_text/pdb_force_logging_clause.md)

pdb_refresh_mode_clause::=

![Description of pdb_refresh_mode_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_refresh_mode_clause.gif)  
[Description of the illustration
pdb_refresh_mode_clause.eps](img_text/pdb_refresh_mode_clause.md)

pdb_refresh_switchover_clause ::=

![Description of pdb_refresh_switchover_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_refresh_switchover_clause.gif)  
[Description of the illustration
pdb_refresh_switchover_clause.eps](img_text/pdb_refresh_switchover_clause.md)

pdb_datafile_clause::=

![Description of pdb_datafile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_datafile_clause.gif)  
[Description of the illustration
pdb_datafile_clause.eps](img_text/pdb_datafile_clause.md)

pdb_recovery_clauses

![Description of pdb_recovery_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_recovery_clauses.gif)  
[Description of the illustration
pdb_recovery_clauses.eps](img_text/pdb_recovery_clauses.md)

pdb_general_recovery::=

![Description of pdb_general_recovery.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_general_recovery.gif)  
[Description of the illustration
pdb_general_recovery.eps](img_text/pdb_general_recovery.md)

pdb_change_state::=

![Description of pdb_change_state.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_change_state.gif)  
[Description of the illustration
pdb_change_state.eps](img_text/pdb_change_state.md)

([pdb_open::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHGJJHH),
[pdb_close::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHEBEAF),
[pdb_save_or_discard_state::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__BGBEFGGC))

pdb_open::=

![Description of pdb_open.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_open.gif)  
[Description of the illustration pdb_open.eps](img_text/pdb_open.md)

instances_clause::=

![Description of instances_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/instances_clause.gif)  
[Description of the illustration
instances_clause.eps](img_text/instances_clause.md)

services_clause::=

  

![Description of services_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/services_clause.gif)  
[Description of the illustration
services_clause.eps](img_text/services_clause.md)

  

pdb_close::=

![Description of pdb_close.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_close.gif)  
[Description of the illustration pdb_close.eps](img_text/pdb_close.md)

relocate_clause::=

![Description of relocate_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/relocate_clause.gif)  
[Description of the illustration
relocate_clause.eps](img_text/relocate_clause.md)

pdb_save_or_discard_state::=

![Description of pdb_save_or_discard_state.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_save_or_discard_state.gif)  
[Description of the illustration
pdb_save_or_discard_state.eps](img_text/pdb_save_or_discard_state.md)

pdb_change_state_from_root::=

![Description of pdb_change_state_from_root.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_change_state_from_root.gif)  
[Description of the illustration
pdb_change_state_from_root.eps](img_text/pdb_change_state_from_root.md)

([pdb_open::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHGJJHH),
[pdb_close::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHEBEAF),
[pdb_save_or_discard_state::=](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__BGBEFGGC))

application_clauses::=

![Description of application_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/application_clauses.gif)  
[Description of the illustration
application_clauses.eps](img_text/application_clauses.md)

snapshot_clauses ::=

![Description of snapshot_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/snapshot_clauses.gif)  
[Description of the illustration
snapshot_clauses.eps](img_text/snapshot_clauses.md)

pdb_snapshot_clause ::=

![Description of pdb_snapshot_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_snapshot_clause.gif)  
[Description of the illustration
pdb_snapshot_clause.eps](img_text/pdb_snapshot_clause.md)

materialize_clause::=

![Description of materialize_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/materialize_clause.gif)  
[Description of the illustration
materialize_clause.eps](img_text/materialize_clause.md)

create_snapshot_clause::=

![Description of create_snapshot_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_snapshot_clause.gif)  
[Description of the illustration
create_snapshot_clause.eps](img_text/create_snapshot_clause.md)

drop_snapshot_clause::=

![Description of drop_snapshot_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_snapshot_clause.gif)  
[Description of the illustration
drop_snapshot_clause.eps](img_text/drop_snapshot_clause.md)

set_max_pdb_snapshots::=

![Description of set_max_pdb_snapshots_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/set_max_pdb_snapshots_clause.gif)  
[Description of the illustration
set_max_pdb_snapshots_clause.eps](img_text/set_max_pdb_snapshots_clause.md)

prepare_clause::=

![Description of prepare_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/prepare_clause.gif)  
[Description of the illustration
prepare_clause.eps](img_text/prepare_clause.md)

drop_mirror_copy::=

![Description of drop_mirror_copy.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_mirror_copy.gif)  
[Description of the illustration
drop_mirror_copy.eps](img_text/drop_mirror_copy.md)

lost_write_protection ::=

The usage for the `lost_write_protection` clause with the `ALTER PLUGGABLE
DATABASE` statement is identical to the `ALTER DATABASE` statement. Look here
[ALTER DATABASE](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986) for syntax details.

pdb_managed_recovery ::=

  

![Description of pdb_managed_recovery.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_managed_recovery.gif)  
[Description of the illustration
pdb_managed_recovery.eps](img_text/pdb_managed_recovery.md)

  

Semantics

database_clause

Specify the `PLUGGABLE DATABASE` option for a container database.

pdb_name

Specify the name of the database to be altered. If you omit `db_name`, then
Oracle Database alters the database identified by the value of the
initialization parameter `DB_NAME`. You can alter only the database whose
control files are specified by the initialization parameter `CONTROL_FILES`.
The database identifier is not related to the Oracle Net database
specification.

pdb_unplug_clause

This clause lets you unplug a PDB from a CDB. When you unplug a PDB, Oracle
stores information about the PDB in a file on your operating system. You can
subsequently use this file to plug the PDB into a CDB.

For `pdb_name`, specify the name of the PDB you want to unplug. The PDB must
be closedâthat is, the open mode must be `MOUNTED`. In an Oracle Real
Application Clusters (Oracle RAC) environment, the PDB must be closed in all
Oracle RAC instances

For `filename`, specify the full path name of the operating system file in
which to store information about the PDB. The file name that you specify
determines the type of information stored and how it is stored.

  * If you specify a file name that ends with the extension .xml, then Oracle creates an XML file containing metadata about the PDB. You can then copy the XML file and the PDB's data files to a new location and specify the XML file name when plugging the PDB into a CDB. In this case, you must copy the PDB's data files separately.

  * If you specify a file name that ends with the extension .pdb, then Oracle creates a .pdb archive file. This is a compressed file that includes an XML file containing metadata about the PDB, as well as the PDB's data files. You can then copy this single archive file to a new location and specify the archive file name when plugging the PDB into a CDB. This eliminates having to copy the PDB's data files separately. When you use a .pdb archive file when plugging in a PDB, this file is extracted when you plug in the PDB, and the PDBâs files are placed in the same directory as the .pdb archive file.

After a PDB is unplugged, it remains in the CDB with an open mode of `MOUNTED`
and a status of `UNPLUGGED`. The only operation you can perform on an
unplugged PDB is `DROP` `PLUGGABLE` `DATABASE`, which will remove it from the
CDB. You must drop the PDB before you can plug it into the same CDB or another
CDB.

See Also:

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN13623) for more information on unplugging a PDB 

  * The [create_pdb_from_xml](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACJHJFE) clause of `CREATE` `PLUGGABLE` `DATABASE` for information on plugging a PDB into a CDB 

pdb_unplug_encrypt

You must have the `SYSKM` privilege to execute this command.

United PDBs

  * `ENCRYPT USING transport_secret` is optional. 

  * If TDE is in use, you must specify this clause. If TDE is not in use, the statement throws the following error `ORA-46680:master keys of the container database must be exported.`

  * The wallet must be open in `ROOT` if TDE is in use. 

  * Keys are encrypted using the provided `transport secret` and exported into the `.XML` or archive file 

Unplugging a PDB Into an XML Metadata File: Example

    
    
    ALTER PLUGGABLE DATABASE CDB1_PDB2 UNPLUG INTO '/tmp/cdb1_pdb2.xml' ENCRYPT USING transport_secret

Unplugging a PDB Into an Archive File: Example

    
    
    ALTER PLUGGABLE DATABASE CDB1_PDB1_1 UNPLUG INTO '/tmp/CDB1_PDB1_1.pdb' ENCRYPT USING transport_secret

For PDBs in isolated mode, you need not specify `ENCRYPT USING
transport_secret`. This is not required because the wallet file of the PDB is
copied during the creation of the pluggable database from an XML file. If you
are unplugging a PDB as an archive file, the wallet file of the PDB is added
to the zipped archive with the `.pdb` extension.

If the `ewallet.p12` file already exists at the destination, a backup is
automatically initiated. The backup file has the following format:
`ewallet_PLGDB_2017090517455564.p12`.

pdb_settings_clauses

These clauses lets you modify various settings for a PDB.

pdb_name

You can optionally use `pdb_name` to specify the name of the PDB whose
settings you want to modify.

DEFAULT EDITION Clause

Use this clause to designate the specified edition as the default edition for
the PDB. For the full semantics of this clause, refer to "[DEFAULT EDITION
Clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BABEADGC)" in the
`ALTER` `DATABASE` documentation.

SET DEFAULT TABLESPACE Clause

Use this clause to specify or change the default type of tablespaces
subsequently created in the PDB. For the full semantics of this clause, refer
to "[SET DEFAULT TABLESPACE Clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGBDJGGH)" in the
`ALTER` `DATABASE` documentation.

DEFAULT TABLESPACE Clause

Use this clause to establish or change the default permanent tablespace of the
PDB. For the full semantics of this clause, refer to "[DEFAULT TABLESPACE
Clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGBIJBIC)" in the
`ALTER` `DATABASE` documentation.

DEFAULT TEMPORARY TABLESPACE Clause

Use this clause to change the default temporary tablespace of the PDB to a new
tablespace or tablespace group. For the full semantics of this clause, refer
to "[DEFAULT [LOCAL] TEMPORARY TABLESPACE Clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGBEIJJD)" in the
`ALTER` `DATABASE` documentation.

RENAME GLOBAL_NAME TO Clause

Use this clause to change the global name of the PDB. The new global name must
be unique within the CDB. For an Oracle Real Application Clusters (Oracle RAC)
database, the PDB must be open in `READ` `WRITE` `RESTRICTED` mode on the
current instance only. The PDB must be closed on all other instances. For the
full semantics of this clause, refer to "[RENAME GLOBAL_NAME Clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2141769)" in the
`ALTER` `DATABASE` documentation.

Note:

When you change the global name of a PDB, be sure to change the `PLUGGABLE`
`DATABASE` property for database services that are used to connect to the PDB.

set_time_zone_clause

Use this clause to modify the time zone setting for the PDB. For the full
semantics of this clause, refer to [set_time_zone_clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2197908) in the
`ALTER` `DATABASE` documentation.

database_file_clauses

Use this clause to modify data files and temp files for the PDB. For the full
semantics of this clause, refer to [database_file_clauses](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2078824) in the
`ALTER` `DATABASE` documentation.

supplemental_db_logging

Use these clauses to instruct Oracle Database to add or stop adding
supplemental data into the log stream for the PDB.

  * Specify the `ADD` `SUPPLEMENTAL` `LOG` clause to add supplemental data into the log stream for the PDB. In order to issue this clause, supplemental logging must have been enabled for the CDB root with the `ALTER` `DATABASE` ... `ADD` `SUPPLEMENTAL` `LOG` ... statement. The level of supplemental logging that you specify for the PDB does not need to match that of the CDB root. That is, you can specify any of the clauses `DATA`, `supplemental_id_key_clause`, or `supplemental_plsql_clause` for the PDB, regardless of which clause was specified when enabling supplemental logging for the CDB root. 

  * Specify the `DROP` `SUPPLEMENTAL` `LOG` clause to stop adding supplemental data into the log stream for the PDB. 

ADD SUPPLEMENTAL LOG DATA SUBSET DATABASE REPLICATION, of `ALTER PLUGGABLE
DATABASE` enables low impact minimal supplemental logging on the PDB.

  * You can only execute this DDL on a pluggable database.

  * You can execute this DDL only when the `enable_goldengate_replication` parameter is TRUE, and database compatible is 19.0 or higher. 

  * You must enable minimal supplemental logging in `CDB$ROOT` to run this command. 

  * After you execute this DDL, minimal supplemental logging will become low impact for the pluggable database. `SYS.PROP$` will be updated to indicate that low impact minimal supplemental logging is enabled at the PDB level for this pluggable database. 

DROP SUPPLEMENTAL LOG DATA SUBSET DATABASE REPLICATION, of `ALTER PLUGGABLE
DATABASE` disables low impact minimal supplemental logging on the PDB.

  * You can only execute this DDL on a pluggable database.

  * You can execute this DDL only when the `enable_goldengate_replication` parameter is TRUE, and database compatible is 19.0 or higher. 

  * You must enable minimal supplemental logging in `CDB$ROOT` to run this command. 

  * `SYS.PROP$` will be updated to indicate that supplemental logging for subset database replication is disabled at the PDB level for this pluggable database. If supplemental logging for subset database replication is also disabled at `CDB$ROOT` (CDB level), then low impact minimal supplemental logging will be disabled for this pluggable database. 

For the full semantics of this clause, refer to
[supplemental_db_logging](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2153841) in the
`ALTER` `DATABASE` documentation.

pdb_storage_clause

Use this clause to modify the storage limits for a PDB.

This clause has the same semantics as the [pdb_storage_clause](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACJAAGI)
in the `CREATE` `PLUGGABLE` `DATABASE` documentation, with the following
additions:

  * If you specify `MAXSIZE` `size_clause`, then the value you specify for `size_clause` must be greater than or equal to the combined size of the existing tablespaces belonging to the PDB. Otherwise, an error occurs. 

  * If you specify `MAX_AUDIT_SIZE` `size_clause`, then the value you specify for `size_clause` must be greater than or equal to the amount of storage used by the existing unified audit OS spillover (`.bin` format) files in the PDB. Otherwise, an error occurs. 

  * If you specify `MAX_DIAG_SIZE` `size_clause`, then the value you specify for `size_clause` must be greater than or equal to the amount of storage for diagnostics in the Automatic Diagnostic Repository (ADR) that is currently used by the PDB. Otherwise an error occurs. 

pdb_logging_clauses

Use these clauses to set or change the logging characteristics of the PDB.

logging_clause

Use this clause to change the default logging attribute for tablespaces
subsequently created within the PDB. This clause has the same semantics as the
[logging_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACJIEBE) in the `CREATE` `PLUGGABLE` `DATABASE`
documentation.

pdb_force_logging_clause

Use this clause to place a PDB into, or take it out of, one of four logging
modes.

Force logging mode instructs the database to log all changes in the PDB,
except changes in temporary tablespaces and temporary segments. Force
nologging mode instructs the database to not log any changes in the PDB.

Standby nologging instructs the database to not log operations that qualify to
be done without logging. The database sends the data blocks that were created
by the operation to each qualifying standby database in the Data Guard
configuration, typically resulting in those standbys not having invalid
blocks.

CDB-wide force logging mode takes precedence over any other setting. PDB-level
force logging mode and force nologging mode take precedence over and are
independent of any `LOGGING`, `NOLOGGING`, or `FORCE` `LOGGING` settings you
specify for individual tablespaces in the PDB and any `LOGGING` or `NOLOGGING`
settings you specify for individual database objects in the PDB.

  * Specify `ENABLE` `FORCE` `LOGGING` to place the PDB in force logging mode. If the PDB is currently in force nologging mode, then specifying this clause results in an error. You must first specify `DISABLE` `FORCE` `NOLOGGING`. 

  * Specify `DISABLE` `FORCE` `LOGGING` to take the PDB out of force logging mode. If the PDB is not currently in force logging mode, then specifying this clause results in an error. 

  * Specify `ENABLE` `FORCE` `NOLOGGING` to place the PDB in force nologging mode. If the PDB is currently in force logging mode, then specifying this clause results in an error. You must first specify `DISABLE` `FORCE` `LOGGING`. The nonlogged operations will use classic invalidation redo, even if the CDB has a standby nologging mode set. 

  * Specify `DISABLE` `FORCE` `NOLOGGING` to take the PDB out of force nologging mode. If the PDB is not currently in force nologging mode, then specifying this clause results in an error. 

  * Specify `SET STANDBY NOLOGGING FOR LOAD PERFORMANCE` to put the PDB into standby nologging for load performance mode. In this mode the data loaded as part of the nonlogged task is sent to the qualifying standbys via a private network connection, provided that doing so will not slow down the load process. If a slow down occurs, then the data is not sent but fetched automatically from the primary as each standby encounters the invalidation redo and will be retried until the data blocks are eventually received. 

  * Specify `SET STANDBY NOLOGGING FOR DATA AVAILABILITY` to put the PDB into standby nologging for data availability mode. In this mode the data loaded as part of the nonlogged task is sent to the qualifying standbys either via a network connection to them, or if that fails, via block images in the redo. That is to say, in this mode the load will switch to be done in a logged fashion if the network connection or related processes prevent the sending of the data over the private network connection. 

For the standby nologging modes a qualifying standby is one that is open for
read, running managed recovery, and receiving redo into standby redo logs.

This clause does not change the default `LOGGING` or `NOLOGGING` mode of the
PDB specified by the [logging_clause](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__BGBDDAGI).

pdb_refresh_mode_clause

Use this clause to change the refresh mode of a PDB. You can specify this
clause only for a refreshable PDB, that is, a PDB whose current refresh mode
is `MANUAL` or `EVERY` `refresh_interval` `MINUTES` or `HOURS`. You can switch
a PDB from manual refresh to automatic refresh, or from automatic refresh to
manual refresh. You can also use this clause to change the number of minutes
between automatic refreshes. You can switch a PDB from manual or automatic
refresh to no refresh, but you cannot enable manual or automatic refresh for a
PDB that is not refreshable. For the complete semantics of this clause, refer
to the [pdb_refresh_mode_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__PDB_REFRESH_MODE_CLAUSE-2C9E58C3) in the
documentation on `CREATE` `PLUGGABLE` `DATABASE`.

REFRESH

Specify this clause to perform a manual refresh of a refreshable PDB, that is,
a PDB whose current refresh mode is `MANUAL` or `EVERY` `number` `MINUTES`.
The PDB must be closed. For more information on refreshable PDBs, refer to the
[pdb_refresh_mode_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__PDB_REFRESH_MODE_CLAUSE-2C9E58C3) in the
documentation on `CREATE` `PLUGGABLE` `DATABASE`.

pdb_refresh_switchover_clause

Use this clause to reverse roles between a refreshable clone PDB and a primary
PDB. This clause makes the refreshable clone PDB into a primary PDB, which can
be opened in read write mode. The former primary PDB becomes the refreshable
clone..

  * This command must be executed from the primary PDB .

  * `REFRESH MODE NONE` may not be specified when issuing this statement. 

  * The `dblink` should point to the Root of the CDB where the refreshable clone PDB currently resides. 

  * After this operation, the current PDB will become the refreshable clone and can only be opened in READ ONLY mode.

  * The database link user must exist in the primary PDB, if the refreshable clone exists in a different CDB.

PRIORITY

You can control the order of operations on PDBs by assigning a `PRIORITY` to
the PDB. The priority`value` should be a whole number greater than 0 and less
than 4099. A value outside this range throws an error.

The following ordering rules apply to manage different kinds of PDBs:

  * PDBs are processed in an ascending order of priority. A PDB with a lower priority value will be processed before a PDB with a higher priority value.

  * PDBs with the same priority may be processed in any order. However, if App PDBs and the App Root have the same priority or have no priority, App PDBs will still be opened after the App Root.

  * PDBs have no priority are considered to be the lowest priority.

  * PDB priority for a given PDB is applicable to all RAC instances, i.e priority is NOT specific to a given RAC instance.

  * Priority will not be copied from source PDB to target PDB by plug, unplug or refreshable clone.

  * App PDBs cannot have a higher priority than App Root.

  * App Root clones have the same priority as App Roots, and cannot be explicitly given a PDB priority.

  * The priority of `CDB$ROOT` and `PDB$SEED` is determined internally by Oracle RDBMS and is not subject to PDB priority . 

SET CONTAINER_MAP

Use this clause to specify the `CONTAINER_MAP` database property for an
application container. The current container must be the application root. The
`map_object` is of the form `[``schema``.]``table`. For `schema`, specify the
schema containing `table`. If you omit `schema`, then the database assumed
that the table is in your own schema. For `table`, specify a range-, list-, or
hash-partitioned table.

CONTAINERS DEFAULT TARGET

Use this clause to specify the default container for DML statements in an
application container. You must be connect to the application root.

  * For `container_name`, specify the name of the default container. The default container can be any container in the application container, including the application root or an application PDB. You can specify only one default container. 

  * If you specify `NONE`, then the default container is the CDB root. This is the default. 

When a DML statement is issued in the application root without specifying
containers in the `WHERE` clause, the DML statement affects the default
container for the application container.

CONTAINERS HOST and PORT

Use the `HOST` and `PORT` clauses if you want to create a PDB that you plan to
reference from a proxy PDB. This type of PDB is called a referenced PDB.

The following statements can be executed within a PDB:

    
    
    ALTER PLUGGABLE DATABASE CONTAINERS HOST='myhost.example.com';
    
    
    ALTER PLUGGABLE DATABASE CONTAINERS PORT=1599;

The following statements can be executed within CDB Root, Application Root, or
within a PDB :

    
    
    ALTER PLUGGABLE DATABASE <pdbname> CONTAINERS HOST='myhost.example.com';
    
    
    ALTER PLUGGABLE DATABASE <pdbname> CONTAINERS PORT=1599;

`pdbname` must meet the following criteria:

  * If the statement is executed in Application Root, then `pdbname` has to match the name of Application Root or the name of one of its Application PDBs. 
  * If the statement is executed in CDB Root, then `pdbname` has to match the name of one of the PDBs in the CDB. 
  * If the statement is executed in a PDB, then `pdbname` has to match the name of the current PDB. 

See Also:

[HOST and PORT ](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__GUID-C1576338-D9C3-4446-BC4A-B92DB920CBC0) of
`CREATE PLUGGABLE DATABASE` for the full semantics of `HOST` and `PORT`

pdb_datafile_clause

This clause lets you bring data files associated with a PDB online or take
them offline. The PDB must be closed when you issue this clause.

  * For `pdb_name`, specify the name of the PDB. If the current container is the PDB, then you can omit `pdb_name`. 

  * The `DATAFILE` clauses let you specify the data files you want to bring online or take offline. Use `filename` or `filenumber` to identify specific data files by name or by number. You can view data file names and numbers by querying the `NAME` and `FILE#` columns of the `V$DATAFILE` dynamic performance view. Use `ALL` to specify all datafiles associated with the PDB. 

  * Specify `ONLINE` to bring the data files online or `OFFLINE` to take the data files offline. 

pdb_recovery_clauses

Use the `pdb_recovery_clauses` to back up and recover a PDB.

pdb_name

You can optionally use `pdb_name` to specify the name of the PDB you want to
back up or recover.

pdb_general_recovery

This clause lets you control media recovery for the PDB or standby database or
for specified tablespaces or files. The `pdb_general_recovery` clause has the
same semantics as the `general_recovery` clause of `ALTER` `DATABASE`. Refer
to the [general_recovery](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208874) clause of
`ALTER` `DATABASE` for more information.

BACKUP Clauses

Use these clauses to move all of the data files in the PDB into or out of
online backup mode (also called hot backup mode). These clauses have the same
semantics in `ALTER` `PLUGGABLE` `DATABASE` and `ALTER` `DATABASE`. Refer to
the "[BACKUP Clauses](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2150230)" of `ALTER`
`DATABASE` for more information.

RECOVERY Clauses

Use these clauses to enable or disable a PDB for recovery. The PDB must be
closedâthat is, the open mode must be `MOUNTED`.

  * Specify `ENABLE` `RECOVERY` to bring all data files that belong to a PDB online and enable the PDB for recovery. 

  * Specify `DISABLE` `RECOVERY` to take all data files that belong to a PDB offline and disable the PDB for recovery. 

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB5261) for more information on the `RECOVERY` clauses

pdb_change_state

This clause enables you to change the state, or open mode, of a PDB. [Table
11-2](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHJEFGC "This first
column lists the PDB open modes and the second column lists their
descriptions.") lists the open modes of a PDB.

  * Specify the `pdb_open` clause to change the open mode to `READ` `WRITE`, `READ` `ONLY`, or `MIGRATE`. 

  * Specify the `pdb_close` clause to change the open mode to `MOUNTED`. 

Table 11-2 PDB Open Modes

Open Mode | Description  
---|---  
`READ` `WRITE` |  A PDB in open read/write mode allows queries and user transactions to proceed and allows users to generate redo logs.  
`READ` `ONLY` |  A PDB in open read-only mode allows queries but does not allow user changes.  
`MIGRATE` |  When a PDB is in open migrate mode, you can run database upgrade scripts on the PDB.  
`MOUNTED` |  When a PDB is in mounted mode, it behaves like a non-CDB in mounted mode. It does not allow changes to any objects, and it is accessible only to database administrators. It cannot read from or write to data files. Information about the PDB is removed from memory caches. Cold backups of the PDB are possible.  
  
You can view the open mode of a PDB by querying the `OPEN_MODE` column of the
`V$PDBS` view.

See Also:

[Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN14090) for a complete description of PDB open modes

pdb_name

You can optionally use `pdb_name` to specify the name of the PDB whose open
mode you want to change.

pdb_open

This clause lets you change the open mode of a PDB to `READ` `WRITE`, `READ`
`ONLY`, or `MIGRATE`. When you specify this clause, the PDB must be in
`MOUNTED` mode unless you specify the `FORCE` keyword.

If you do not specify `READ` `WRITE` or `READ` `ONLY`, then the default is
`READ` `WRITE`. The exception is when the PDB belongs to a CDB that is used as
a physical standby database, in which case the default is `READ` `ONLY`.

READ WRITE

Specify this clause to change the open mode to `READ` `WRITE`.

READ ONLY

Specify this clause to change the open mode to `READ` `ONLY`.

HYBRID READ ONLY

Specify this clause to open a PDB in `READ ONLY` and `READ WRITE` mode
depending on the type of user that connects to it. When a local user connects
to the PDB, the PDB operates in `READ ONLY` mode. The PDB operates in `READ
WRITE` mode for common users.

[READ WRITE] UPGRADE

Specify this clause to change the open mode to `MIGRATE`. The `READ` `WRITE`
keywords are optional and are provided for semantic clarity.

RESTRICTED

If you specify the optional `RESTRICTED` keyword, then the PDB is accessible
only to users with the `RESTRICTED` `SESSION` privilege in the PDB.

If the PDB is in `READ` `WRITE` or `READ` `ONLY` mode, and you specify the
`RESTRICTED` and `FORCE` keywords while changing the open mode, then all
sessions connected to the PDB that do not have the `RESTRICTED` `SESSION`
privilege in the PDB are terminated, and their transactions are rolled back.

FORCE

Specify this keyword to change the open mode of a PDB from `READ` `WRITE` to
`READ` `ONLY`, or from `READ` `ONLY` to `READ` `WRITE`. The `FORCE` keyword
allows users to remain connected to the PDB while the open mode is changed.

When you specify `FORCE` to change the open mode of a PDB from `READ` `WRITE`
to `READ` `ONLY`, any `READ` `WRITE` transaction that is open when you change
the open mode will not be allowed to perform any more DML operations or to
`COMMIT`.

Restriction on FORCE

You cannot specify the `FORCE` keyword if the PDB is currently in `MIGRATE`
mode, and you cannot specify the `FORCE` keyword to change a currently open
PDB to `MIGRATE` mode.

RESETLOGS

Specify this clause to create a new PDB incarnation and open the PDB in `READ`
`WRITE` mode after point-in-time recovery of the PDB.

See Also:

[Oracle Database Backup and Recovery User's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV640) for more information on performing point-in-
time recovery of CDBs and PDBs

instances_clause

In an Oracle Real Application Clusters environment, use this clause to modify
the state of the PDB in the specified Oracle RAC instances. If you omit this
clause, then the state of the PDB is modified only in the current instance.

  * Use `instance_name` to specify one or more instance names, in a comma-separated list enclosed in parenthesis. This modifies the state of the PDB only in those instances. 

  * Specify `ALL` to modify the state of the PDB in all instances. 

  * Specify `ALL` `EXCEPT` to modify the state of the PDB in all instances except the specified instances. 

If the PDB is already open in one or more instances, then you can open it in
additional instances, but it must be opened in the same mode as in the
instances in which it is already open.

services_clause

  * Use `service_name` to specify one or more services, in a comma-separated list enclosed in parenthesis. 

  * Specify `ALL` to specify all services on the PDB. 

  * Specify `ALL` `EXCEPT` to specify all services except the services specifed. 

pdb_close

This clause lets you change the open mode of a PDB to `MOUNTED`. When you
specify this clause, the PDB must be in `READ` `WRITE`, `READ` `ONLY`, or
`MIGRATE` mode. This clause is the PDB equivalent of the SQL*Plus `SHUTDOWN`
command.

IMMEDIATE

If you specify the optional `IMMEDIATE` keyword, then this clause is the PDB
equivalent of the SQL*Plus `SHUTDOWN` command with the immediate mode.
Otherwise, the PDB is shut down with the normal mode.

See Also:

[SQL*Plus User's Guide and
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SQPUG125) for more information on the SQL*Plus `SHUTDOWN`
command

ABORT

Specify `ABORT` to forcibly shut down the PDB.

instances_clause

In an Oracle Real Application Clusters environment, use this clause to modify
the state of the PDB in the specified Oracle RAC instances. You can close a
PDB in some instances and leave it open in others. Refer to the
[instances_clause](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHDCJCE) for the
full semantics of this clause.

relocate_clause

In an Oracle Real Application Clusters environment, use this clause to
instruct the database to reopen the PDB on a different Oracle RAC instance.

  * Specify `RELOCATE` to reopen the PDB on a different instance that is selected by Oracle Database. 

  * Specify `RELOCATE` `TO` `'``instance_name``'` to reopen the PDB in the specified instance. 

  * Specify `NORELOCATE` to close the PDB in the current instance. This is the default. 

pdb_save_or_discard_state

Use this clause to instruct the database to save or discard the open mode of
the PDB when the CDB restarts.

  * If you specify `SAVE`, then the PDB's open mode after the CDB restarts will be identical to its open mode just before the CDB restarted. 

  * If you specify `DISCARD`, then the PDB's open mode after the CDB restarts will be `MOUNTED`. This is the default. 

instances_clause

In an Oracle Real Application Clusters environment, use this clause to
instruct the database to save or discard the open mode of the PDB in the
specified Oracle RAC instances. If you omit this clause, then the database
applies the `SAVE` or `DISCARD` setting only to the PDB in the current
instance.

  * Use `instance_name` to specify one or more instance names, in a comma-separated list enclosed in parenthesis. This applies the `SAVE` or `DISCARD` setting to the PDB only in those instances. 

  * Specify `ALL` to apply the `SAVE` or `DISCARD` setting to the PDB in all instances. 

  * Specify `ALL` `EXCEPT` to apply the `SAVE` or `DISCARD` setting to the PDB in all instances except the specified instances. 

pdb_change_state_from_root

This clause enables you to modify the state of one or more PDBs.

  * Specify the `pdb_name` for one or more PDBs whose state you want to modify. 

  * Specify `ALL` to modify the state of all PDBs in the CDB. 

  * Specify `ALL` `EXCEPT` to modify the state of all PDBs in the CDB except those specified by using `pdb_name`. 

If a PDB is already in the specified state, then the PDB's state is unchanged
and no error is returned. If the state of a PDB cannot be changed, then an
error occurs only for that PDB.

application_clauses

Use the `APPLICATION` clauses to:

  * Install, patch, upgrade, and uninstall applications

  * Register application versions and patch numbers

  * Sync operations on applications

See Also:

[Oracle Database Administratorâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-1AFD0268-6A2B-4F84-BB4D-4D36976DE53B) for more
information on administering application containers

Specifying Application Names

Most of the `application_clauses` require you to specify an application name.
The maximum length of an application name is 30 bytes. The name must satisfy
the requirements listed in "[Database Object Naming Rules](Database-Object-
Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)". The
application name must be unique within an application container.

Specifying Application Versions

Several of the `application_clauses` require you to specify an application
version. The application version can be up to 30 bytes in length and can
contain alphanumeric characters, punctuations marks, and spaces. The
application version is case-sensitive and must be enclosed in single quotation
marks.

Specifying Comments

Several of the `application_clauses` allow you to specify a comment to
associate with an application install, patch, or upgrade operation. For
`comment`, enter a character string enclosed in single quotation marks.

INSTALL Clauses

Use the `INSTALL` clauses when installing an application in an application
container. The current container must be the application root, not an
application PDB.

  * Specify the `BEGIN` `INSTALL` clause before you start installing the application. 

    * Use `app_name` to assign a name to the application. 

    * Use `app_version` to assign a version to the application. 

    * The optional `COMMENT` clause allows you to enter a comment to be associated with the application version created by this installation. 

  * Specify the `END` `INSTALL` clause after you have finished installing the application. 

    * You must specify the same `app_name` that you specified for the corresponding `BEGIN` `INSTALL` clause. 

    * You need not specify `app_version`, but if you do, then you must specify the same version that you specified for the corresponding `BEGIN` `INSTALL` clause. 

PATCH Clauses

Use the `PATCH` clauses when patching an application in an application
container. The current container must be the application root, not an
application PDB.

  * Specify the `BEGIN` `PATCH` clause before you start patching the application. 

    * For `app_name`, specify the name of the application you want to patch. 

    * For `number`, specify the patch number. 

    * The optional `MINIMUM` `VERSION` clause allows you to specify the minimum version at which the application must be before the patch can be applied. For `app_version`, specify the minimum application version. If the current application version is lower than the minimum application version, then an error occurs. If you omit this clause, then the minimum version is the current application version. 

    * The optional `COMMENT` clause allows you to enter a comment to be associated with the patch. 

  * Specify the `END` `PATCH` clause after you finish patching the application. 

    * You must specify the same `app_name` that you specified for the corresponding `BEGIN` `PATCH` clause. 

    * You need not specify `number`, but if you do, then you must specify the same value that you specified for the corresponding `BEGIN` `PATCH` clause. 

UPGRADE Clauses

Use the `UPGRADE` clauses when upgrading an application in an application
container. The current container must be the application root, not an
application PDB.

If the application root is using TDE, then you must configure an external
store before upgrading the application.

  * Specify the `BEGIN` `UPGRADE` clause before you start upgrading the application. 

    * For `app_name`, specify the name of the application you want to upgrade. 

    * For `start_app_version`, specify the version from which you are upgrading the application. If this version does not match the current application version, then an error occurs. 

    * For `end_app_version`, specify the version to which you are upgrading the application. 

    * The optional `COMMENT` clause allows you to enter a comment to be associated with the upgrade. 

  * Specify the `END` `UPGRADE` clause after you finish upgrading the application. 

    * You must specify the same `app_name` that you specified for the corresponding `BEGIN` `UPGRADE` clause. 

    * You need not specify `TO` `end_app_version`, but if you do, then you must specify the same version that you specified for the corresponding `BEGIN` `UPGRADE` clause. 

UNINSTALL Clauses

Use the `UNINSTALL` clauses when uninstalling an application from an
application container. The current container must be the application root, not
an application PDB.

  * Specify the `BEGIN` `UNINSTALL` clause before you start uninstalling the application. 

    * For `app_name`, specify the name of the application you want to uninstall. 

  * Specify the `END` `UNINSTALL` clause after you have finished uninstalling the application. 

    * You must specify the same `app_name` that you specified for the corresponding `BEGIN` `UNINSTALL` clause. 

SET PATCH

Use the `SET` `PATCH` clause to register the patch number of an application
that is already installed in an application container. This clause allows you
to assign a patch number to an application that was not patched using the
`PATCH` clauses. This is useful if the application was migrated from a PDB in
an earlier Oracle Database release, when the `PATCH` clauses were not
available. The current container can be the application root or an application
PDB.

  * For `app_name`, specify the name of an existing application. 

  * Use `number` to assign a patch number to the existing application. 

SET VERSION

Use the `SET` `VERSION` clause to register the version of an application that
is already installed in an application container. This clause allows you to
assign a name and a version to an application that was not installed using the
`INSTALL` clauses. This is useful if the application was migrated from a PDB
in an earlier Oracle Database release, when the `INSTALL` clauses were not
available. The current container can be the application root or an application
PDB.

  * Use `app_name` to assign a name to the existing application. 

  * Use `app_version` to assign a version to the existing application. 

SET COMPATIBILITY VERSION

Use the `SET` `COMPATIBILITY` `VERSION` clause to set the compatibility
version for an application.

The compatibility version of an application is the earliest version of the
application possible for the application PDBs that belong to the application
container. The current container must be the application root, not an
application PDB.

Note:

You cannot plug in an application PDB that uses an application version earlier
than the compatibility setting of the application container.

  * Use `app_name` to specify the name of the application. 

  * Use `app_version` to specify the compatibility version for the application. 

  * If you specify `CURRENT`, then the compatibility version is set to the version of the application in the application root. 

The compatibility version is enforced when the compatibility version is set
and when an application PDB is created. If there are application root clones
that resulted from application upgrades, then all application root clones that
correspond to versions earlier than the compatibility version are implicitly
dropped.

SYNC TO

You can synchronize an application to a particular version or a patch number.
There are two variations:

  1. `SYNC TO` `version_string`

  2. `SYNC TO` `PATCH` `patch_number`

Example

Assume that you perform the following operations on application `salesapp` :

  1. Install version 1.0

  2. Patch 101

  3. Upgrade to version 2.0

  4. Patch 102

  5. Upgrade to 3.0

`ALTER PLUGGABLE DATABASE APPLICATION salesapp SYNC TO 2.0` replays all
statements up to and including ' Upgrade to version 2.0'.

`ALTER PLUGGABLE DATABASE APPLICATION salesapp SYNC TO PATCH 102` replays all
statements up to and including ' Patch 102'.

Restrictions on SYNC TO

You can use `SYNC TO` only with an individual application.

You cannot use `SYNC TO` with the `ALL SYNC` clause.

You cannot use `SYNC TO` with the `SYNC` clause, in the case when you are
synchronizing multiple applications in a single statement.

SYNC

Use the `SYNC` clause to synchronize an application in an application PDB to
the version and patch level of the same application in the application root.
The current container must be an application PDB.

`app_name` specifies the name of an application that exists in the application
root. The application may or may not exist in the application PDB.

Starting with Oracle Database Release 21c you can synchronize mutiple
applications in one statement with `SYNC` . This is necessary to preserve
functional correctness for applications that depend on one another.

Example

    
    
    ALTER PLUGGABLE DATABASE APPLICATION hrapp payrollapp employeesapp SYNC

Restrictions on Synchronizing Multiple Applications Using SYNC

  * You cannot use the `SYNC TO` `version_string` clause while synchronizing multiple applications with `SYNC`. 

  * You cannot use the `SYNC TO` `PATCH` `patch_number` clause while synchronizing multiple applications with `SYNC`. 

ALL SYNC

Use the `ALL` `SYNC` clause to sync all applications in an application PDB
with all applications in the application root. This clause is useful, if you
have recently added the application PDB to the CDB and would like to sync its
applications with the CDB. The current container must be an application PDB.

With Release 21c you can use `EXCEPT` to exclude applications from `ALL`
`SYNC`.

Example

    
    
    ALTER PLUGGABLE DATABASE APPLICATION ALL EXCEPT hrapp payrollapp SYNC

Restrictions on Excluding Multiple Applications Using ALL SYNC

  * You cannot use the `SYNC TO` `version_string` clause while excluding multiple applications with `ALL EXCEPT SYNC`. 

  * You cannot use the `SYNC TO` `PATCH` `patch_number` clause while excluding multiple applications with `ALL EXCEPT SYNC`. 

snapshot_clauses

The snapshot clauses allow you to create and manage snapshots of the PDB for
the lifetime of the PDB.

pdb_snapshot_clause

Specify this clause to enable the creation of PDB snapshots. You can also
specify this clause in the `CREATE PLUGGABLE DATABASE` statement.

  * `NONE` is the default and means that no snapshots of the PDB can be created. 

  * `MANUAL` means that a snapshot of the PDB can be created only manually. 

  * If `snapshot_interval` is specified, PDB snapshots will be created automatically at the interval specified. In addition, a user will also be able to create PDB snapshots manually. 

  * If expressed in minutes, the `snapshot_interval` must be less than 3000. 

  * If expressed in hours, the `snapshot_interval` must be less than 2000. 

materialize_clause

Use this clause to convert a snapshot PDB into a full PDB clone. You can
delete and purge a PDB snapshot using the clause in this way.

  * This clause can only be specified for PDBs created as a snapshot.

  * All blocks in all datafiles belonging to the PDB will be copied.

create_snapshot_clause

Use this clause to manually create a PDB snapshot after connecting to the PDB.

  * This statement may be issued even if the PDB was set to have PDB snapshots created automatically. 

  * If a PDB Snapshot with the specified name already exists, an error will be reported.

  * A PDB Snapshot with specified name will be created.

drop_snapshot_clause

Use this clause to manually drop a PDB snapshot after connecting to the PDB.

  * If this snapshot is being used by some PDB, an error will be reported.

set_max_pdb_snapshots

Use this clause to increase or decrease the maximum number of snapshots for a
given PDB. You must first connect to the PDB.

  * If the PDB is not open in read/write mode when issuing the statement, an error is raised.

  * You can drop all PDB snapshots by setting the the max number to 0.

  * The maximum number of snapshots that you can set per PDB is 8.

prepare_clause

  * Use this clause to prepare mirror copies of the database. You must provide a `mirror_name` to identify the filegroup that is created. The created filegroup contains all the prepared files. 

  * Specify the number of copies to be prepared by the `REDUNDANCY` options: `EXTERNAL`, `NORMAL`, or `HIGH`. 

  * If you do not specify the redundancy of the mirror, the redundancy of the source database is used.

  * Use the `FOR DATABASE` clause to specify the new name of the CDB. This name should be unique. It will be used in the `create_pdb_from_mirror_copy` clause of the `CREATE PLUGGABLE DATABASE` statement. 

Prepare a Pluggable Database By Name: Example

If you specify the name ( `pdb_name`) of the pluggable database, it checks if
`pdb_name` matches with the current PDB. If it matches, it runs.

    
    
    ALTER PLUGGABLE DATABASE pdb_name PREPARE MIRROR COPY mirror_name WITH HIGH REDUNDANCY

Prepare a Pluggable Database Without a Name: Example

If you do not specify the name ( `pdb_name`) of the pluggable database, the
statement runs on the current PDB.

    
    
    ALTER PLUGGABLE DATABASE PREPARE MIRROR COPY mirror_name WITH HIGH REDUNDANCY

drop_mirror_copy

Use this clause to discard mirror copies of data and metadata created by the
prepare statement. You must specify the same mirror name that you used for the
prepare operation.

You cannot use this clause to drop a database that has already been split by
the `CREATE DATABASE` or `CREATE PLUGGABLE DATABASE` statement.

lost_write_protection

Turn on Lost Write for a Pluggable Database : Example

    
    
     ALTER PLUGGABLE DATABASE 
       ENABLE LOST WRITE PROTECTION

Turn off Lost Write for a Pluggable Database : Example

    
    
     ALTER PLUGGABLE DATABASE 
       DISABLE LOST WRITE PROTECTION

Note that disabling lost write for the database does not deallocate the lost
write storage. You must use the `DROP TABLESPACE` statement to deallocate lost
write storage.

pdb_managed_recovery

Specify this clause to recover a PDB in instances where the PDB is within a
physical standby CDB.

ENABLE | DISABLE BACKUP

PDB backup is enabled by default. To exclude the PDB from the backup, you can
specify disable.

Examples

Unplugging a PDB from a CDB: Example

The following statement unplugs PDB `pdb1` and stores metadata for the PDB
into XML file `/oracle/data/pdb1.xml`:

    
    
    ALTER PLUGGABLE DATABASE pdb1
      UNPLUG INTO '/oracle/data/pdb1.xml';

Modifying the Settings of a PDB: Example

The following statement changes the limit for the amount of storage used by
all tablespaces in PDB `pdb2` to 500M:

    
    
    ALTER PLUGGABLE DATABASE pdb2
      STORAGE (MAXSIZE 500M);

Taking the Data Files of a PDB Offline: Example

The following statement takes the data files associated with PDB `pdb3`
offline:

    
    
    ALTER PLUGGABLE DATABASE pdb3
      DATAFILE ALL OFFLINE;

Changing the State of a PDB: Examples

Assume that PDB `pdb4` is closedâthat is, its open mode is `MOUNTED`. The
following statement opens `pdb4` with open mode `READ` `ONLY`:

    
    
    ALTER PLUGGABLE DATABASE pdb4
      OPEN READ ONLY;
    

The following statement uses the `FORCE` keyword to change the open mode of
`pdb4` from `READ` `ONLY` to `READ` `WRITE`:

    
    
    ALTER PLUGGABLE DATABASE pdb4
      OPEN READ WRITE FORCE;
    

The following statement closes PDB `pdb4`:

    
    
    ALTER PLUGGABLE DATABASE pdb4
      CLOSE;
    

The following statement opens PDB pdb4 with open mode `READ` `ONLY`. Because
the `RESTRICTED` keyword is specified, the PDB is accessible only to users
with the `RESTRICTED` `SESSION` privilege in the PDB.

    
    
    ALTER PLUGGABLE DATABASE pdb4
      OPEN READ ONLY RESTRICTED;
    

Assume that PDB `pdb5` is closedâthat is, its open mode is `MOUNTED`. In an
Oracle Real Application Clusters environment, the following statement opens
PDB `pdb5` with open mode `READ` `WRITE` in instances `ORCLDB_1` and
`ORCLDB_2`:

    
    
    ALTER PLUGGABLE DATABASE pdb5
      OPEN READ WRITE INSTANCES = ('ORCLDB_1', 'ORCLDB_2');
    

In an Oracle Real Application Clusters environment, the following statement
closes PDB `pdb6` in the current instance and instructs the database to reopen
`pdb6` in instance `ORCLDB_3`:

    
    
    ALTER PLUGGABLE DATABASE pdb6
      CLOSE RELOCATE TO 'ORCLDB_3';

Changing the State of All PDBs in a CDB: Example

Assume that the current container is the root. The following statement opens
all PDBs in the CDB with open mode `READ` `ONLY`:

    
    
    ALTER PLUGGABLE DATABASE ALL
      OPEN READ ONLY;


[← Previous](ALTER-PACKAGE.md)

[Next →](alter-pmem-filestore.md)
