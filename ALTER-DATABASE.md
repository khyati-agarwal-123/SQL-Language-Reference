[Previous](ALTER-CLUSTER.md) [Next](ALTER-DATABASE-DICTIONARY.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER DATABASE 

## ALTER DATABASE

Purpose

Use the `ALTER` `DATABASE` statement to modify, maintain, or recover an
existing database.

See Also:

  * [Oracle Database Backup and Recovery User's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV8152) for examples of performing media recovery 

  * [Oracle Data Guard Concepts and Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SBYDB00300) for additional information on using the `ALTER` `DATABASE` statement to maintain standby databases 

  * [CREATE DATABASE](CREATE-DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C) for information on creating a database 

Prerequisites

You must have the `ALTER` `DATABASE` system privilege.

To specify the `startup_clauses`, you must also be connected `AS` `SYSDBA`,
`AS` `SYSOPER`, `AS` `SYSBACKUP`, or `AS` `SYSDG`.

To specify the `general_recovery` clause, you must also have the `SYSDBA` or
`SYSBACKUP` system privilege.

To specify the `DEFAULT` `EDITION` clause, you must also have the `USE` object
privilege `WITH` `GRANT` `OPTION` on the specified edition.

If you are connected to a multitenant container database (CDB):

  * To modify the entire CDB, the current container must be the root and you must have the commonly granted `ALTER` `DATABASE` privilege. 

  * To modify a container, it must be the current container and you must have the `ALTER` `DATABASE` privilege, either granted commonly or granted locally in the container. 

Notes on Using ALTER DATABASE in a CDB

When you issue the `ALTER` `DATABASE` statement while connected to a CDB, the
behavior of the statement depends on the current container and the clause(s)
you specify.

If the current container is the root, then `ALTER` `DATABASE` statements with
the following clauses modify the entire CDB. In order to specify these
clauses, you must have the commonly granted `ALTER` `DATABASE` privilege:

  * `startup_clauses`

  * `recovery_clauses`

Note: A subset of the `recovery_clauses` are supported to back up and recover
an individual pluggable database (PDB). In order to specify these clauses, you
must have the `ALTER` `DATABASE` privilege, either granted commonly or granted
locally in the PDB. Refer to "[Notes on Using the recovery_clauses in a
CDB](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGECCCCG)"
for more information.

  * `logfile_clauses`

  * `controlfile_clauses`

  * `standby_database_clauses`

  * `instance_clauses`

  * `security_clause`

  * `RENAME` `GLOBAL_NAME` `TO`

  * `ENABLE` `BLOCK` `CHANGE` `TRACKING`

  * `DISABLE` `BLOCK` `CHANGE` `TRACKING`

  * `undo_mode_clause`

If the current container is the root, then `ALTER` `DATABASE` statements with
the following clauses modify only the root. In order to specify these clauses,
you must have the `ALTER` `DATABASE` privilege, either granted commonly or
granted locally in the root:

  * `database_file_clauses`

  * `DEFAULT` `EDITION`

  * `DEFAULT` `TABLESPACE`

If the current container is the root, then `ALTER` `DATABASE` statements with
the following clauses modify the root and set default values for the PDBs. In
order to specify these clauses, you must have the commonly granted `ALTER`
`DATABASE` privilege:

  * `DEFAULT` [ `LOCAL` ] `TEMPORARY` `TABLESPACE`

  * `flashback_mode_clause`

  * `SET` `DEFAULT` `{` `BIGFILE` `|` `SMALLFILE` `}` `TABLESPACE`

  * `set_time_zone_clause`

If the current container is a PDB, then `ALTER` `DATABASE` statements modify
that PDB. In this case, you can issue only `ALTER` `DATABASE` clauses that are
also supported by the `ALTER` `PLUGGABLE` `DATABASE` statement. This
functionality is provided to maintain backward compatibility for applications
that have been migrated to a CDB environment. The exception is modifying PDB
storage limits, for which you must use the `pdb_storage_clause` of `ALTER`
`PLUGGABLE` `DATABASE`. Refer to the documentation on [ALTER PLUGGABLE
DATABASE](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7) for complete
information on these clauses.

Syntax

alter_database::=

  

![Description of alter_database.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_database.gif)  
[Description of the illustration
alter_database.eps](img_text/alter_database.md)

  

Groups of ALTER DATABASE syntax:

  * [startup_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2080129)

  * [recovery_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2080163)

  * [database_file_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2082829)

  * [logfile_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2191688)

  * [controlfile_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2078526)

  * [standby_database_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2078537)

  * [default_settings_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2078546)

  * [instance_clauses::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGBGGFBC)

  * [security_clause::=](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2110829)

database_clause::=

![Description of database_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/database_clause.gif)  
[Description of the illustration
database_clause.eps](img_text/database_clause.md)

startup_clauses::=

  

![Description of startup_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/startup_clauses.gif)  
[Description of the illustration
startup_clauses.eps](img_text/startup_clauses.md)

  

recovery_clauses::=

  

![Description of recovery_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/recovery_clauses.gif)  
[Description of the illustration
recovery_clauses.eps](img_text/recovery_clauses.md)

  

([general_recovery::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2191631),
[managed_standby_recovery::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2128273))

general_recovery::=

  

![Description of general_recovery.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/general_recovery.gif)  
[Description of the illustration
general_recovery.eps](img_text/general_recovery.md)

  

([full_database_recovery::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2128285),
[partial_database_recovery::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2128299),
[parallel_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2128310))

full_database_recovery::=

![Description of full_database_recovery.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/full_database_recovery.gif)  
[Description of the illustration
full_database_recovery.eps](img_text/full_database_recovery.md)

partial_database_recovery::=

![Description of partial_database_recovery.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/partial_database_recovery.gif)  
[Description of the illustration
partial_database_recovery.eps](img_text/partial_database_recovery.md)

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

managed_standby_recovery::=

![Description of managed_standby_recovery.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/managed_standby_recovery.gif)  
[Description of the illustration
managed_standby_recovery.eps](img_text/managed_standby_recovery.md)

([parallel_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2128310))

Note:

Several subclauses of `managed_standby_recovery` are no longer needed and have
been deprecated. These clauses no longer appear in the syntax diagrams. Refer
to the semantics of [managed_standby_recovery](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2079973).

database_file_clauses::=

![Description of database_file_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/database_file_clauses.gif)  
[Description of the illustration
database_file_clauses.eps](img_text/database_file_clauses.md)

([create_datafile_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2188488),
[alter_datafile_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2188492),
[alter_tempfile_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2188496),
[move_datafile_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGEIAHCA))

create_datafile_clause::=

![Description of create_datafile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_datafile_clause.gif)  
[Description of the illustration
create_datafile_clause.eps](img_text/create_datafile_clause.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF))

alter_datafile_clause::=

![Description of alter_datafile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_datafile_clause.gif)  
[Description of the illustration
alter_datafile_clause.eps](img_text/alter_datafile_clause.md)

([autoextend_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2131187),
[size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

alter_tempfile_clause::=

![Description of alter_tempfile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_tempfile_clause.gif)  
[Description of the illustration
alter_tempfile_clause.eps](img_text/alter_tempfile_clause.md)

([autoextend_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2131187),
[size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

move_datafile_clause::=

![Description of move_datafile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/move_datafile_clause.gif)  
[Description of the illustration
move_datafile_clause.eps](img_text/move_datafile_clause.md)

ASM_filename::=

![Description of asm_filename.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/asm_filename.gif)  
[Description of the illustration asm_filename.eps](img_text/asm_filename.md)

autoextend_clause::=

![Description of autoextend_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/autoextend_clause.gif)  
[Description of the illustration
autoextend_clause.eps](img_text/autoextend_clause.md)

maxsize_clause::=

![Description of maxsize_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/maxsize_clause.gif)  
[Description of the illustration
maxsize_clause.eps](img_text/maxsize_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

logfile_clauses::=

![Description of logfile_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logfile_clauses.gif)  
[Description of the illustration
logfile_clauses.eps](img_text/logfile_clauses.md)

([logfile_descriptor::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2153709),
[add_logfile_clauses::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208239),
[drop_logfile_clauses::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208250),
[switch_logfile_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGBFEFCC),
[supplemental_db_logging::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208261))

add_logfile_clauses::=

![Description of add_logfile_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_logfile_clauses.gif)  
[Description of the illustration
add_logfile_clauses.eps](img_text/add_logfile_clauses.md)

([redo_log_file_spec::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJABCHEE),
[logfile_descriptor::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2153709))

drop_logfile_clauses::=

![Description of drop_logfile_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_logfile_clauses.gif)  
[Description of the illustration
drop_logfile_clauses.eps](img_text/drop_logfile_clauses.md)

([logfile_descriptor::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2153709))

switch_logfile_clause::=

![Description of switch_logfile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/switch_logfile_clause.gif)  
[Description of the illustration
switch_logfile_clause.eps](img_text/switch_logfile_clause.md)

supplemental_db_logging::=

![Description of supplemental_db_logging.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/supplemental_db_logging.gif)  
[Description of the illustration
supplemental_db_logging.eps](img_text/supplemental_db_logging.md)

([supplemental_id_key_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208273))

supplemental_id_key_clause::=

![Description of supplemental_id_key_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/supplemental_id_key_clause.gif)  
[Description of the illustration
supplemental_id_key_clause.eps](img_text/supplemental_id_key_clause.md)

supplemental_plsql_clause::=

![Description of supplemental_plsql_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/supplemental_plsql_clause.gif)  
[Description of the illustration
supplemental_plsql_clause.eps](img_text/supplemental_plsql_clause.md)

supplemental_subset_replication_clause

![Description of supplemental_subset_replication_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/supplemental_subset_replication_clause.gif)  
[Description of the illustration
supplemental_subset_replication_clause.eps](img_text/supplemental_subset_replication_clause.md)

logfile_descriptor::=

![Description of logfile_descriptor.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logfile_descriptor.gif)  
[Description of the illustration
logfile_descriptor.eps](img_text/logfile_descriptor.md)

controlfile_clauses::=

![Description of controlfile_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/controlfile_clauses.gif)  
[Description of the illustration
controlfile_clauses.eps](img_text/controlfile_clauses.md)

([trace_file_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208285))

trace_file_clause::=

![Description of trace_file_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/trace_file_clause.gif)  
[Description of the illustration
trace_file_clause.eps](img_text/trace_file_clause.md)

standby_database_clauses::=

![Description of standby_database_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/standby_database_clauses.gif)  
[Description of the illustration
standby_database_clauses.eps](img_text/standby_database_clauses.md)

([activate_standby_db_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208296),
[maximize_standby_db_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208307),
[register_logfile_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208318),
[commit_switchover_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208329),
[start_standby_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208340),
[stop_standby_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208351),
[convert_database_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGBEFBFC),
[parallel_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2128310),
[switchover_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGEFBEFD),
[failover_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGEGHAAC))

activate_standby_db_clause::=

![Description of activate_standby_db_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/activate_standby_db_clause.gif)  
[Description of the illustration
activate_standby_db_clause.eps](img_text/activate_standby_db_clause.md)

maximize_standby_db_clause::=

![Description of maximize_standby_db_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/maximize_standby_db_clause.gif)  
[Description of the illustration
maximize_standby_db_clause.eps](img_text/maximize_standby_db_clause.md)

register_logfile_clause::=

![Description of register_logfile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/register_logfile_clause.gif)  
[Description of the illustration
register_logfile_clause.eps](img_text/register_logfile_clause.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF))

switchover_clause::=

![Description of switchover_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/switchover_clause.gif)  
[Description of the illustration
switchover_clause.eps](img_text/switchover_clause.md)

failover_clause::=

![Description of failover_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/failover_clause.gif)  
[Description of the illustration
failover_clause.eps](img_text/failover_clause.md)

commit_switchover_clause::=

![Description of commit_switchover_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/commit_switchover_clause.gif)  
[Description of the illustration
commit_switchover_clause.eps](img_text/commit_switchover_clause.md)

start_standby_clause::=

![Description of start_standby_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/start_standby_clause.gif)  
[Description of the illustration
start_standby_clause.eps](img_text/start_standby_clause.md)

stop_standby_clause::=

![Description of stop_standby_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/stop_standby_clause.gif)  
[Description of the illustration
stop_standby_clause.eps](img_text/stop_standby_clause.md)

convert_database_clause::=

![Description of convert_database_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/convert_database_clause.gif)  
[Description of the illustration
convert_database_clause.eps](img_text/convert_database_clause.md)

default_settings_clauses::=

![Description of default_settings_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_settings_clauses.gif)  
[Description of the illustration
default_settings_clauses.eps](img_text/default_settings_clauses.md)

([flashback_mode_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208395),
[undo_mode_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__UNDO_MODE_CLAUSE-53B3B8E9),
[set_time_zone_clause::=](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208406))

flashback_mode_clause::=

![Description of flashback_mode_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/flashback_mode_clause.gif)  
[Description of the illustration
flashback_mode_clause.eps](img_text/flashback_mode_clause.md)

undo_mode_clause::=

![Description of undo_mode_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/undo_mode_clause.gif)  
[Description of the illustration
undo_mode_clause.eps](img_text/undo_mode_clause.md)

set_time_zone_clause::=

![Description of set_time_zone_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/set_time_zone_clause.gif)  
[Description of the illustration
set_time_zone_clause.eps](img_text/set_time_zone_clause.md)

instance_clauses::=

![Description of instance_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/instance_clauses.gif)  
[Description of the illustration
instance_clauses.eps](img_text/instance_clauses.md)

security_clause::=

![Description of security_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/security_clause.gif)  
[Description of the illustration
security_clause.eps](img_text/security_clause.md)

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

![Description of lost_write_protection.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lost_write_protection.gif)  
[Description of the illustration
lost_write_protection.eps](img_text/lost_write_protection.md)

cdb_fleet_clauses::=

![Description of cdb_fleet_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cdb_fleet_clauses.gif)  
[Description of the illustration
cdb_fleet_clauses.eps](img_text/cdb_fleet_clauses.md)

lead_cdb_clause::=

![Description of lead_cdb_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lead_cdb_clause.gif)  
[Description of the illustration
lead_cdb_clause.eps](img_text/lead_cdb_clause.md)

lead_cdb_uri_clause::=

![Description of lead_cdb_uri_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lead_cdb_uri_clause.gif)  
[Description of the illustration
lead_cdb_uri_clause.eps](img_text/lead_cdb_uri_clause.md)

property_clause

![Description of property_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/property_clause.gif)  
[Description of the illustration
property_clause.eps](img_text/property_clause.md)

replay_upgrade_clause::=

  

![Description of replay_upgrade_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/replay_upgrade_clause.gif)  
[Description of the illustration
replay_upgrade_clause.eps](img_text/replay_upgrade_clause.md)

  

Semantics

database_clause

Specify the `DATABASE` option for a non-container database.

db_name

Specify the name of the database to be altered. If you omit `db_name`, then
Oracle Database alters the database identified by the value of the
initialization parameter `DB_NAME`. You can alter only the database whose
control files are specified by the initialization parameter `CONTROL_FILES`.
The database identifier is not related to the Oracle Net database
specification.

startup_clauses

The `startup_clauses` let you mount and open the database so that it is
accessible to users.

MOUNT Clause

Use the `MOUNT` clause to mount the database. Do not use this clause when the
database is already mounted.

MOUNT STANDBY DATABASE

You can specify `MOUNT` `STANDBY` `DATABASE` to mount a physical standby
database. The keywords `STANDBY` `DATABASE` are optional, because Oracle
Database determines automatically whether the database to be mounted is a
primary or standby database. As soon as this statement executes, the standby
instance can receive redo data from the primary instance.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00300) for more information on standby databases

MOUNT CLONE DATABASE

Specify `MOUNT` `CLONE` `DATABASE` to mount the clone database.

OPEN Clause

Use the `OPEN` clause to make the database available for normal use. You must
mount the database before you can open it.

If you specify only `OPEN` without any other keywords, then the default is
`OPEN` `READ` `WRITE` `NORESETLOGS` on a primary database, logical standby
database, or snapshot standby database and `OPEN` `READ` `ONLY` on a physical
standby database.

OPEN READ WRITE

Specify `OPEN` `READ` `WRITE` to open the database in read/write mode,
allowing users to generate redo logs. This is the default if you are opening a
primary database. You cannot specify this clause for a physical standby
database.

See Also:

"[READ ONLY / READ WRITE: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135540)"

RESETLOGS | NORESETLOGS

This clause determines whether Oracle Database resets the current log sequence
number to 1, archives any unarchived logs (including the current log), and
discards any redo information that was not applied during recovery, ensuring
that it will never be applied. Oracle Database uses `NORESETLOGS`
automatically except in the following specific situations, which require a
setting for this clause:

  * You must specify `RESETLOGS`: 

    * After performing incomplete media recovery or media recovery using a backup control file

    * After a previous `OPEN` `RESETLOGS` operation that did not complete 

    * After a `FLASHBACK` `DATABASE` operation 

  * If a created control file is mounted, then you must specify `RESETLOGS` if the online logs are lost, or you must specify `NORESETLOGS` if they are not lost. 

UPGRADE | DOWNGRADE

Use these `OPEN` clause parameters only if you are upgrading or downgrading a
database. This clause instructs Oracle Database to modify system parameters
dynamically as required for upgrade and downgrade, respectively. You can
achieve the same result using the SQL*Plus `STARTUP` `UPGRADE` or `STARTUP`
`DOWNGRADE` command.

When you use the `UPGRADE` or `DOWNGRADE` parameters for a CDB, the root
container is opened in the specified mode, but all other containers are opened
in `READ WRITE` mode.

See Also:

  * Oracle Database Upgrade Guide for information on the steps required to [upgrade](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=UPGRD003) or [downgrade](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=UPGRD007) a database from one release to another 

  * [SQL*Plus User's Guide and Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SQPUG128) for information on the SQL*Plus `STARTUP` command 

OPEN READ ONLY

Specify `OPEN` `READ` `ONLY` to restrict users to read-only transactions,
preventing them from generating redo logs. This setting is the default when
you are opening a physical standby database, so that the physical standby
database is available for queries even while archive logs are being copied
from the primary database site.

Restrictions on Opening a Database

The following restrictions apply to opening a database:

  * You cannot open a database in `READ` `ONLY` mode if it is currently opened in `READ` `WRITE` mode by another instance. 

  * You cannot open a database in `READ` `ONLY` mode if it requires recovery. 

  * You cannot take tablespaces offline while the database is open in `READ` `ONLY` mode. However, you can take data files offline and online, and you can recover offline data files and tablespaces while the database is open in `READ` `ONLY` mode. 

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00706) for additional information about opening a
physical standby database

recovery_clauses

The `recovery_clauses` include post-backup operations. For all of these
clauses, Oracle Database recovers the database using any incarnations of data
files and log files that are known to the current control file.

See Also:

[Oracle Database Backup and Recovery User's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV8001) for information on backing up the database and
"[Database Recovery: Examples](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135908)"

Notes on Using the recovery_clauses in a CDB

When the current container is the root, you can specify all of the
`recovery_clauses` to back up and recover the entire CDB.

When the current container is a PDB, you can specify the following subclauses
of the `recovery_clauses` to back up and recover the PDB:

  * `BEGIN` `BACKUP`

  * `END` `BACKUP`

  * `full_database_recovery`: You can specify only the `DATABASE` keyword 

  * `partial_database_recovery`

  * The `LOGFILE` and `CONTINUE` clauses of `general_recovery`

You can also specify the preceding subclauses using the `pdb_recovery_clauses`
of `ALTER` `PLUGGABLE` `DATABASE`. Refer to the syntax diagram
[pdb_recovery_clauses](ALTER-PLUGGABLE-
DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__CCHDJFHH) of `ALTER`
`PLUGGABLE` `DATABASE`.

general_recovery

The `general_recovery` clause lets you control media recovery for the database
or standby database or for specified tablespaces or files. You can use this
clause when your instance has the database mounted, open or closed, and the
files involved are not in use.

Note:

Parallelism is enabled by default during full or partial database recovery and
logfile recovery. The database computes the degree of parallelism. You can
disable parallelism of these operations by specifying `NOPARALLEL`, or specify
a degree of parallelism with `PARALLEL` `integer`, as shown in the respective
syntax diagrams.

Restrictions on General Database Recovery

General recovery is subject to the following restrictions:

  * You can recover the entire database only when the database is closed. 

  * Your instance must have the database mounted in exclusive mode.

  * You can recover tablespaces or data files when the database is open or closed, if the tablespaces or data files to be recovered are offline. 

  * You cannot perform media recovery if you are connected to Oracle Database through the shared server architecture. 

See Also:

  * [Oracle Database Backup and Recovery User's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV8152) for more information on [RMAN media recovery](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV8152) and user-defined media recovery 

  * [SQL*Plus User's Guide and Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SQPUG053) for information on the SQL*Plus `RECOVER` command 

AUTOMATIC

Specify `AUTOMATIC` if you want Oracle Database to automatically generate the
name of the next archived redo log file needed to continue the recovery
operation. If the `LOG_ARCHIVE_DEST_``n` parameters are defined, then Oracle
Database scans those that are valid and enabled for the first local
destination. It uses that destination in conjunction with `LOG_ARCHIVE_FORMAT`
to generate the target redo log filename. If the `LOG_ARCHIVE_DEST_``n`
parameters are not defined, then Oracle Database uses the value of the
`LOG_ARCHIVE_DEST` parameter instead.

If the resulting file is found, then Oracle Database applies the redo
contained in that file. If the file is not found, then Oracle Database prompts
you for a filename, displaying the generated filename as a suggestion.

If you specify neither `AUTOMATIC` nor `LOGFILE`, then Oracle Database prompts
you for a filename, displaying the generated filename as a suggestion. You can
then accept the generated filename or replace it with a fully qualified
filename. If you know that the archived filename differs from what Oracle
Database would generate, then you can save time by using the `LOGFILE` clause.

FROM 'location'

Specify `FROM` `'location'` to indicate the location from which the archived
redo log file group is read. The value of `location` must be a fully specified
file location following the conventions of your operating system. If you omit
this parameter, then Oracle Database assumes that the archived redo log file
group is in the location specified by the initialization parameter
`LOG_ARCHIVE_DEST` or `LOG_ARCHIVE_DEST_1`.

full_database_recovery

The `full_database_recovery` clause lets you recover an entire database.

DATABASE

Specify the `DATABASE` clause to recover the entire database. This is the
default. You can use this clause only when the database is closed.

STANDBY DATABASE

Specify the `STANDBY` `DATABASE` clause to manually recover a physical standby
database using the control file and archived redo log files copied from the
primary database. The standby database must be mounted but not open.

This clause recovers only online data files.

  * Use the `UNTIL` clause to specify the duration of the recovery operation. 

    * `CANCEL` indicates cancel-based recovery. This clause recovers the database until you issue the `ALTER` `DATABASE` statement with the `RECOVER` `CANCEL` clause. 

    * `TIME` indicates time-based recovery. This parameter recovers the database to the time specified by the date. The date must be a character literal in the format `'YYYY-MM-DD:HH24:MI:SS'`. 

    * `CHANGE` indicates change-based recovery. This parameter recovers the database to a transaction-consistent state immediately before the system change number specified by `integer`. 

    * `CONSISTENT` recovers the database until all online files are brought to a consistent SCN point so that the database can be open in read only mode. This clauses requires the controlfile to be a backup controlfile. 

  * Specify `USING` `BACKUP` `CONTROLFILE` if you want to use a backup control file instead of the current control file. 

  * Specify the `SNAPSHOT` `TIME` clause to recover the database with a storage snapshot using Storage Snapshot Optimization. This clause can be used in cases where the database was not placed in backup mode when the storage snapshot was created. 

    * `date` must be a character literal in the format `'YYYY-MM-DD:HH24:MI:SS'`. It must represent a time that is immediately after the snapshot was completed. If you specify the `UNTIL` `TIME` clause, then `SNAPSHOT` `TIME` `date` must be earlier than `UNTIL` `TIME` `date`. 

See Also:

[Oracle Database Backup and Recovery User's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV727) for more information on recovery using Storage
Snapshot Optimization

partial_database_recovery

The `partial_database_recovery` clause lets you recover individual tablespaces
and data files.

TABLESPACE

Specify the `TABLESPACE` clause to recover only the specified tablespaces. You
can use this clause if the database is open or closed, provided the
tablespaces to be recovered are offline.

See Also:

"[Using Parallel Recovery Processes: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2104508)"

DATAFILE

Specify the `DATAFILE` clause to recover the specified data files. You can use
this clause when the database is open or closed, provided the data files to be
recovered are offline.

You can identify the data file by name or by number. If you identify it by
number, then `filenumber` is an integer representing the number found in the
`FILE#` column of the `V$DATAFILE` dynamic performance view or in the
`FILE_ID` column of the `DBA_DATA_FILES` data dictionary view.

STANDBY {TABLESPACE | DATAFILE}

In earlier releases, you could specify `STANDBY` `TABLESPACE` or `STANDBY`
`DATAFILE` to recover older backups of a specific tablespace or a specific
data file on the standby to be consistent with the rest of the standby
database. These two clauses are now desupported. Instead, to recover the
standby database to a consistent point, but no further, use the statement
`ALTER` `DATABASE` `RECOVER` `MANAGED` `STANDBY` `DATABASE` `UNTIL`
`CONSISTENT`.

LOGFILE

Specify the `LOGFILE` '`filename`' to continue media recovery by applying the
specified redo log file.

TEST

Use the `TEST` clause to conduct a trial recovery. A trial recovery is useful
if a normal recovery procedure has encountered some problem. It lets you look
ahead into the redo stream to detect possible additional problems. The trial
recovery applies redo in a way similar to normal recovery, but it does not
write changes to disk, and it rolls back its changes at the end of the trial
recovery.

You can use this clause only if you have restored a backup taken since the
last `RESETLOGS` operation. Otherwise, Oracle Database returns an error.

ALLOW ... CORRUPTION

The `ALLOW` `integer` `CORRUPTION` clause lets you specify, in the event of
logfile corruption, the number of corrupt blocks that can be tolerated while
allowing recovery to proceed.

See Also:

  * [Oracle Database Backup and Recovery User's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV8001) for information on database recovery in general 

  * [Oracle Data Guard Concepts and Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SBYDB00530) for information on managed recovery of standby databases 

CONTINUE

Specify `CONTINUE` to continue multi-instance recovery after it has been
interrupted to disable a thread.

Specify `CONTINUE` `DEFAULT` to continue recovery using the redo log file that
Oracle Database would automatically generate if no other logfile were
specified. This clause is equivalent to specifying `AUTOMATIC`, except that
Oracle Database does not prompt for a filename.

CANCEL

Specify `CANCEL` to terminate cancel-based recovery.

managed_standby_recovery

Use the `managed_standby_recovery` clause to start and stop Redo Apply on a
physical standby database. Redo Apply keeps the standby database
transactionally consistent with the primary database by continuously applying
redo received from the primary database.

A primary database transmits its redo data to standby sites. As the redo data
is written to redo log files at the physical standby site, the log files
become available for use by Redo Apply. You can use the
`managed_standby_recovery` clause when your standby instance has the database
mounted or is opened read-only.

Note:

Beginning with Oracle Database 12c, real-time apply is enabled by default
during Redo Apply. Real-time apply recovers redo from the standby redo log
files as soon as they are written, without requiring them to be archived first
at the physical standby database. You can disable real-time apply with the
`USING` `ARCHIVED` `LOGFILE` clause. Refer to:

  * [Oracle Data Guard Concepts and Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SBYDB0050) for more information on real-time apply 

  * [USING ARCHIVED LOGFILE Clause](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGECJDHB)

Note:

Parallelism is enabled by default during Redo Apply. The database computes the
degree of parallelism. You can disable parallelism of these operations by
specifying `NOPARALLEL`, or specify a degree of parallelism with `PARALLEL`
`integer`, as shown in the respective syntax diagrams.

Restrictions on Managed Standby Recovery

The same restrictions listed under [general_recovery](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2208874) apply to
this clause.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00530) for more information on the use of this
clause

USING ARCHIVED LOGFILE Clause

Specify `USING` `ARCHIVED` `LOGFILE` to start Redo Apply without enabling
real-time apply.

DISCONNECT

Specify `DISCONNECT` to indicate that Redo Apply should be performed in the
background, leaving the current session available for other tasks. The `FROM`
`SESSION` keywords are optional and are provided for semantic clarity.

NODELAY

The `NODELAY` clause overrides the `DELAY` attribute on the
`LOG_ARCHIVE_DEST_n` parameter on the primary database. If you do not specify
the `NODELAY` clause, then application of the archived redo log file is
delayed according to the `DELAY` attribute of the `LOG_ARCHIVE_DEST_``n`
setting (if any). If the `DELAY` attribute was not specified on that
parameter, then the archived redo log file is applied immediately to the
standby database.

If you specify real-time apply with the `USING` `CURRENT` `LOGFILE` clause,
then any `DELAY` value specified for the `LOG_ARCHIVE_DEST_``n` parameter at
the primary for this standby is ignored, and `NODELAY` is the default.

UNTIL CHANGE Clause

Use this clause to instruct Redo Apply to recover redo data up to, but not
including, the specified system change number.

UNTIL CONSISTENT

Use this clause to recover the standby database to a consistent SCN point so
that the standby database can be opened in read only mode.

USING INSTANCES

This clause is applicable only for Oracle Real Application Clusters (Oracle
RAC) or Oracle RAC One Node databases and allows you to start apply processes
on multiple instances of the standby that are started in the same mode
(`MOUNTED` or `READ` `ONLY`) as the instance on which the command is executed.
Specify `USING` `INSTANCES` `ALL` to perform Redo Apply on all instances in an
Oracle RAC standby database started in the same mode. Specify `USING`
`INSTANCES` `integer` to perform Redo Apply on the specified number of
instances that are started in the same mode. For `integer`, specify an integer
value from 1 to the number of instances in the standby database. The database
chooses the instances on which to perform Redo Apply; you cannot specify
particular instances. For example, if you specify 4 instances from an instance
that is `MOUNTED` and only 3 instances of the standby are running in the
`MOUNTED` mode, then Redo Apply will only be started on 3 instances. If you
omit the `USING` `INSTANCES` clause, then Oracle Database performs Redo Apply
only on the instance where the command was executed.

FINISH

Specify `FINISH` to complete applying all available redo data in preparation
for a failover.

Use the `FINISH` clause only in the event of the failure of the primary
database. This clause overrides any specified delay intervals and applies all
available redo immediately. After the `FINISH` command completes, this
database can no longer run in the standby database role, and it must be
converted to a primary database by issuing the `ALTER` `DATABASE` `COMMIT`
`TO` `SWITCHOVER` `TO` `PRIMARY` statement.

CANCEL

Specify `CANCEL` to stop Redo Apply immediately. Control is returned as soon
as Redo Apply stops.

TO LOGICAL STANDBY Clause

Use this clause to convert a physical standby database into a logical standby
database.

db_name

Specify a database name to identify the new logical standby database. If you
are using a server parameter file (spfile) at the time you issue this
statement, then the database will update the file with appropriate information
about the new logical standby database. If you are not using an spfile, then
the database issues a message reminding you to set the name of the `DB_NAME`
parameter after shutting down the database. In addition, you must invoke the
`DBMS_LOGSTDBY.BUILD` PL/SQL procedure on the primary database before using
this clause on the standby database.

See Also:

[Oracle Database PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS363) for information about the `DBMS_LOGSTDBY.BUILD`
procedure

KEEP IDENTITY

Use this clause if you want to use the rolling upgrade feature provided by a
logical standby and also revert to the original configuration of a primary
database and a physical standby. A logical standby database created using this
clause provides only limited support for switchover and failover. Therefore,
do not use this clause create a general-purpose logical standby database.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00830) for more information on rolling upgrade

Deprecated Managed Standby Recovery Clauses

The following clauses appeared in the syntax of earlier releases. They have
been deprecated and are no longer needed. Oracle recommends that you do not
use these clauses.

FINISH FORCE, FINISH WAIT, FINISH NOWAIT

These optional forms of the `FINISH` clause are deprecated. Their semantics
are presented here for backward compatibility:

  * `FORCE` terminates inactive redo transport sessions that would otherwise prevent `FINISH` processing from beginning. 

  * `NOWAIT` returns control to the foreground process before the recovery completes 

  * `WAIT` (the default) returns control to the foreground process after recovery completes 

When specified, these clauses are ignored. Terminal recovery now runs in the
foreground and always terminates all redo transport sessions. Therefore
control is not returned to the user until recovery completes.

CANCEL IMMEDIATE, CANCEL WAIT, CANCEL NOWAIT

These optional forms of the `CANCEL` clause are deprecated. Their semantics
are presented here for backward compatibility:

  * Include the `IMMEDIATE` keyword to stop Redo Apply before completely applying the current redo log file. Session control returns when Redo Apply actually stops. 

  * Include the `NOWAIT` keyword to return session control without waiting for the `CANCEL` operation to complete. 

When specified, these clauses are ignored. Redo Apply is now always cancelled
immediately and control returns to the session only after the operation
completes.

USING CURRENT LOGFILE Clause

The `USING` `CURRENT` `LOGFILE` clause is deprecated. It invokes real-time
apply during Redo Apply. However, this is now the default behavior and this
clause is no longer useful.

BACKUP Clauses

Use these clauses to move all the data files in the database into or out of
online backup mode (also called hot backup mode).

See Also:

[ALTER TABLESPACE](ALTER-TABLESPACE.md#GUID-
CA074861-55D3-4768-8995-43D4DA26365D) for information on moving all data files
in an individual tablespace into and out of online backup mode

BEGIN BACKUP Clause

Specify `BEGIN` `BACKUP` to move all data files in the database into online
backup mode. The database must be mounted and open, and media recovery must be
enabled (the database must be in `ARCHIVELOG` mode).

While the database is in online backup mode, you cannot shut down the instance
normally, begin backup of an individual tablespace, or take any tablespace
offline or make it read only.

This clause has no effect on data files that are in offline or on read-only
tablespaces.

END BACKUP Clause

Specify `END` `BACKUP` to take out of online backup mode any data files in the
database currently in online backup mode. The database must be mounted (either
open or closed) when you perform this operation.

After a system failure, instance failure, or `SHUTDOWN` `ABORT` operation,
Oracle Database does not know whether the files in online backup mode match
the files at the time the system crashed. If you know the files are
consistent, then you can take either individual data files or all data files
out of online backup mode. Doing so avoids media recovery of the files upon
startup.

  * To take an individual data file out of online backup mode, use the `ALTER` `DATABASE` `DATAFILE` ... `END` `BACKUP` statement. See [database_file_clauses](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2078824). 

  * To take all data files in a tablespace out of online backup mode, use an `ALTER` `TABLESPACE` ... `END` `BACKUP` statement. 

database_file_clauses

The `database_file_clauses` let you modify data files and temp files. You can
use any of the following clauses when your instance has the database mounted,
open or closed, and the files involved are not in use. The exception is the
`move_datafile_clause`, which allows you to move a data file that is in use.

RENAME FILE Clause

Use the `RENAME` `FILE` clause to rename data files, temp files, or redo log
file members. You must create each filename using the conventions for
filenames on your operating system before specifying this clause.

  * To use this clause for a data file or temp file, the database must be mounted. The database can also be open, but the data file or temp file being renamed must be offline. In addition, you must first rename the file on the file system to the new name.

  * To use this clause for logfiles, the database must be mounted but not open.

  * If you have enabled block change tracking, then you can use this clause to rename the block change tracking file. The database must be mounted but not open when you rename the block change tracking file.

This clause renames only files in the control file. It does not actually
rename them on your operating system. The operating system files continue to
exist, but Oracle Database no longer uses them.

See Also:

  * [Oracle Database Backup and Recovery User's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=BRADV8152) for information on recovery of data files and temp files 

  * "[Renaming a Log File Member: Example](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135684)" and "[Manipulating Temp Files: Example](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__BGBGEDFB)"

create_datafile_clause

Use the `CREATE` `DATAFILE` clause to create a new empty data file in place of
an old one. You can use this clause to re-create a data file that was lost
with no backup. The `filename` or `filenumber` must identify a file that is or
was once part of the database. If you identify the file by number, then
`filenumber` is an integer representing the number found in the `FILE#` column
of the `V$DATAFILE` dynamic performance view or in the `FILE_ID` column of the
`DBA_DATA_FILES` data dictionary view.

  * Specify `AS` `NEW` to create an Oracle-managed data file with a system-generated filename, the same size as the file being replaced, in the default file system location for data files. 

  * Specify `AS` `file_specification` to assign a file name (and optional size) to the new data file. Use the `datafile_tempfile_spec` form of `file_specification` (see [file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)) to list regular data files and temp files in an operating system file system or to list Oracle Automatic Storage Management (Oracle ASM) disk group files. 

If the original file (`filename` or `filenumber`) is an existing Oracle-
managed data file, then Oracle Database attempts to delete the original file
after creating the new file. If the original file is an existing user-managed
data file, then Oracle Database does not attempt to delete the original file.

If you omit the `AS` clause entirely, then Oracle Database creates the new
file with the same name and size as the file specified by `filename` or
`filenumber`.

During recovery, all archived redo logs written to since the original data
file was created must be applied to the new, empty version of the lost data
file.

Oracle Database creates the new file in the same state as the old file when it
was created. You must perform media recovery on the new file to return it to
the state of the old file at the time it was lost.

Restrictions on Creating New Data Files

The creation of new data files is subject to the following restrictions:

  * You cannot create a new file based on the first data file of the `SYSTEM` tablespace. 

  * You cannot specify the `autoextend_clause` of `datafile_tempfile_spec` in this `CREATE` `DATAFILE` clause. 

See Also:

  * "[DATAFILE Clause](CREATE-CONTROLFILE.md#GUID-9B389F28-C4D0-405D-BFE6-48237E8BD791__I2160226)" of `CREATE` `DATABASE` for information on the result of this clause if you do not specify a name for the new data file 

  * [file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688) for a full description of the file specification (`datafile_tempfile_spec`) and "[Creating a New Data File: Example](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135811)"

alter_datafile_clause

The `DATAFILE` clause lets you manipulate a file that you identify by name or
by number. If you identify it by number, then `filenumber` is an integer
representing the number found in the `FILE#` column of the `V$DATAFILE`
dynamic performance view or in the `FILE_ID` column of the `DBA_DATA_FILES`
data dictionary view. The `DATAFILE` clauses affect your database files as
follows:

ONLINE

Specify `ONLINE` to bring the data file online.

OFFLINE

Specify `OFFLINE` to take the data file offline. If the database is open, then
you must perform media recovery on the data file before bringing it back
online, because a checkpoint is not performed on the data file before it is
taken offline.

FOR DROP

If the database is in `NOARCHIVELOG` mode, then you must specify `FOR` `DROP`
clause to take a data file offline. However, this clause does not remove the
data file from the database. To do that, you must use an operating system
command or drop the tablespace in which the data file resides. Until you do
so, the data file remains in the data dictionary with the status `RECOVER` or
`OFFLINE`.

If the database is in `ARCHIVELOG` mode, then Oracle Database ignores the
`FOR` `DROP` clause.

RESIZE

Specify `RESIZE` if you want Oracle Database to attempt to increase or
decrease the size of the data file to the specified absolute size in bytes.
There is no default, so you must specify a size. You can also use this command
to resize datafiles in shadow tablespaces, that store lost write data.

If sufficient disk space is not available for the increased size, or if the
file contains data beyond the specified decreased size, then Oracle Database
returns an error.

See Also:

"[Resizing a Data File: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135881)"

END BACKUP

Specify `END` `BACKUP` to take the data file out of online backup mode. The
`END` `BACKUP` clause is described more fully at the top level of the syntax
of `ALTER` `DATABASE`. See "[END BACKUP Clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2150184)".

ENCRYPT | DECRYPT

Use these clauses to perform offline encryption or decryption of the data file
using Transparent Data Encryption (TDE). In any given tablespace, either all
data files must be encrypted or all data files must be unencrypted.

Before issuing either of these clauses, the database must be mounted. The
database can also be open, but the tablespace that contains the data file
being encrypted or decrypted must be offline. The TDE master key must be
loaded into database memory.

  * Specify `ENCRYPT` to encrypt an unencrypted data file. The data file is encrypted using the `AES128` algorithm. 

  * Specify `DECRYPT` to decrypt a data file. The data file must have been previously encrypted with the `ALTER` `DATABASE` `DATAFILE` ... `ENCRYPT` statement. 

Restrictions on Encrypting and Decrypting Data Files

The following restrictions apply to the `ENCRYPT` and `DECRYPT` clauses:

  * You cannot encrypt or decrypt a temporary data file of a temporary tablespace. Instead, you must drop the temporary tablespace and recreate it as an encrypted tablespace.

  * Oracle recommends against encrypting the data files of an undo tablespace. Doing so prevents the keystore from being closed, which prevents the database from functioning. Furthermore, this practice is unnecessary because all undo records that are associated with an encrypted tablespace are already automatically encrypted in the undo tablespace.

Note:

The use of the `ENCRYPT` or `DECRYPT` clause is only one step in a series of
steps for performing offline encryption or decryption of a data file. Refer to
[Oracle Database Advanced Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ASOAG-GUID-DE533D60-C711-4ECD-AB1B-36E41A331A35) for the
complete set of steps before you use either of these clauses.

alter_tempfile_clause

Use the `TEMPFILE` clause to resize your temporary data file or specify the
`autoextend_clause`, with the same effect as for a permanent data file. The
database must be open. You can identify the temp file by name or by number. If
you identify it by number, then `filenumber` is an integer representing the
number found in the `FILE#` column of the `V$TEMPFILE` dynamic performance
view.

Note:

On some operating systems, Oracle does not allocate space for a temp file
until the temp file blocks are actually accessed. This delay in space
allocation results in faster creation and resizing of temp files, but it
requires that sufficient disk space is available when the temp files are later
used. To avoid potential problems, before you create or resize a temp file,
ensure that the available disk space exceeds the size of the new temp file or
the increased size of a resized temp file. The excess space should allow for
anticipated increases in disk space use by unrelated operations as well. Then
proceed with the creation or resizing operation.

DROP

Specify `DROP` to drop `tempfile` from the database. The tablespace remains.

If you specify `INCLUDING` `DATAFILES`, then Oracle Database also deletes the
associated operating system files and writes a message to the alert log for
each such deleted file. You can achieve the same result using an `ALTER`
`TABLESPACE` ... `DROP` `TEMPFILE` statement. Refer to the `ALTER`
`TABLESPACE` [DROP Clause](ALTER-TABLESPACE.md#GUID-
CA074861-55D3-4768-8995-43D4DA26365D__CIHBAGCD) for more information.

move_datafile_clause

Use the `MOVE` `DATAFILE` clause to move an online data file to a new
location. The database can be open and accessing the data file when you
perform this operation. The database creates a copy of the data file when it
is performing this operation. Ensure that there is adequate disk space for the
original data file and the copy before using this clause.

You can specify the original data file using the `file_name`, `ASM_filename`,
or `file_number`. Refer to
[ASM_filename](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1026664)
for information on ASM file names. If you identify the file by number, then
`file_number` is an integer representing the number found in the `FILE#`
column of the `V$DATAFILE` dynamic performance view or in the `FILE_ID` column
of the `DBA_DATA_FILES` data dictionary view.

Use the `TO` clause to specify the new `file_name` or `ASM_filename`. If you
are using Oracle Managed Files, then you can omit the `TO` clause. In this
case, Oracle Database creates a unique name for the data file and saves it in
the directory specified by the `DB_CREATE_FILE_DEST` initialization parameter.

If you specify `REUSE`, then the new data file is created even if it already
exists.

If you specify `KEEP`, then the original data file will be kept after the
`MOVE` `DATAFILE` operation. You cannot specify `KEEP` if the original data
file is an Oracle Managed File. You can specify `KEEP` if the new data file is
an Oracle Managed File.

autoextend_clause

Use the `autoextend_clause` to enable or disable the automatic extension of a
new or existing data file or temp file. Refer to
[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)
for information about this clause.

logfile_clauses

The logfile clauses let you add, drop, or modify log files.

ARCHIVELOG``

Specify `ARCHIVELOG` if you want the contents of a redo log file group to be
archived before the group can be reused. This mode prepares for the
possibility of media recovery. Use this clause only after shutting down your
instance normally, or immediately with no errors, and then restarting it and
mounting the database.

MANUAL

Specify `MANUAL` to indicate that Oracle Database should create redo log
files, but the archiving of the redo log files is controlled entirely by the
user. This clause is provided for backward compatibility, for example for
users who archive directly to tape. If you specify `MANUAL`, then:

  * Oracle Database does not archive redo log files when a log switch occurs. You must handle this manually. 

  * You cannot have specified a standby database as an archivelog destinations. As a result, the database cannot be in `MAXIMUM` `PROTECTION` or `MAXIMUM` `AVAILABILITY` standby protection mode. 

If you omit this clause, then Oracle Database automatically archives the redo
log files to the destination specified in the `LOG_ARCHIVE_DEST_``n`
initialization parameters.

NOARCHIVELOG

Specify `NOARCHIVELOG` if you do not want the contents of a redo log file
group to be archived so that the group can be reused. This mode does not
prepare for recovery after media failure. Use this clause only if your
instance has the database mounted but not open.

[NO] FORCE LOGGING

Use this clause to put the database into or take the database out of `FORCE`
`LOGGING` mode. The database must be mounted or open.

In `FORCE` `LOGGING` mode, Oracle Database logs all changes in the database
except changes in temporary tablespaces and temporary segments. This setting
takes precedence over and is independent of any `NOLOGGING` or `FORCE`
`LOGGING` settings you specify for individual tablespaces and any `NOLOGGING`
settings you specify for individual database objects.

If you specify `FORCE` `LOGGING`, then Oracle Database waits for all ongoing
unlogged operations to finish.

See Also:

[Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN002) for information on when to use `FORCE`
`LOGGING` mode

SET STANDBY NOLOGGING

Standby nologging instructs the database to not log operations that qualify to
be done without logging. The database sends the data blocks created by the
operation to each qualifying standby database in the Data Guard configuration,
to prevent missed data on the standby and keep it in sync with the primary.

Use this clause to determine how nonlogged tasks are handled . You can choose
one of two logging modes for a database when you create the database, and you
can change the logging mode of a database from one mode to the other.

  * `SET STANDBY NOLOGGING FOR LOAD PERFORMANCE` to put the database into standby nologging for load performance mode. In this mode, the data loaded as part of the nonlogged task is sent to the qualifying standbys via a private network connection, provided that doing so will not slow down the load process. If the load process slows, then the data is not sent but automatically fetched from the primary as each standby encounters the invalidation redo and will be retried until the data blocks are eventually received. 

  * Specify `SET STANDBY NOLOGGING FOR DATA AVAILABILITY` to put the database into standby nologging for data availability mode. In this mode the data loaded as part of the nonlogged task is sent to the qualifying standbys either via a network connection or via block images in the redo, in case the network connection fails. That is to say, in this mode the load will switch to be done in a logged fashion if the network connection or related processes prevent the sending of the data over the private network connection. 

For the standby nologging modes, a qualifying standby is one that is open for
read, running managed recovery and receiving redo into standby redo logs.

Restrictions on Setting Standby Nologging

The`SET STANDBY NOLOGGING` clause cannot be used at the same time as `FORCE
LOGGING`.

RENAME FILE Clause

This clause has the same function for logfiles that it has for data files and
temp files. See "[RENAME FILE Clause](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2162839)".

CLEAR LOGFILE Clause

Use the `CLEAR` `LOGFILE` clause to reinitialize an online redo log,
optionally without archiving the redo log. `CLEAR` `LOGFILE` is similar to
adding and dropping a redo log, except that the statement may be issued even
if there are only two logs for the thread and may be issued for the current
redo log of a closed thread.

For a standby database, if the `STANDBY_FILE_MANAGEMENT` initialization
parameter is set to `AUTO`, and if any of the log files are Oracle Managed
Files, Oracle Database will create as many Oracle-managed log files as are in
the control file. The log file members will reside in the current default log
file destination.

  * You must specify `UNARCHIVED` if you want to reuse a redo log that was not archived. 

Note:

Specifying `UNARCHIVED` makes backups unusable if the redo log is needed for
recovery.

  * You must specify `UNRECOVERABLE` `DATAFILE` if you have taken the data file offline with the database in `ARCHIVELOG` mode (that is, you specified `ALTER` `DATABASE` ... `DATAFILE` `OFFLINE` without the `DROP` keyword), and if the unarchived log to be cleared is needed to recover the data file before bringing it back online. In this case, you must drop the data file and the entire tablespace once the `CLEAR` `LOGFILE` statement completes. 

Do not use `CLEAR` `LOGFILE` to clear a log needed for media recovery. If it
is necessary to clear a log containing redo after the database checkpoint,
then you must first perform incomplete media recovery. The current redo log of
an open thread can be cleared. The current log of a closed thread can be
cleared by switching logs in the closed thread.

If the `CLEAR` `LOGFILE` statement is interrupted by a system or instance
failure, then the database may hang. In this case, reissue the statement after
the database is restarted. If the failure occurred because of I/O errors
accessing one member of a log group, then that member can be dropped and other
members added.

See Also:

"[Clearing a Log File: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135897)"

add_logfile_clauses

Use these clauses to add redo log file groups to the database and to add new
members to existing redo log file groups.

ADD LOGFILE Clause

Use the `ADD` `LOGFILE` clause to add one or more redo log file groups to the
online redo log or standby redo log.

See Also:

  * "[LOGFILE Clause](CREATE-DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__I2160227)" of `CREATE` `DATABASE` for information on the result of this clause for Oracle Managed Files if you do not specify a name for the new log file group 

  * "[Adding Redo Log File Groups: Examples](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135589)"

  * [Oracle Data Guard Concepts and Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SBYDB4752) for more information on standby redo logs 

STANDBY

Use the `STANDBY` clause to add a redo log file group to the standby redo log.
If you do not specify this clause, then a log file group is added to the
online redo log.

INSTANCE

The `INSTANCE` clause is applicable only for Oracle Real Application Clusters
(Oracle RAC) or Oracle RAC One Node databases. Specify the name of the
instance for which you want to add a redo log file group. The instance name is
a string of up to 80 characters. Oracle Database automatically uses the thread
that is mapped to the specified instance. If no thread is mapped to the
specified instance, then Oracle Database automatically acquires an available
unmapped thread and assigns it to that instance. If you do not specify this
clause, then Oracle Database executes the command as if you had specified the
current instance. If the specified instance has no current thread mapping and
there are no available unmapped threads, then Oracle Database returns an
error.

THREAD

When adding a redo log file group to the standby redo log, use the `THREAD`
clause to assign the log file group to a specific primary database redo
thread. Query the `V$INSTANCE` view on the primary database to determine which
redo threads have been opened, and specify one of these thread numbers.

You can also use the `THREAD` clause to assign a log file group to a specific
redo thread when adding the log file group to the online redo log. This usage
has been deprecated. The `INSTANCE` clause achieves the same purpose and is
easier to use.

GROUP

The `GROUP` clause uniquely identifies the redo log file group among all
groups in all threads and can range from 1 to the value specified for
`MAXLOGFILES` in the `CREATE` `DATABASE` statement. You cannot add multiple
redo log file groups having the same `GROUP` value. If you omit this
parameter, then Oracle Database generates its value automatically. You can
examine the `GROUP` value for a redo log file group through the dynamic
performance view `V$LOG`.

redo_log_file_spec

Each `redo_log_file_spec` specifies a redo log file group containing one or
more members (copies). If you do not specify a filename for the new log file,
then Oracle Database creates Oracle Managed Files according to the rules
described in the "[LOGFILE Clause](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2160227)" of `CREATE` `DATABASE`.

See Also:

  * [file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN003) for information on dynamic performance views 

ADD LOGFILE MEMBER Clause

Use the `ADD` `LOGFILE` `MEMBER` clause to add new members to existing redo
log file groups. Each new member is specified by `'filename'`. If the file
already exists, then it must be the same size as the other group members and
you must specify `REUSE`. If the file does not exist, then Oracle Database
creates a file of the correct size. You cannot add a member to a group if all
of the members of the group have been lost through media failure.

STANDBY

You must specify `STANDBY` when adding a member to a standby redo log file
group. Otherwise, Oracle Database returns an error.

You can use the `logfile_descriptor` clause to specify an existing redo log
file group in one of two ways:

GROUP integer

Specify the value of the `GROUP` parameter that identifies the redo log file
group.

filename(s)

List all members of the redo log file group. You must fully specify each
filename according to the conventions of your operating system.

See Also:

  * "[LOGFILE Clause](CREATE-DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__I2160227)" of `CREATE` `DATABASE` for information on the result of this clause for Oracle Managed Files if you do not specify a name for the new log file group 

  * "[Adding Redo Log File Group Members: Example](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2188734)"

drop_logfile_clauses

Use these clauses to drop redo log file groups or redo log file members.

DROP LOGFILE Clause

Use the `DROP` `LOGFILE` clause to drop all members of a redo log file group.
If you use this clause to drop Oracle Managed Files, then Oracle Database also
removes all log file members from disk. Specify a redo log file group as
indicated for the `ADD` `LOGFILE` `MEMBER` clause.

  * To drop the current log file group, you must first issue an `ALTER` `SYSTEM` `SWITCH` `LOGFILE` statement. 

  * You cannot drop a redo log file group if it needs archiving.

  * You cannot drop a redo log file group if doing so would cause the redo thread to contain less than two redo log file groups.

See Also:

[ALTER SYSTEM](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB)
and "[Dropping Log File Members: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135628)"

DROP LOGFILE MEMBER Clause

Use the `DROP` `LOGFILE` `MEMBER` clause to drop one or more redo log file
members. Each `'filename'` must fully specify a member using the conventions
for filenames on your operating system.

  * To drop a log file in the current log, you must first issue an `ALTER` `SYSTEM` `SWITCH` `LOGFILE` statement. Refer to [ALTER SYSTEM](ALTER-SYSTEM.md#GUID-2C638517-D73A-41CA-9D8E-A62D1A0B7ADB) for more information. 

  * You cannot use this clause to drop all members of a redo log file group that contains valid data. To perform that operation, use the `DROP` `LOGFILE` clause. 

See Also:

"[Dropping Log File Members: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135628)"

switch_logfile_clause

This clause is useful when you are migrating the database to disks with a
different block size that the block size of the current database. Use this
clause to switch logfiles to a different block size for all externally enabled
threads, including both open and closed threads. If you are migrating the
database to use 4KB sector disks, then you must specify 4096 for `integer`. If
you are unmigrating the database back to using 512B sector disks, then you
must specify 512 for `integer`.

This clause is an extension of the existing `ALTER` `SYSTEM` `SWITCH`
`LOGFILE` statement. That statement switches logs for a single thread. This
clause switches logfiles for all externally enabled threads, including both
open and closed threads.

Before using this clause, you must already have created at least two redo log
groups with the same target block size on the migration target disk.

See Also:

[Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN12891) for more information on migrating the
database to disks with a different block size, and "[Adding a Log File:
Example](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1015789)"

supplemental_db_logging

Use these clauses to instruct Oracle Database to add or stop adding
supplemental data into the log stream.

ADD SUPPLEMENTAL LOG Clause

Specify `ADD` `SUPPLEMENTAL` `LOG` `DATA` to enable minimal supplemental
logging. Specify `ADD` `SUPPLEMENTAL` `LOG` `supplemental_id_key_clause` to
enable column data logging in addition to minimal supplemental logging.
Specify `ADD` `SUPPLEMENTAL` `LOG` `supplemental_plsql_clause` to enable
supplemental logging of PL/SQL calls. Oracle Database does not enable either
minimal supplemental logging or supplemental logging by default.

Minimal supplemental logging ensures that LogMiner (and any products building
on LogMiner technology) will have sufficient information to support chained
rows and various storage arrangements such as cluster tables.

If the redo generated on one database is to be the source of changes (to be
mined and applied) at another database, as is the case with logical standby,
then the affected rows need to be identified using column data (as opposed to
rowids). In this case, you should specify the `supplemental_id_key_clause`.

You can query the appropriate columns in the `V$DATABASE` view to determine
whether any supplemental logging has already been enabled.

You can use this clause when the database is open. However, Oracle Database
will invalidate all DML cursors in the cursor cache, which will have an effect
on performance until the cache is repopulated.

If you use this clause in a CDB, then the current container must be the root
and the operation will be performed on the entire CDB.

You can enable supplemental logging levels at PDB without minimal supplemental
logging enabled at `CDB$ROOT`. Dropping all supplemental logging from
`CDB$ROOT` will not disable supplemental logging enabled at the PDB level.

For a full discussion of the `supplemental_id_clause`, refer to
[supplemental_id_key_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2215249) in the
documentation on `CREATE` `TABLE`.

See Also:

  * [Oracle Data Guard Concepts and Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SBYDB00308) for information on supplemental logging on the primary database to support a logical standby database 

  * [Oracle Database Utilities](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SUTIL019) for examples using the `supplemental_db_logging` clause syntax 

DROP SUPPLEMENTAL LOG Clause

Use this clause to stop supplemental logging.

  * Specify `DROP` `SUPPLEMENTAL` `LOG` `DATA` to instruct Oracle Database to stop placing minimal additional log information into the redo log stream whenever an update operation occurs. If Oracle Database is doing column data supplemental logging specified with the `supplemental_id_key_clause`, then you must first stop the column data supplemental logging with the `DROP` `SUPPLEMENTAL` `LOG` `supplemental_id_key_clause` and then specify this clause. 

  * Specify `DROP` `SUPPLEMENTAL` `LOG` `supplemental_id_key_clause` to drop some or all of the system-generated supplemental log groups. You must specify the `supplemental_id_key_clause` if the supplemental log groups you want to drop were added using that clause. 

  * Specify `DROP` `SUPPLEMENTAL` `LOG` `supplemental_plsql_clause` disable supplemental logging of PL/SQL calls. 

If you use this clause in a CDB, then the current container must be the root
and the operation will be performed on the entire CDB.

ADD SUPPLEMENTAL LOG DATA SUBSET DATABASE REPLICATION of `ALTER DATABASE`
enables low impact minimal supplemental logging.

  * You can execute this DDL only when the `enable_goldengate_replication` parameter is TRUE, and database compatible is 19.0 or higher. 

  * This DDL implicitly adds DB-level minimal supplemental logging, similar to other DB-level supplemental logging DDLs.

  * In case of CDB, this DDL can be executed in both `CDB$ROOT` and pluggable databases. 

  * When executed in `CDB$ROOT`, it enables low impact minimal supplemental logging for entire database. Low impact minimal supplemental logging will be enabled for all the pluggable databases regardless of the PDB level setting for subset database replication. 

  * When executed in pluggable database, itâs same as `ALTER PLUGGABLE DATABASE ADD SUPPLEMENTAL LOG DATA SUBSET DATABASE REPLICATION`. See [ALTER PLUGGABLE DATABASE](ALTER-PLUGGABLE-DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7) for details. 

DROP SUPPLEMENTAL LOG DATA SUBSET DATABASE REPLICATION of `ALTER DATABASE`
disables low impact minimal supplemental logging.

  * You can execute this DDL only when the`enable_goldengate_replication` parameter is TRUE, and database compatible should be 19.0 or higher. 

  * You must have explicitly enabled other supplemental log data. This restriction ensures that disabling low impact minimal supplemental logging never disables minimal supplemental logging.

  * Once this DDL is executed, the minimal supplemental logging will go back to its current behavior.

  * In case of CDB, this DDL can be executed in both `CDB$ROOT` and pluggable databases. 

  * When executed in `CDB$ROOT` , it disables low impact minimal supplemental logging at the database level. For each pluggable database, whether low impact supplemental logging is enabled depends on the PDB-level setting for subset database replication. 

  * When executed in pluggable database, the behavior is the same as `ALTER PLUGGABLE DATABASE DROP SUPPLEMENTAL LOG DATA SUBSET DATABASE REPLICATION`. See [ALTER PLUGGABLE DATABASE](ALTER-PLUGGABLE-DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7) for details. 

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00308) for information on supplemental logging

controlfile_clauses

The `controlfile_clauses` let you create or back up a control file.

CREATE CONTROLFILE Clause

The `CREATE` `CONTROLFILE` clause lets you create a control file.

  * Specify `PHYSICAL` `STANDBY` to create a control file to be used to maintain a physical database. This is the default if you specify `STANDBY` and do not specify `PHYSICAL` or `LOGICAL`. 

  * Specify `LOGICAL` `STANDBY` to create a control file to be used to maintain a logical database. 

  * Specify `FAR` `SYNC` `INSTANCE` to create a control file to be used to maintain a Data Guard far sync instance. 

If the file already exists, then you must specify `REUSE`. In an Oracle RAC
environment, the control file must be on shared storage.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB4723) for more information on creating control files

BACKUP CONTROLFILE Clause

Use the `BACKUP` `CONTROLFILE` clause to back up the current control file. The
database must be open or mounted when you specify this clause.

TO 'filename'

Use this clause to specify a binary backup of the control file. You must fully
specify the `filename` using the conventions for your operating system. If the
specified file already exists, then you must specify `REUSE`. In an Oracle RAC
environment, `filename` must be on shared storage.

A binary backup contains information that is not captured if you specify `TO`
`TRACE`, such as the archived log history, offline range for read-only and
offline tablespaces, and backup sets and copies (if you use RMAN). If the
`COMPATIBLE` initialization parameter is `10`.`2` or higher, binary control
file backups include temp file entries.

TO TRACE

Specify `TO` `TRACE` if you want Oracle Database to write SQL statements to a
trace file rather than making a physical backup of the control file. You can
use SQL statements written to the trace file to start up the database, re-
create the control file, and recover and open the database appropriately,
based on the created control file. If you issue an `ALTER` `DATABASE` `BACKUP`
`CONTROLFILE` `TO` `TRACE` statement while block change tracking is enabled,
then the resulting trace file will contain a command to reenable block change
tracking.

This statement issues an implicit `ALTER` `DATABASE` `REGISTER` `LOGFILE`
statement, which creates incarnation records if the archived log files reside
in the current archivelog destinations.

The trace file will also include `ALTER` `DATABASE` `REGISTER` `LOGFILE`
statements for existing logfiles that reside in the current archivelog
destinations. This will implicitly create database incarnation records for the
branches of redo to which the logfiles apply.

You can copy the statements from the trace file into a script file, edit the
statements as necessary, and use the script if all copies of the control file
are lost (or to change the size of the control file).

  * Specify `AS` `filename` if you want Oracle Database to place the trace output into a file called `filename` rather than into the standard trace file. 

  * Specify `REUSE` to allow Oracle Database to overwrite any existing file called `filename`. 

  * `RESETLOGS` indicates that the SQL statement written to the trace file for starting the database is `ALTER` `DATABASE` `OPEN` `RESETLOGS`. This setting is valid only if the online logs are unavailable. 

  * `NORESETLOGS` indicates that the SQL statement written to the trace file for starting the database is `ALTER` `DATABASE` `OPEN` `NORESETLOGS`. This setting is valid only if all the online logs are available. 

If you cannot predict the future state of the online logs, then specify
neither `RESETLOGS` nor `NORESETLOGS`. In this case, Oracle Database puts both
versions of the script into the trace file, and you can choose which version
is appropriate when the script becomes necessary.

The trace files are stored in a subdirectory determined by the
`DIAGNOSTIC_DEST` initialization parameter. You can find the name and location
of the trace file to which the `CREATE` `CONTROLFILE` statements were written
by looking in the alert log. You can also find the directory for trace files
by querying the `NAME` and `VALUE` columns of the `V$DIAG_INFO` dynamic
performance view.

See Also:

[Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN11267) for information on viewing the alert log

standby_database_clauses

Use these clauses to activate the standby database or to specify whether it is
in protected or unprotected mode.

See Also:

Oracle Data Guard Concepts and Administration for descriptions of the
[physical](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00200) and
[logical](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00300) standby database and for information on
maintaining and using standby databases

activate_standby_db_clause

Use the `ACTIVATE` `STANDBY` `DATABASE` clause to convert a standby database
into a primary database.

Note:

Before using this command, refer to [Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00600) for important usage information.

PHYSICAL

Specify `PHYSICAL` to activate a physical standby database. This is the
default.

LOGICAL

Specify `LOGICAL` to activate a logical standby database. If you have more
than one logical standby database, then you should first ensure that the same
log data is available on all the standby systems.

FINISH APPLY

This clause applies only to logical standby databases. Use it to initiate
terminal apply, which is the application of any remaining redo to bring the
logical standby database to the same state as the primary database. When
terminal apply is complete, the database completes the switchover from logical
standby to primary database.

If you require immediate restoration of the database in spite of data loss,
then omit this clause. The database will execute the switchover from logical
standby to primary database immediately without terminal apply.

maximize_standby_db_clause

Use this clause to specify the level of protection for the data in your
database environment. You specify this clause from the primary database.

Note:

The `PROTECTED` and `UNPROTECTED` keywords have been replaced for clarity but
are still supported. `PROTECTED` is equivalent to `TO` `MAXIMIZE`
`PROTECTION`. `UNPROTECTED` is equivalent to `TO` `MAXIMIZE` `PERFORMANCE`.

TO MAXIMIZE PROTECTION

This setting establishes maximum protection mode and offers the highest level
of data protection. A transaction does not commit until all data needed to
recover that transaction has been written to at least one physical standby
database that is configured to use the `SYNC` log transport mode. If the
primary database is unable to write the redo records to at least one such
standby database, then the primary database is shut down. This mode guarantees
zero data loss, but it has the greatest potential impact on the performance
and availability of the primary database.

Restriction on Establishing Maximum Protection Mode

You can specify `TO` `MAXIMIZE` `PROTECTION` on an open database only if the
current data protection mode is `MAXIMUM` `AVAILABILITY` and there is at least
one synchronized standby database.

TO MAXIMIZE AVAILABILITY

This setting establishes maximum availability mode and offers the next highest
level of data protection. A transaction does not commit until all data needed
to recover that transaction has been written to at least one physical or
logical standby database that is configured to use the `SYNC` log transport
mode. Unlike maximum protection mode, the primary database does not shut down
if it is unable to write the redo records to at least one such standby
database. Instead, the protection is lowered to maximum performance mode until
the fault has been corrected and the standby database has caught up with the
primary database. This mode guarantees zero data loss unless the primary
database fails while in maximum performance mode. Maximum availability mode
provides the highest level of data protection that is possible without
affecting the availability of the primary database.

TO MAXIMIZE PERFORMANCE

This setting establishes maximum performance mode and is the default setting.
A transaction commits before the data needed to recover that transaction has
been written to a standby database. Therefore, some transactions may be lost
if the primary database fails and you are unable to recover the redo records
from the primary database. This mode provides the highest level of data
protection that is possible without affecting the performance of the primary
database.

To determine the current mode of the database, query the `PROTECTION_MODE`
column of the `V$DATABASE` dynamic performance view.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00710) for full information on using these standby
database settings

register_logfile_clause

Specify the `REGISTER` `LOGFILE` clause from the standby database to manually
register log files from the failed primary. Use the `redo_log_file_spec` form
of `file_specification` (see
[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688))
to list regular redo log files in an operating system file system or to list
Oracle ASM disk group redo log files.

When a log file is from an unknown incarnation, the `REGISTER` `LOGFILE`
clause causes an incarnation record to be added to the
`V$DATABASE_INCARNATION` view. If the newly registered log file belongs to an
incarnation having a higher `RESETLOGS_TIME` than the current
`RECOVERY_TARGET_INCARNATION#`, then the `REGISTER` `LOGFILE` clause also
causes `RECOVERY_TARGET_INCARNATION#` to be changed to correspond to the newly
added incarnation record.

OR REPLACE

Specify `OR` `REPLACE` to allow an existing archivelog entry in the standby
database to be updated, for example, when its location or file specification
changes. The system change numbers of the entries must match exactly, and the
original entry must have been created by the managed standby log transmittal
mechanism.

FOR logminer_session_name

This clause is useful in a Streams environment. It lets you register the log
file with one specified LogMiner session.

switchover_clause

Caution:

Before using this command, refer to [Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB5170) for complete usage information.

Use this clause to perform a switchover to a physical standby database.
Specify this clause from the primary database. For `target_db_name`, specify
the `DB_UNIQUE_NAME` of the standby database.

VERIFY

Use this clause to verify that a physical standby database is ready for a
switchover. Specify this clause from the primary database. For
`target_db_name`, specify the `DB_UNIQUE_NAME` of the standby database. If the
standby database is ready for a switchover, then the "Database Altered"
message is returned. Otherwise, an error message that will assist you in
preparing the standby database for a switchover is returned.

FORCE

Use this clause if a previous switchover command failed and created a
configuration with no primary database. Specify this clause from the physical
standby database that you want to convert to the primary database. For
`target_db_name`, specify the `DB_UNIQUE_NAME` of the database that you want
to convert to the primary database.

failover_clause

Caution:

Before using this command, refer to [Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB5171) for complete usage information.

Use this clause to perform a failover to a physical standby database. Specify
this clause from the standby database. For `target_db_name`, specify the
`DB_UNIQUE_NAME` of the standby database.

FORCE

This clause has meaning only when the failover target is serviced by a Data
Guard far sync instance. Use this clause when a previous failover command
failed and the reason for the failure cannot be resolved. It instructs the
failover to ignore any failures encountered when interacting with the Data
Guard far sync instance and proceed with the failover, if at all possible.

commit_switchover_clause

Use this clause to perform database role transitions in a Data Guard
configuration.

Caution:

Before using this command, refer to [Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00600) for complete usage information.

PREPARE TO SWITCHOVER

This clause prepares a primary database to become a logical standby database
or a logical standby database to become a primary database.

  * Specify `PREPARE` `TO` `SWITCHOVER` `TO` `LOGICAL` `STANDBY` on a primary database. 

  * Specify `PREPARE` `TO` `SWITCHOVER` `TO` `PRIMARY` `DATABASE` on a logical standby database. 

COMMIT TO SWITCHOVER

This clause switches a primary database to a standby database role or switches
a standby database to the primary database role.

  * Specify `COMMIT` `TO` `SWITCHOVER` `TO` `PHYSICAL` `STANDBY` or `COMMIT` `TO` `SWITCHOVER` `TO` `LOGICAL` `STANDBY` on a primary database. 

  * Specify `COMMIT` `TO` `SWITCHOVER` `TO` `PRIMARY` `DATABASE` on a standby database. 

PHYSICAL

This clause is always optional. Use of this clause with the `COMMIT` `TO`
`SWITCHOVER` `TO` `PRIMARY` clause has been deprecated.

LOGICAL

This clause is specified with the `PREPARE` `TO` `SWITCHOVER` or `COMMIT` `TO`
`SWITCHOVER` clauses when switching a primary database to the logical standby
database role. Use of this clause with the `COMMIT` `TO` `SWITCHOVER` `TO`
`PRIMARY` clause has been deprecated.

WITH SESSION SHUTDOWN

This clause causes all database sessions to be closed and uncommitted
transactions to be rolled back before performing a database role transition.

WITHOUT SESSION SHUTDOWN

This clause prevents a requested role transition from occurring if there are
any database sessions. This is the default.

WAIT

Specify this clause to wait for a role transition to complete before returning
control to the user.

NOWAIT

Specify this clause to return control to the user without waiting for a role
transition to complete. This is the default.

CANCEL

Specify this clause to reverse the effect of a previously specified `PREPARE`
`TO` `SWITCHOVER` statement.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00605) for full information on switchover between
primary and standby databases

start_standby_clause

Specify the `START` `LOGICAL` `STANDBY` `APPLY` clause to begin applying redo
logs to a logical standby database. This clause enables primary key, unique
index, and unique constraint supplemental logging as well as PL/SQL call
logging.

  * Specify `IMMEDIATE` to apply redo data from the current standby redo log file. 

  * Specify `NODELAY` if you want Oracle Database to ignore a delay for this apply. This is useful if the primary database is no longer present, which would otherwise require a PL/SQL call to be made. 

  * Specify `INITIAL` the first time you apply the logs to the standby database. 

  * The `NEW` `PRIMARY` clause is needed in two situations: 

    * On a failover to a logical standby, specify this clause on a logical standby not participating in the failover operation, and on the old primary database after it has been reinstated as a logical standby database. 

    * During a rolling upgrade using a logical standby database (which uses an unprepared switchover operation), specify this clause after the original primary database has been upgraded to the new database software.

  * Specify `SKIP` `FAILED` [`TRANSACTION`] to skip the last transaction in the events table and restart the apply. 

  * Specify `FINISH` to force the standby redo logfile information into archived logs. If the primary database becomes disabled, then you can then apply the data in the redo log files. 

stop_standby_clause

Use this clause to stop the log apply services. This clause applies only to
logical standby databases, not to physical standby databases. Use the `STOP`
clause to stop the apply in an orderly fashion.

convert_database_clause

Use this clause to convert a database from one form to another.

  * Specify `CONVERT` `TO` `PHYSICAL` `STANDBY` to convert a primary database, a logical standby database, or a snapshot standby database into a physical standby database. 

Perform these steps before specifying this clause:

    * On an Oracle Real Application Clusters (Oracle RAC) database, shut down all but one instance.

    * Ensure that the database is mounted, but not open.

The database is dismounted after conversion and must be restarted.

  * Specify `CONVERT` `TO` `SNAPSHOT` `STANDBY` to convert a physical standby database into a snapshot standby database. 

Ensure that redo apply is stopped before specifying this clause.

Note:

A snapshot standby database must be opened at least once in read/write mode
before it can be converted into a physical standby database.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00708) for more information about standby databases

default_settings_clauses

Use these clauses to modify the default settings of the database.

DEFAULT EDITION Clause

Use this clause to designate the specified edition as the default edition for
the database. The specified edition must already have been created and must be
`USABLE`. The change takes place immediately and is visible to all nodes in an
Oracle RAC environment. New database sessions automatically start out in the
specified edition. The new setting persists across database shutdown and
startup.

When you designate an edition as the database default edition, all users can
use the edition, as though the `USE` object privilege were granted on the
specified edition to the role `PUBLIC`.

You can determine the current default edition of the database with the
following query:

    
    
    SELECT PROPERTY_VALUE FROM DATABASE_PROPERTIES 
      WHERE PROPERTY_NAME = 'DEFAULT_EDITION';

See Also:

[CREATE EDITION](CREATE-
EDITION.md#GUID-6CF92CA1-CAF7-4967-9B34-C02D72C23617) for more information
on editions and [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS99919) for information on how editions are
designated as `USABLE`

CHARACTER SET, NATIONAL CHARACTER SET

You can no longer change the database character set or the national character
set using the `ALTER` `DATABASE` statement. Refer to [Oracle Database
Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG011) for information on database character set
migration.

SET DEFAULT TABLESPACE Clause

Use this clause to specify or change the default type of subsequently created
tablespaces. Specify `BIGFILE` or `SMALLFILE` to indicate whether the
tablespaces should be bigfile or smallfile tablespaces.

  * A bigfile tablespace contains only one data file or temp file, which can contain up to approximately 4 billion (232) blocks. The maximum size of the single data file or temp file is 128 terabytes (TB) for a tablespace with 32K blocks and 32TB for a tablespace with 8K blocks. 

  * A smallfile tablespace is a traditional Oracle tablespace, which can contain 1022 data files or temp files, each of which can contain up to approximately 4 million (222) blocks. 

See Also:

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN01102) for more information about bigfile tablespaces 

  * "[Setting the Default Type of Tablespaces: Example](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2187081)"

DEFAULT TABLESPACE Clause

Specify this clause to establish or change the default permanent tablespace of
the database. The tablespace you specify must already have been created. After
this operation completes, Oracle Database automatically reassigns to the new
default tablespace all non-`SYSTEM` users. All objects subsequently created by
those users will by default be stored in the new default tablespace. If you
are replacing a previously specified default tablespace, then you can move the
previously created objects from the old to the new default tablespace, and
then drop the old default tablespace if you want to.

DEFAULT [LOCAL] TEMPORARY TABLESPACE Clause

Specify this clause to change the default shared temporary tablespace of the
database to a new tablespace or tablespace group, or to change the default
local temporary tablespace to a new tablespace.

  * Specify `tablespace` to indicate the new default temporary tablespace for the database. After this operation completes, Oracle Database automatically reassigns to the new default temporary tablespace all users who had been assigned to the old default temporary tablespace. You can then drop the old default temporary tablespace if you want to. Specify `DEFAULT` `TEMPORARY` `TABLESPACE` to change the default shared temporary tablespace. Specify `DEFAULT` `LOCAL` `TEMPORARY` `TABLESPACE` to change the default local temporary tablespace. 

  * Specify `tablespace_group_name` to indicate that all tablespaces in the tablespace group specified by `tablespace_group_name` are now default shared temporary tablespaces for the database. After this operation completes, users who have not been explicitly assigned a default temporary tablespace can create temporary segments in any of the tablespaces that are part of `tablespace_group_name`. You cannot drop an old default temporary tablespace if it is part of the default temporary tablespace group. Local temporary tablespaces cannot be part of a tablespace group. 

To learn the name of the current default temporary tablespace or default
temporary tablespace group, query the `TEMPORARY_TABLESPACE` column of the
`ALL_`, `DBA_`, or `USER_USERS` data dictionary views.

Restrictions on Default Temporary Tablespaces

Default temporary tablespaces are subject to the following restrictions:

  * The tablespace you assign or reassign as the default temporary tablespace must have a standard block size.

  * If the `SYSTEM` tablespace is locally managed, then the tablespace you specify as the default temporary tablespace must also be locally managed. 

See Also:

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN01103) for information on tablespace groups 

  * "[Changing the Default Temporary Tablespace: Examples](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2189294)"

instance_clauses

In an Oracle Real Application Clusters environment, specify `ENABLE`
`INSTANCE` to enable the thread that is mapped to the specified database
instance. The thread must have at least two redo log file groups, and the
database must be open.

Specify `DISABLE` `INSTANCE` to disable the thread that is mapped to the
specified database instance. The name of the instance is a string of up to 80
characters. If no thread is currently mapped to the specified instance, then
Oracle Database returns an error. The database must be open, but you cannot
disable a thread if an instance using it has the database mounted.

See Also:

[Oracle Real Application Clusters Administration and Deployment
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=RACAD5023) for more information on enabling and disabling
instances

RENAME GLOBAL_NAME Clause

Specify `RENAME` `GLOBAL_NAME` to change the global name of the database. The
database must be open. The `database` is the new database name and can be as
long as eight bytes. The optional `domain` specifies where the database is
effectively located in the network hierarchy. If you specify a domain name,
then the components of the domain name must be legal identifiers. See
"[Database Object Naming Rules](Database-Object-Names-and-
Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)" for information on
valid identifiers.

Note:

Renaming your database does not change global references to your database from
existing database links, synonyms, and stored procedures and functions on
remote databases. Changing such references is the responsibility of the
administrator of the remote databases.

See Also:

"[Changing the Global Database Name: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2135837)"

BLOCK CHANGE TRACKING Clauses

The block change tracking feature causes Oracle Database to keep track of the
physical locations of all database updates on both the primary database and
any physical standby database. You must enable block change tracking on each
database for which you want tracking to be performed. The tracking information
is maintained in a separate file called the block change tracking file. If you
are using Oracle Managed Files, then Oracle Database automatically creates the
block change tracking file in the location specified by `DB_CREATE_FILE_DEST`.
If you are not using Oracle Managed Files, then you must specify the change
tracking filename. Oracle Database uses change tracking data for some internal
tasks, such as increasing the performance of incremental backups. You can
enable or disable block change tracking with the database either open or
mounted, in either archivelog or `NOARCHIVELOG` mode.

ENABLE BLOCK CHANGE TRACKING

This clause enables block change tracking and causes Oracle Database to create
a block change tracking file.

  * Specify `USING` `FILE` '`filename`' if you want to name the block change tracking file instead of letting Oracle Database generate a name for it. You must specify this clause if you are not using Oracle Managed Files. 

  * Specify `REUSE` to allow Oracle Database to overwrite an existing block change tracking file of the same name. 

Note:

On a standby database, the block change tracking only becomes effective when
the managed recovery starts. If the recovery is already active on the standby
database when you issue the command, the recovery must be stopped and then
started again to benefit from the fast incremental backups.

DISABLE BLOCK CHANGE TRACKING

Specify this clause if you want Oracle Database to stop tracking changes and
delete the existing block change tracking file.

See Also:

[Oracle Database Backup and Recovery User's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV8125) for information on setting up block change
tracking and "[Enabling and Disabling Block Change Tracking: Examples](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2185699)"

[NO] FORCE FULL DATABASE CACHING

Use this clause to enable or disable the force full database caching mode. In
contrast to the default mode, which is automatic, the force full database
caching mode considers the entire database, including `NOCACHE` LOBs, as
eligible for caching in the buffer cache.

The database must be mounted but not open. In an Oracle RAC environment, the
database must be mounted but not open in the current instance and unmounted in
all other instances.

  * Specify `FORCE` `FULL` `DATABASE` `CACHING` to enable the force full database caching mode. 

  * Specify `NO` `FORCE` `FULL` `DATABASE` `CACHING` to disable the force full database caching mode. This is the default mode. 

You can determine whether the force full database caching mode is enabled by
querying the `FORCE_FULL_DB_CACHING` column of the `V$DATABASE` dynamic
performance view.

See Also:

  * [Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT94675) for more information on the force full database caching mode 

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN14235) to learn how to enable the force full database caching mode 

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN30047) for more information on the `V$DATABASE` dynamic performance view 

CONTAINERS DEFAULT TARGET

Use this clause to specify the default container for DML statements in a CDB.
You must be connect to the CDB root.

  * For `container_name`, specify the name of the default container. The default container can be any container in the CDB, including the CDB root, a PDB, an application root, or an application PDB. You can specify only one default container. 

  * If you specify `NONE`, then the default container is the CDB root. This is the default. 

When a DML statement is issued in a CDB root without specifying containers in
the `WHERE` clause, the DML statement affects the default container for the
CDB.

flashback_mode_clause

Use this clause to put the database in or take the database out of `FLASHBACK`
mode. You can specify this clause only if the database is in `ARCHIVELOG` mode
and you have already prepared a fast recovery area for the database. You can
specify this clause when the database is mounted or open. This clause cannot
be specified on a physical standby database if redo apply is active.

See Also:

[Oracle Database Backup and Recovery User's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV8183) for information on preparing the fast recovery
area for Flashback operations

FLASHBACK ON

Use this clause to put the database in `FLASHBACK` mode. When the database is
in `FLASHBACK` mode, Oracle Database automatically creates and manages
Flashback Database logs in the fast recovery area. Users with `SYSDBA` system
privilege can then issue a `FLASHBACK` `DATABASE` statement.

FLASHBACK OFF

Use this clause to take the database out of `FLASHBACK` mode. Oracle Database
stops logging Flashback data and deletes all existing Flashback Database logs.
Any attempt to issue a `FLASHBACK` `DATABASE` will fail with an error.

undo_mode_clause

This clause is valid only when you are connected to a CDB. It lets you change
the undo mode for the CDB. The CDB must be in `OPEN` `UPGRADE` mode.

  * Specify `LOCAL` `UNDO` `ON` to change the CDB to use local undo mode. 

  * Specify `LOCAL` `UNDO` `OFF` to change the CDB to use shared undo mode. 

See Also:

  * `CREATE` `DATABASE` [undo_mode_clause](CREATE-DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__UNDO_MODE_CLAUSE-53B363BB) for the full semantics of this clause 

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-24EA5811-94F0-4EEC-864F-23AEF48F2D51) for the complete steps for configuring a CDB to use local undo mode or shared undo mode 

set_time_zone_clause

This clause has the same semantics in `CREATE` `DATABASE` and `ALTER`
`DATABASE` statements. When used in with `ALTER` `DATABASE`, this clause
resets the time zone of the database. To determine the time zone of the
database, query the built-in function
[DBTIMEZONE](DBTIMEZONE.md#GUID-F2368F72-7065-462F-80B9-E115F5A48025). After
setting or changing the time zone with this clause, you must restart the
database for the new time zone to take effect.

Oracle Database normalizes all new `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE`
data to the time zone of the database when the data is stored on disk.Oracle
Database does not automatically update existing data in the database to the
new time zone. Therefore, you cannot reset the database time zone if there is
any `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE` data in the database. You must
first delete or export the `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE` data and
then reset the database time zone. For this reason, Oracle does not encourage
you to change the time zone of a database that contains data.

For a full description of this clause, refer to [set_time_zone_clause](CREATE-
DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__I2082011) in the
documentation on `CREATE` `DATABASE`.

security_clause

Use the `security_clause` (`GUARD`) to protect data in the database from being
changed. You can override this setting for a current session using the `ALTER`
`SESSION` `DISABLE` `GUARD` statement. Refer to [ALTER SESSION](ALTER-
SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B) for more information.

ALL

Specify `ALL` to prevent all users other than `SYS` from making any changes to
the database.

STANDBY

Specify `STANDBY` to prevent all users other than `SYS` from making changes to
any database object being maintained by logical standby. This setting is
useful if you want report operations to be able to modify data as long as it
is not being replicated by logical standby.

See Also:

[Oracle Data Guard Concepts and
Administration](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=SBYDB00300) for information on logical standby

NONE

Specify `NONE` if you want normal security for all data in the database.

Note:

Oracle strongly recommends that you not use this setting on a logical standby
database.

prepare_clause

  * Use this clause to prepare mirror copies of the database. You must provide a `mirror_name` to identify the filegroup that is created. The filegroup contains all the prepared files. 

  * Specify the number of copies to be prepared by the `REDUNDANCY` options: `EXTERNAL`, `NORMAL`, or `HIGH`. 

  * If you do not specify the redundancy of the mirror, the redundancy of the source database is used.

Prepare a Database : Example

    
    
    ALTER DATABASE db_name PREPARE MIRROR COPY mirror_name WITH HIGH REDUNDANCY

drop_mirror_copy

Use this clause to discard mirror copies of data created by the prepare
statement. You must specify the same mirror name that you used for the prepare
operation.

You cannot use this clause to drop a database that has already been split by
the `CREATE DATABASE `or `CREATE PLUGGABLE DATABASE` statement.

lost_write_protection

Specify this clause to enable lost write protection for data files. You can
enable, remove, and suspend lost write protection for data files.

Example: Turn on Lost Write for a Datafile

The example turns on lost write on datafile `td_file.df`.

    
    
     ALTER DATABASE DATAFILE td_file.df ENABLE LOST WRITE PROTECTION

Note that the lost write database is zeroed out. It is not initialized with
the contents of the current data file.

You can turn off lost write protection for a datafile in two ways, with the
`REMOVE` or `SUSPEND` options.

  1. The `REMOVE` option stops lost write protection for the data file. Additionally, it removes all references to lost write protection including tracking data from the shadow tablespace. 

Example: Remove Lost Write for a Datafile

    
         ALTER DATABASE DATAFILE td_file.df REMOVE LOST WRITE PROTECTION

  2. The `SUSPEND` option disables updates and lost write checking, but leaves the tracking data in the shadow tablespace. If you suspend lost write protection for a short time, lost write protection for the data file is stopped during the suspended period. This means that no lost write data is gathered, and no blocks are checked. If you turn on lost write protection for the data file later, there will be no records of SCN updates made to the blocks in the datafile during the suspended period. Note that the `SUSPEND` option does not deallocate the lost write storage. 

Example: Suspend Lost Write for a Datafile

    
         ALTER DATABASE DATAFILE td_file.df SUSPEND LOST WRITE PROTECTION

You can enable lost write protection for container databases and pluggable
databases.

Example: Turn on Lost Write for a Database

    
    
     ALTER DATABASE ENABLE LOST WRITE PROTECTION

Example: Turn off Lost Write for a Database

    
    
     ALTER DATABASE DISABLE LOST WRITE PROTECTION

Note that disabling lost write for the database does not deallocate the lost
write storage. You must use the `DROP TABLESPACE` statement to deallocate lost
write storage.

cdb_fleet_clauses

Specify the `cdb_fleet_clauses` to set a Lead CDB in a collection of different
CDBs.

lead_cdb_clause

Use this clause to designate a CDB as the Lead CDB in a CDB fleet. The
database property `LEAD_CDB` indicates that the current CDB is a Lead CDB, and
can be found in `DATABASE_PROPERTIES` view.

There is a new parameter in `SYS_CONTEXT` named `IS_LEAD_CDB` which can be
used to determine if the current session is connected to a Lead CDB in a CDB
fleet.

lead_cdb_uri_clause

Use this clause to specify the connection URI for the Lead CDB in a CDB fleet.
It is used to register a Member CDB with the Lead CDB of the fleet.

The database link name specified in `dblink` must exist in the CDB ROOT of the
Member CDB joining the CDB fleet. It is used to synchronize PDB metadata with
the Lead CDB in the fleet.

The `uri_string` specified is stored as a database property named
`LEAD_CDB_URI` and can be found in `DATABASE_PROPERTIES` view.

There is a new parameter in `SYS_CONTEXT` named `IS_LEAD_CDB` which can be
used to determine if the current session is connected to a Member CDB in a CDB
fleet.

property_clause

Specify this clause to set or remove database properties visible through
`DATABASE_PROPERTIES` or `CDB_PROPERTIES` views.

replay_upgrade_clause

Use this clause to enable or disable replay upgrade on the database.

If `UPGRADE` `SYNC` is `ON`, then replay upgrade and upgrade on open is
enabled.

Examples

READ ONLY / READ WRITE: Example

The following statement opens the database in read-only mode:

    
    
    ALTER DATABASE OPEN READ ONLY;
    

The following statement opens the database in read/write mode and clears the
online redo logs:

    
    
    ALTER DATABASE OPEN READ WRITE RESETLOGS;

Using Parallel Recovery Processes: Example

The following statement performs tablespace recovery using parallel recovery
processes:

    
    
    ALTER DATABASE
       RECOVER TABLESPACE tbs_03
       PARALLEL;

Adding Redo Log File Groups: Examples

The following statement adds a redo log file group with two members and
identifies it with a `GROUP` parameter value of 3:

    
    
    ALTER DATABASE
      ADD LOGFILE GROUP 3 
        ('diska:log3.log' ,  
         'diskb:log3.log') SIZE 50K; 
    

The following statement adds a redo log file group containing two members to
thread 5 (in a Real Application Clusters environment) and assigns it a `GROUP`
parameter value of 4:

    
    
    ALTER DATABASE  
        ADD LOGFILE THREAD 5 GROUP 4  
            ('diska:log4.log', 
             'diskb:log4:log'); 

Adding Redo Log File Group Members: Example

The following statement adds a member to the redo log file group added in the
previous example:

    
    
    ALTER DATABASE   
       ADD LOGFILE MEMBER 'diskc:log3.log'  
       TO GROUP 3; 

Dropping Log File Members: Example

The following statement drops one redo log file member added in the previous
example:

    
    
    ALTER DATABASE
        DROP LOGFILE MEMBER 'diskb:log3.log'; 
    

The following statement drops all members of the redo log file group 3:

    
    
    ALTER DATABASE DROP LOGFILE GROUP 3; 

Renaming a Log File Member: Example

The following statement renames a redo log file member:

    
    
    ALTER DATABASE   
        RENAME FILE 'diskc:log3.log' TO 'diskb:log3.log'; 
    

The preceding statement only changes the member of the redo log group from one
file to another. The statement does not actually change the name of the file
`diskc:log3.log` to `diskb:log3.log`. Before issuing this statement, you must
change the name of the file through your operating system.

Setting the Default Type of Tablespaces: Example

The following statement specifies that subsequently created tablespaces be
created as bigfile tablespaces by default:

    
    
    ALTER DATABASE
        SET DEFAULT BIGFILE TABLESPACE;

Changing the Default Temporary Tablespace: Examples

The following statement makes the `tbs_05` tablespace (created in "[Creating a
Temporary Tablespace: Example](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2204579)") the
default temporary tablespace of the database. This statement either
establishes a default temporary tablespace if none was specified at create
time, or replaces an existing default temporary tablespace with `tbs_05`:

    
    
    ALTER DATABASE 
       DEFAULT TEMPORARY TABLESPACE tbs_05;
    

Alternatively, a group of tablespaces can be defined as the default temporary
tablespace by using a tablespace group. The following statement makes the
tablespaces in the tablespace group `tbs_group_01` (created in "[Adding a
Temporary Tablespace to a Tablespace Group: Example](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2204334)") the
default temporary tablespaces of the database:

    
    
    ALTER DATABASE
       DEFAULT TEMPORARY TABLESPACE tbs_grp_01;

Creating a New Data File: Example

The following statement creates a new data file `tbs_f04.dbf` based on the
file `tbs_f03.dbf`. Before creating the new data file, you must take the
existing data file (or the tablespace in which it resides) offline.

    
    
    ALTER DATABASE 
        CREATE DATAFILE 'tbs_f03.dbf' 
                     AS 'tbs_f04.dbf'; 

Manipulating Temp Files: Example

The following takes offline the temp file temp02.dbf created in [Adding and
Dropping Data Files and Temp Files: Examples](ALTER-TABLESPACE.md#GUID-
CA074861-55D3-4768-8995-43D4DA26365D__I2133310) and then renames the temp
file:

    
    
    ALTER DATABASE TEMPFILE 'temp02.dbf' OFFLINE;
    
    ALTER DATABASE RENAME FILE 'temp02.dbf' TO 'temp03.dbf';
    

The statement renaming the temp file requires that you first create the file
`temp03.dbf` on the operating system.

Changing the Global Database Name: Example

The following statement changes the global name of the database and includes
both the database name and domain:

    
    
    ALTER DATABASE  
        RENAME GLOBAL_NAME TO demo.world.example.com; 

Enabling and Disabling Block Change Tracking: Examples

The following statement enables block change tracking and causes Oracle
Database to create a block change tracking file named `tracking_file` and
overwrite the file if it already exists:

    
    
    ALTER DATABASE
      ENABLE BLOCK CHANGE TRACKING
        USING FILE 'tracking_file' REUSE;
    

The following statement disables block change tracking and deletes the
existing block change tracking file:

    
    
    ALTER DATABASE
      DISABLE BLOCK CHANGE TRACKING;

Resizing a Data File: Example

The following statement attempts to change the size of data file
`diskb:tbs_f5.dbf`:

    
    
    ALTER DATABASE  
        DATAFILE 'diskb:tbs_f5.dbf' RESIZE 10 M;

Clearing a Log File: Example

The following statement clears a log file:

    
    
    ALTER DATABASE  
        CLEAR LOGFILE 'diskc:log3.log';

Database Recovery: Examples

The following statement performs complete recovery of the entire database,
letting Oracle Database generate the name of the next archived redo log file
needed:

    
    
    ALTER DATABASE 
      RECOVER AUTOMATIC DATABASE; 
    

The following statement explicitly names a redo log file for Oracle Database
to apply:

    
    
    ALTER DATABASE 
        RECOVER LOGFILE 'diskc:log3.log'; 
    

The following statement performs time-based recovery of the database:

    
    
    ALTER DATABASE 
        RECOVER AUTOMATIC UNTIL TIME '2001-10-27:14:00:00'; 
    

Oracle Database recovers the database until 2:00 p.m. on October 27, 2001.

For an example of recovering a tablespace, see "[Using Parallel Recovery
Processes: Example](ALTER-
DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2104508)".


[← Previous](ALTER-CLUSTER.md)

[Next →](ALTER-DATABASE-DICTIONARY.md)
