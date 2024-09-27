[Previous](CREATE-CONTEXT.md) [Next](CREATE-DATABASE.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE CONTROLFILE 

## CREATE CONTROLFILE

Note:

Oracle recommends that you perform a full backup of all files in the database
before using this statement. For more information, see [Oracle Database Backup
and Recovery User's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV8206).

Purpose

The `CREATE` `CONTROLFILE` statement should be used in only a few cases. Use
this statement to re-create a control file if all control files being used by
the database are lost and no backup control file exists. You can also use this
statement to change the maximum number of redo log file groups, redo log file
members, archived redo log files, data files, or instances that can
concurrently have the database mounted and open.

To change the name of the database, Oracle recommends that you use the
`DBNEWID` utility rather than the `CREATE` `CONTROLFILE` statement. `DBNEWID`
is preferable because no `OPEN` `RESETLOGS` operation is required after
changing the database name.

See Also:

  * [Oracle Database Utilities](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=SUTIL014) for more information about the `DBNEWID` utility 

  * `ALTER` `DATABASE` "[BACKUP CONTROLFILE Clause](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2089277)" for information creating a script based on an existing database control file 

Prerequisites

To create a control file, you must have the `SYSDBA` or `SYSBACKUP` system
privilege.

The database must not be mounted by any instance. After successfully creating
the control file, Oracle mounts the database in the mode specified by the
`CLUSTER_DATABASE` parameter. The DBA must then perform media recovery before
opening the database. If you are using the database with Oracle Real
Application Clusters (Oracle RAC), then you must then shut down and remount
the database in `SHARED` mode (by setting the value of the `CLUSTER_DATABASE`
initialization parameter to `TRUE`) before other instances can start up.

Syntax

create_controlfile::=

![Description of create_controlfile.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_controlfile.gif)  
[Description of the illustration
create_controlfile.eps](img_text/create_controlfile.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB))

logfile_clause::=

![Description of logfile_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logfile_clause.gif)  
[Description of the illustration
logfile_clause.eps](img_text/logfile_clause.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF))

character_set_clause::=

![Description of character_set_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/character_set_clause.gif)  
[Description of the illustration
character_set_clause.eps](img_text/character_set_clause.md)

Semantics

When you issue a `CREATE` `CONTROLFILE` statement, Oracle Database creates a
new control file based on the information you specify in the statement. The
control file resides in the location specified in the `CONTROL_FILES`
initialization parameter. If that parameter does not have a value, then the
database creates an Oracle-managed control file in the default control file
destination, which is one of the following (in order of precedence):

  1. One or more control files as specified in the `DB_CREATE_ONLINE_LOG_DEST_``n` initialization parameter. The file in the first directory is the primary control file. When `DB_CREATE_ONLINE_LOG_DEST_``n` is specified, the database does not create a control file in `DB_CREATE_FILE_DEST` or in `DB_RECOVERY_FILE_DEST` (the fast recovery area). 

  2. If no value is specified for `DB_CREATE_ONLINE_LOG_DEST_``n`, but values are set for both the `DB_CREATE_FILE_DEST` and `DB_RECOVERY_FILE_DEST`, then the database creates one control file in each location. The location specified in `DB_CREATE_FILE_DEST` is the primary control file. 

  3. If a value is specified only for `DB_CREATE_FILE_DEST`, then the database creates one control file in that location. 

  4. If a value is specified only for `DB_RECOVERY_FILE_DEST`, then the database creates one control file in that location. 

If no values are set for any of these parameters, then the database creates a
control file in the default location for the operating system on which the
database is running. This control file is not an Oracle Managed File.

If you omit any clauses, then Oracle Database uses the default values rather
than the values for the previous control file. After successfully creating the
control file, Oracle Database mounts the database in the mode specified by the
initialization parameter `CLUSTER_DATABASE`. If that parameter is not set,
then the default value is `FALSE`, and the database is mounted in `EXCLUSIVE`
mode. Oracle recommends that you then shut down the instance and take a full
backup of all files in the database.

See Also:

[Oracle Database Backup and Recovery User's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV8001)

REUSE

Specify `REUSE` to indicate that existing control files identified by the
initialization parameter `CONTROL_FILES` can be reused, overwriting any
information they may currently contain. If you omit this clause and any of
these control files already exists, then Oracle Database returns an error.

DATABASE Clause

Specify the name of the database. The value of this parameter must be the
existing database name established by the previous `CREATE` `DATABASE`
statement or `CREATE` `CONTROLFILE` statement.

SET DATABASE Clause

Use `SET` `DATABASE` to change the name of the database. The name of a
database can be as long as eight bytes.

When you specify this clause, you must also specify `RESETLOGS`. If you want
to rename the database and retain your existing log files, then after issuing
this `CREATE` `CONTROLFILE` statement you must complete a full database
recovery using an `ALTER` `DATABASE` `RECOVER` `USING` `BACKUP` `CONTROLFILE`
statement.

logfile_clause

Use the `logfile_clause` to specify the redo log files for your database. You
must list all members of all redo log file groups.

Use the `redo_log_file_spec` form of `file_specification` (see
[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688))
to list regular redo log files in an operating system file system or to list
Oracle ASM disk group redo log files. When using a form of `ASM_filename`, you
cannot specify the `autoextend_clause` of the `redo_log_file_spec`.

If you specify `RESETLOGS` in this clause, then you must use one of the file
creation forms of `ASM_filename`. If you specify `NORESETLOGS`, then you must
specify one of the reference forms of `ASM_filename`.

See Also:

[ASM_filename](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1026664)
for information on the different forms of syntax and [Oracle Automatic Storage
Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG036) for general information about using Oracle ASM

GROUP integer

Specify the logfile group number. If you specify `GROUP` values, then Oracle
Database verifies these values with the `GROUP` values when the database was
last open.

If you omit this clause, then the database creates logfiles using system
default values. In addition, if either the `DB_CREATE_ONLINE_LOG_DEST_``n` or
`DB_CREATE_FILE_DEST` initialization parameter has been set, and if you have
specified `RESETLOGS`, then the database creates two logs in the default
logfile destination specified in the `DB_CREATE_ONLINE_LOG_DEST_`n parameter,
and if it is not set, then in the `DB_CREATE_FILE_DEST` parameter.

See Also:

[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)
for a full description of this clause

RESETLOGS

Specify `RESETLOGS` if you want Oracle Database to ignore the contents of the
files listed in the `LOGFILE` clause. These files do not have to exist. You
must specify this clause if you have specified the `SET` `DATABASE` clause.

Each `redo_log_file_spec` in the `LOGFILE` clause must specify the `SIZE`
parameter. The database assigns all online redo log file groups to thread 1
and enables this thread for public use by any instance. After using this
clause, you must open the database using the `RESETLOGS` clause of the `ALTER`
`DATABASE` statement.

NORESETLOGS

Specify `NORESETLOGS` if you want Oracle Database to use all files in the
`LOGFILE` clause as they were when the database was last open. These files
must exist and must be the current online redo log files rather than restored
backups. The database reassigns the redo log file groups to the threads to
which they were previously assigned and reenables the threads as they were
previously enabled.

You cannot specify `NORESETLOGS` if you have specified the `SET` `DATABASE`
clause to change the name of the database. Refer to "[SET DATABASE
Clause](CREATE-
CONTROLFILE.md#GUID-9B389F28-C4D0-405D-BFE6-48237E8BD791__BABBCFCI)" for
more information.

DATAFILE Clause

Specify the data files of the database. You must list all data files. These
files must all exist, although they may be restored backups that require media
recovery.

Do not include in the `DATAFILE` clause any data files in read-only
tablespaces. You can add these types of files to the database later. Also, do
not include in this clause any temporary data files (temp files).

Use the `datafile_tempfile_spec` form of `file_specification` (see
[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688))
to list regular data files and temp files in an operating system file system
or to list Oracle ASM disk group files. When using a form of `ASM_filename`,
you must use one of the reference forms of `ASM_filename`. Refer to
[ASM_filename](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1026664)
for information on the different forms of syntax.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG036) for general information about using Oracle ASM

Restriction on DATAFILE

You cannot specify the `autoextend_clause` of `file_specification` in this
`DATAFILE` clause.

MAXLOGFILES Clause

Specify the maximum number of online redo log file groups that can ever be
created for the database. Oracle Database uses this value to determine how
much space to allocate in the control file for the names of redo log files.
The default and maximum values depend on your operating system. The value that
you specify should not be less than the greatest `GROUP` value for any redo
log file group.

MAXLOGMEMBERS Clause

Specify the maximum number of members, or identical copies, for a redo log
file group. Oracle Database uses this value to determine how much space to
allocate in the control file for the names of redo log files. The minimum
value is 1. The maximum and default values depend on your operating system.

MAXLOGHISTORY Clause

This parameter is useful only if you are using Oracle Database in `ARCHIVELOG`
mode. Specify your current estimate of the maximum number of archived redo log
file groups needed for automatic media recovery of the database. The database
uses this value to determine how much space to allocate in the control file
for the names of archived redo log files.

The minimum value is 0. The default value is a multiple of the `MAXINSTANCES`
value and depends on your operating system. The maximum value is limited only
by the maximum size of the control file. The database will continue to add
additional space to the appropriate section of the control file as needed, so
that you do not need to re-create the control file if your your original
configuration is no longer adequate. As a result, the actual value of this
parameter can eventually exceed the value you specify.

MAXDATAFILES Clause

Specify the initial sizing of the data files section of the control file at
`CREATE` `DATABASE` or `CREATE` `CONTROLFILE` time. An attempt to add a file
whose number is greater than `MAXDATAFILES`, but less than or equal to
`DB_FILES`, causes the control file to expand automatically so that the data
files section can accommodate more files.

The number of data files accessible to your instance is also limited by the
initialization parameter `DB_FILES`.

MAXINSTANCES Clause

Specify the maximum number of instances that can simultaneously have the
database mounted and open. This value takes precedence over the value of the
initialization parameter `INSTANCES`. The minimum value is 1. The maximum and
default values depend on your operating system.

ARCHIVELOG | NOARCHIVELOG

Specify `ARCHIVELOG` to archive the contents of redo log files before reusing
them. This clause prepares for the possibility of media recovery as well as
instance or system failure recovery.

If you omit both the `ARCHIVELOG` clause and `NOARCHIVELOG` clause, then
Oracle Database chooses `NOARCHIVELOG` mode by default. After creating the
control file, you can change between `ARCHIVELOG` mode and `NOARCHIVELOG` mode
with the `ALTER` `DATABASE` statement.

FORCE LOGGING

Use this clause to put the database into `FORCE` `LOGGING` mode after control
file creation. When the database is in this mode, Oracle Database logs all
changes in the database except changes to temporary tablespaces and temporary
segments. This setting takes precedence over and is independent of any
`NOLOGGING` or `FORCE` `LOGGING` settings you specify for individual
tablespaces and any `NOLOGGING` settings you specify for individual database
objects. If you omit this clause, then the database will not be in `FORCE`
`LOGGING` mode after the control file is created.

Note:

`FORCE` `LOGGING` mode can have performance effects. Refer to [Oracle Database
Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN011) for information on when to use this setting.

SET STANDBY NOLOGGING FOR DATA AVAILABILITY | LOAD PERFORMANCE

SET STANDBY NOLOGGING

The `SET STANDBY NOLOGGING` disables logging on the standby. You can specify
it in two modes:

  * SET STANDBY NOLOGGING FOR DATA AVAILABILITY  guarantees full data replication to the standby database. The primary and standby databases are synchronized during the load. In cases of network congestion the primary database will throttle its load. 

  * SET STANDBY NOLOGGING FOR LOAD PERFORMANCE to maintain speed of primary database load and synchronize with the standby later. 

Restrictions On SET STANDBY NOLOGGING

The `SET STANDBY NOLOGGING` clause cannot be used at the same time as `FORCE
LOGGING`.

character_set_clause

If you specify a character set, then Oracle Database reconstructs character
set information in the control file. If media recovery of the database is
subsequently required, then this information will be available before the
database is open, so that tablespace names can be correctly interpreted during
recovery. This clause is required only if you are using a character set other
than the default, which depends on your operating system. Oracle Database
prints the current database character set to the alert log in
`$ORACLE_HOME/log` during startup.

If you are re-creating your control file and you are using Recovery Manager
for tablespace recovery, and if you specify a different character set from the
one stored in the data dictionary, then tablespace recovery will not succeed.
However, at database open, the control file character set will be updated with
the correct character set from the data dictionary.

You cannot modify the character set of the database with this clause.

See Also:

[Oracle Database Backup and Recovery User's Guide
](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=BRADV009)for more information on tablespace recovery

Examples

Creating a Controlfile: Example

This statement re-creates a control file. In this statement, database `demo`
was created with the WE8DEC character set. The example uses the word `path`
where you would normally insert the path on your system to the appropriate
Oracle Database directories.

    
    
    STARTUP NOMOUNT
    
    CREATE CONTROLFILE REUSE DATABASE "demo" NORESETLOGS NOARCHIVELOG
        MAXLOGFILES 32
        MAXLOGMEMBERS 2
        MAXDATAFILES 32
        MAXINSTANCES 1
        MAXLOGHISTORY 449
    LOGFILE
      GROUP 1 '/path/oracle/dbs/t_log1.f'  SIZE 500K,
      GROUP 2 '/path/oracle/dbs/t_log2.f'  SIZE 500K
    # STANDBY LOGFILE
    DATAFILE
      '/path/oracle/dbs/t_db1.f',
      '/path/oracle/dbs/dbu19i.dbf',
      '/path/oracle/dbs/tbs_11.f',
      '/path/oracle/dbs/smundo.dbf',
      '/path/oracle/dbs/demo.dbf'
    CHARACTER SET WE8DEC
    ;


[← Previous](CREATE-CONTEXT.md)

[Next →](CREATE-DATABASE.md)
