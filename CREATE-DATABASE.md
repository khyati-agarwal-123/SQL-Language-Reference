[Previous](CREATE-CONTROLFILE.md) [Next](CREATE-DATABASE-LINK.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE DATABASE

## CREATE DATABASE

Note:

This statement prepares a database for initial use and erases any data
currently in the specified files. Use this statement only when you understand
its ramifications.

Note:

In this release of Oracle Database and in subsequent releases, several
enhancements are being made to ensure the security of default database user
accounts. You can find a security checklist for this release in [Oracle
Database Security Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG009). Oracle recommends that you read this checklist
and configure your database accordingly.

Purpose

Use the `CREATE` `DATABASE` statement to create a database, making it
available for general use.

This statement erases all data in any specified data files that already exist
in order to prepare them for initial database use. If you use the statement on
an existing database, then all data in the data files is lost.

After creating the database, this statement mounts it in either exclusive or
parallel mode, depending on the value of the `CLUSTER_DATABASE` initialization
parameter and opens it, making it available for normal use. You can then
create tablespaces for the database.

See Also:

  * [ALTER DATABASE](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986) for information on modifying a database 

  * [Oracle Database Java Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=JJDEV13016) for information on creating an Oracle Java virtual machine 

  * [CREATE TABLESPACE](CREATE-TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9) for information on creating tablespaces 

Prerequisites

To create a database, you must have the `SYSDBA` system privilege. An
initialization parameter file with the name of the database to be created must
be available, and you must be in `STARTUP` `NOMOUNT` mode.

Syntax

create_database::=

![Description of create_database.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_database.gif)  
[Description of the illustration
create_database.eps](img_text/create_database.md)

([database_logging_clauses::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2143359),
[tablespace_clauses::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2143375),
[set_time_zone_clause::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2127485),
[datafile_tempfile_spec::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CHDHEGJH),
[enable_pluggable_database::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__ENABLE_PLUGGABLE_DATABASE-5AE49A3F))

database_logging_clauses::=

![Description of database_logging_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/database_logging_clauses.gif)  
[Description of the illustration
database_logging_clauses.eps](img_text/database_logging_clauses.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF))

tablespace_clauses::=

![Description of tablespace_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/tablespace_clauses.gif)  
[Description of the illustration
tablespace_clauses.eps](img_text/tablespace_clauses.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF),
[default_tablespace::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2186919),
[default_temp_tablespace::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2142113), [undo_tablespace::=](CREATE-
DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__I2127474),
[undo_tablespace::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2127474))

default_tablespace::=

![Description of default_tablespace.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_tablespace.gif)  
[Description of the illustration
default_tablespace.eps](img_text/default_tablespace.md)

default_temp_tablespace::=

![Description of default_temp_tablespace.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_temp_tablespace.gif)  
[Description of the illustration
default_temp_tablespace.eps](img_text/default_temp_tablespace.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF))

extent_management_clause::=

![Description of extent_management_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/extent_management_clause.gif)  
[Description of the illustration
extent_management_clause.eps](img_text/extent_management_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

undo_tablespace::=

![Description of undo_tablespace.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/undo_tablespace.gif)  
[Description of the illustration
undo_tablespace.eps](img_text/undo_tablespace.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF))

set_time_zone_clause::=

![Description of set_time_zone_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/set_time_zone_clause.gif)  
[Description of the illustration
set_time_zone_clause.eps](img_text/set_time_zone_clause.md)

enable_pluggable_database::=

![Description of enable_pluggable_database.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/enable_pluggable_database.gif)  
[Description of the illustration
enable_pluggable_database.eps](img_text/enable_pluggable_database.md)

([tablespace_datafile_clauses::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__TABLESPACE_DATAFILE_CLAUSES-5AE4C9AF),
[undo_mode_clause::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__UNDO_MODE_CLAUSE-5AE4C3C4))

file_name_convert::=

![Description of file_name_convert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/file_name_convert.gif)  
[Description of the illustration
file_name_convert.eps](img_text/file_name_convert.md)

tablespace_datafile_clauses::=

![Description of tablespace_datafile_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/tablespace_datafile_clauses.gif)  
[Description of the illustration
tablespace_datafile_clauses.eps](img_text/tablespace_datafile_clauses.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID),
[autoextend_clause::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CHDBAADC))

undo_mode_clause::=

![Description of undo_mode_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/undo_mode_clause.gif)  
[Description of the illustration
undo_mode_clause.eps](img_text/undo_mode_clause.md)

Semantics

database

Specify the name of the database to be created. The name must match the value
of the `DB_NAME` initialization parameter. The name can be up to 8 bytes long
and can contain only ASCII characters. The following characters are valid in a
database name: alphanumeric characters, underscore (_), number sign (#), and
dollar sign ($). No other characters are valid. The database name must start
with an alphabetic character. Oracle Database writes this name into the
control file. If you subsequently issue an `ALTER` `DATABASE` statement that
explicitly specifies a database name, then Oracle Database verifies that name
with the name in the control file.

The database name is case insensitive and is stored in uppercase ASCII
characters. If you specify the database name as a quoted identifier, then the
quotation marks are silently ignored.

Note:

You cannot use special characters from European or Asian character sets in a
database name. For example, characters with umlauts are not allowed.

If you omit the database name from a `CREATE` `DATABASE` statement, then
Oracle Database uses the name specified by the initialization parameter
`DB_NAME`. The `DB_NAME` initialization parameter must be set in the database
initialization parameter file, and if you specify a different name from the
value of that parameter, then the database returns an error. Refer to
"[Database Object Naming Rules](Database-Object-Names-and-
Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)" for additional
rules to which database names should adhere.

USER SYS ..., USER SYSTEM ...

Use these clauses to establish passwords for the `SYS` and `SYSTEM` users.
These clauses are not mandatory in this release. However, if you specify
either clause, then you must specify both clauses.

If you do not specify these clauses, then Oracle Database creates the default
password `change_on_install` for user `SYS` . You can change this password
later with the `ALTER` `USER` statement.

See Also:

[ALTER USER](ALTER-USER.md#GUID-9FCD038D-8193-4241-85CD-2F4723B27D44)

CONTROLFILE REUSE Clause

Specify `CONTROLFILE` `REUSE` to reuse existing control files identified by
the initialization parameter `CONTROL_FILES`, overwriting any information they
currently contain. Normally you use this clause only when you are re-creating
a database, rather than creating one for the first time. When you create a
database for the first time, Oracle Database creates a control file in the
default destination, which is dependent on the value or several initialization
parameters. See `CREATE` `CONTROLFILE`, "[Semantics](CREATE-
CONTROLFILE.md#GUID-9B389F28-C4D0-405D-BFE6-48237E8BD791__I2146881)".

You cannot use this clause if you also specify a parameter value that requires
that the control file be larger than the existing files. These parameters are
`MAXLOGFILES`, `MAXLOGMEMBERS`, `MAXLOGHISTORY`, `MAXDATAFILES`, and
`MAXINSTANCES`.

If you omit this clause and any of the files specified by `CONTROL_FILES`
already exist, then the database returns an error.

MAXDATAFILES Clause

Specify the initial sizing of the data files section of the control file at
`CREATE` `DATABASE` or `CREATE` `CONTROLFILE` time. An attempt to add a file
whose number is greater than `MAXDATAFILES`, but less than or equal to
`DB_FILES`, causes the Oracle Database control file to expand automatically so
that the data files section can accommodate more files.

The number of data files accessible to your instance is also limited by the
initialization parameter `DB_FILES`.

MAXINSTANCES Clause

Specify the maximum number of instances that can simultaneously have this
database mounted and open. This value takes precedence over the value of
initialization parameter `INSTANCES`. The minimum value is 1. The maximum
value is 1055. The default depends on your operating system.

CHARACTER SET Clause

Specify the character set the database uses to store data. The supported
character sets and default value of this parameter depend on your operating
system.

Restriction on CHARACTER SET

You cannot specify the `AL16UTF16` character set as the database character
set.

See Also:

[Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG002) for more information about choosing a character
set

NATIONAL CHARACTER SET Clause

Specify the national character set used to store data in columns specifically
defined as `NCHAR`, `NCLOB`, or `NVARCHAR2`. Valid values are `AL16UTF16` and
`UTF8`. The default is `AL16UTF16`.

See Also:

[Oracle Database Globalization Support
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=NLSPG0073) for information on Unicode data type support

SET DEFAULT TABLESPACE Clause

Use this clause to determine the default type of subsequently created
tablespaces and of the `SYSTEM` and `SYSAUX` tablespaces. Specify either
`BIGFILE` or `SMALLFILE` to set the default type of subsequently created
tablespaces as a bigfile or smallfile tablespace, respectively.

  * A bigfile tablespace contains only one data file or temp file, which can contain up to approximately 4 billion (232) blocks. The maximum size of the single data file or temp file is 128 terabytes (TB) for a tablespace with 32K blocks and 32TB for a tablespace with 8K blocks. 

  * A smallfile tablespace is a traditional Oracle tablespace, which can contain 1022 data files or temp files, each of which can contain up to approximately 4 million (222) blocks. 

If you omit this clause, then Oracle Database creates bigfile tablespaces by
default for `SYSAUX`, `SYSTEM`, and `USER` tablespaces .

See Also:

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN01102) for more information about bigfile tablespaces 

  * "[Setting the Default Type of Tablespaces: Example](ALTER-DATABASE.md#GUID-8069872F-E680-4511-ADD8-A4E30AF67986__I2187081)" for an example using this syntax 

database_logging_clauses

Use the `database_logging_clauses` to determine how Oracle Database will
handle redo log files for this database.

LOGFILE Clause

Specify one or more files to be used as redo log files. Use the
`redo_log_file_spec` form of `file_specification` to create regular redo log
files in an operating system file system or to create Oracle ASM disk group
redo log files. When using a form of `ASM_filename`, you cannot specify the
`autoextend_clause` of `redo_log_file_spec.`

The `redo_log_file_spec` clause specifies a redo log file group containing one
or more redo log file members (copies). All redo log files specified in a
`CREATE` `DATABASE` statement are added to redo log thread number 1.

See Also:

[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)
for a full description of this clause

If you omit the `LOGFILE` clause, then Oracle Database creates an Oracle-
managed log file member in the default destination, which is one of the
following locations (in order of precedence):

  * If `DB_CREATE_ONLINE_LOG_DEST_``n` is set, then the database creates a log file member in each directory specified, up to the value of the `MAXLOGMEMBERS` initialization parameter. 

  * If the `DB_CREATE_ONLINE_LOG_DEST_``n` parameter is not set, but both the `DB_CREATE_FILE_DEST` and `DB_RECOVERY_FILE_DEST` initialization parameters are set, then the database creates one Oracle-managed log file member in each of those locations. The log file in the `DB_CREATE_FILE_DEST` destination is the first member. 

  * If only the `DB_CREATE_FILE_DEST` initialization parameter is specified, then Oracle Database creates a log file member in that location. 

  * If only the `DB_RECOVERY_FILE_DEST` initialization parameter is specified, then Oracle Database creates a log file member in that location. 

In all these cases, the parameter settings must correctly specify operating
system filenames or creation form Oracle ASM filenames, as appropriate.

If no values are set for any of these parameters, then the database creates a
log file in the default location for the operating system on which the
database is running. This log file is not an Oracle Managed File.

GROUP integer

Specify the number that identifies the redo log file group. The value of
`integer` can range from 1 to the value of the `MAXLOGFILES` parameter. A
database must have at least two redo log file groups. You cannot specify
multiple redo log file groups having the same `GROUP` value. If you omit this
parameter, then Oracle Database generates its value automatically. You can
examine the `GROUP` value for a redo log file group through the dynamic
performance view `V$LOG`.

MAXLOGFILES Clause

Specify the maximum number of redo log file groups that can ever be created
for the database. Oracle Database uses this value to determine how much space
to allocate in the control file for the names of redo log files. The default,
minimum, and maximum values depend on your operating system.

MAXLOGMEMBERS Clause

Specify the maximum number of members, or copies, for a redo log file group.
Oracle Database uses this value to determine how much space to allocate in the
control file for the names of redo log files. The minimum value is 1. The
maximum and default values depend on your operating system.

MAXLOGHISTORY Clause

This parameter is useful only if you are using Oracle Database in `ARCHIVELOG`
mode with Oracle Real Application Clusters (Oracle RAC). Specify the maximum
number of archived redo log files for automatic media recovery of Oracle RAC.
The database uses this value to determine how much space to allocate in the
control file for the names of archived redo log files. The minimum value is 0.
The default value is a multiple of the `MAXINSTANCES` value and depends on
your operating system. The maximum value is limited only by the maximum size
of the control file.

ARCHIVELOG

Specify `ARCHIVELOG` if you want the contents of a redo log file group to be
archived before the group can be reused. This clause prepares for the
possibility of media recovery.

NOARCHIVELOG

Specify `NOARCHIVELOG` if the contents of a redo log file group need not be
archived before the group can be reused. This clause does not allow for the
possibility of media recovery.

The default is `NOARCHIVELOG` mode. After creating the database, you can
change between `ARCHIVELOG` mode and `NOARCHIVELOG` mode with the `ALTER`
`DATABASE` statement.

FORCE LOGGING

Use this clause to put the database into `FORCE` `LOGGING` mode. Oracle
Database will log all changes in the database except for changes in temporary
tablespaces and temporary segments. This setting takes precedence over and is
independent of any `NOLOGGING` or `FORCE` `LOGGING` settings you specify for
individual tablespaces and any `NOLOGGING` settings you specify for individual
database objects.

`FORCE` `LOGGING` mode is persistent across instances of the database. If you
shut down and restart the database, then the database is still in `FORCE`
`LOGGING` mode. However, if you re-create the control file, then Oracle
Database will take the database out of `FORCE` `LOGGING` mode unless you
specify `FORCE` `LOGGING` in the `CREATE` `CONTROLFILE` statement.

Note:

`FORCE` `LOGGING` mode can have performance effects. Refer to [Oracle Database
Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN011) for information on when to use this setting.

See Also:

[CREATE CONTROLFILE](CREATE-
CONTROLFILE.md#GUID-9B389F28-C4D0-405D-BFE6-48237E8BD791)

SET STANDBY NOLOGGING FOR DATA AVAILABILITY | LOAD PERFORMANCE

The `SET STANDBY NOLOGGING` disables logging on the standby. You can specify
it in two modes:

  * SET STANDBY NOLOGGING FOR DATA AVAILABILITY  guarantees full data replication to the standby database. The primary and standby databases are synchronized during the load. In cases of network congestion the primary database will throttle its load. 

  * SET STANDBY NOLOGGING FOR LOAD PERFORMANCE to maintain speed of primary database load and synchronize with the standby later. 

Restrictions SET STANDBY NOLOGGING

The`SET STANDBY NOLOGGING` clause cannot be used at the same time as `FORCE
LOGGING`.

tablespace_clauses

Use the tablespace clauses to configure the `SYSTEM` and `SYSAUX` tablespaces
and to specify a default temporary tablespace and an undo tablespace.

extent_management_clause

Use this clause to create a locally managed `SYSTEM` tablespace. If you omit
this clause, then the `SYSTEM` tablespace will be dictionary managed.

Note:

When you create a locally managed `SYSTEM` tablespace, you cannot change it to
be dictionary managed, nor can you create any other dictionary-managed
tablespaces in this database.

If you specify this clause, then the database must have a default temporary
tablespace, because a locally managed `SYSTEM` tablespace cannot store
temporary segments.

  * If you specify `EXTENT` `MANAGEMENT` `LOCAL` but you do not specify the `DATAFILE` clause, then you can omit the `default_temp_tablespace` clause. Oracle Database will create a default temporary tablespace called `TEMP` with one data file of size 10M with autoextend disabled. 

  * If you specify both `EXTENT` `MANAGEMENT` `LOCAL` and the `DATAFILE` clause, then you must also specify the `default_temp_tablespace` clause and explicitly specify a temp file for that temporary tablespace. 

If you have opened the instance in automatic undo mode, similar requirements
exist for the database undo tablespace:

  * If you specify `EXTENT` `MANAGEMENT` `LOCAL` but you do not specify the `DATAFILE` clause, then you can omit the `undo_tablespace` clause. Oracle Database will create an undo tablespace named `SYS_UNDOTBS`. 

  * If you specify both `EXTENT` `MANAGEMENT` `LOCAL` and the `DATAFILE` clause, then you must also specify the `undo_tablespace` clause and explicitly specify a data file for that tablespace. 

See Also:

[Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN11359) for more information on locally managed and
dictionary-managed tablespaces

DATAFILE Clause

Specify one or more files to be used as data files. All these files become
part of the `SYSTEM` tablespace. Use the data `file_tempfile_spec` form of
`file_specification` to create regular data files and temp files in an
operating system file system or to create Oracle ASM disk group files.

Note:

This clause is optional, as is the `DATAFILE` clause of the `undo_tablespace`
clause. Therefore, to avoid ambiguity, if your intention is to specify a data
file for the `SYSTEM` tablespace with this clause, then do not specify it
immediately after an `undo_tablespace` clause that does not include the
optional `DATAFILE` clause. If you do so, then Oracle Database will interpret
the `DATAFILE` clause to be part of the `undo_tablespace` clause.

The syntax for specifying data files for the `SYSTEM` tablespace is the same
as that for specifying data files during tablespace creation using the
`CREATE` `TABLESPACE` statement, whether you are storing files using Oracle
ASM or in a file system.

See Also:

[CREATE TABLESPACE](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9) for information on
specifying data files

If you are running the database in automatic undo mode and you specify a data
file name for the `SYSTEM` tablespace, then Oracle Database expects to
generate data files for all tablespaces. Oracle Database does this
automatically if you are using Oracle Managed Filesâyou have set a value for
the `DB_CREATE_FILE_DEST` initialization parameter. However, if you are not
using Oracle Managed Files and you specify this clause, then you must also
specify the `undo_tablespace` clause and the `default_temp_tablespace` clause.

If you omit this clause, then:

  * If the `DB_CREATE_FILE_DEST` initialization parameter is set, then Oracle Database creates a 100 MB Oracle-managed data file with a system-generated name in the default file destination specified in the parameter. 

  * If the `DB_CREATE_FILE_DEST` initialization parameter is not set, then Oracle Database creates one data file whose name and size depend on your operating system. 

See Also:

[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)
for syntax

SYSAUX Clause

Oracle Database creates both the `SYSTEM` and `SYSAUX` tablespaces as part of
every database. Use this clause if you are not using Oracle Managed Files and
you want to specify one or more data files for the `SYSAUX` tablespace.

You must specify this clause if you have specified one or more data files for
the `SYSTEM` tablespace using the `DATAFILE` clause. If you are using Oracle
Managed Files and you omit this clause, then the database creates the `SYSAUX`
data files in the default location set up for Oracle Managed Files.

If you have enabled Oracle Managed Files and you omit the `SYSAUX` clause,
then the database creates the `SYSAUX` tablespace as an online, permanent,
locally managed tablespace with one data file of 100 MB, with logging enabled
and automatic segment-space management.

The syntax for specifying data files for the `SYSAUX` tablespace is the same
as that for specifying data files during tablespace creation using the
`CREATE` `TABLESPACE` statement, whether you are storing files using Oracle
ASM or in a file system.

See Also:

  * [CREATE TABLESPACE](CREATE-TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9) for information on creating the `SYSAUX` tablespace during database upgrade and for information on specifying data files in a tablespace 

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN00203) for more information on creating the `SYSAUX` tablespace 

default_tablespace

Specify this clause to create a default permanent tablespace for the database.
Oracle Database creates a smallfile tablespace and subsequently will assign to
this tablespace any non-`SYSTEM` users for whom you do not specify a different
permanent tablespace. If you do not specify this clause, then the `SYSTEM`
tablespace is the default permanent tablespace for non-`SYSTEM` users.

The `DATAFILE` clause and `extent_management_clause` have the same semantics they have in a `CREATE` `TABLESPACE` statement. Refer to "[DATAFILE | TEMPFILE Clause](CREATE-TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2171920)" and [extent_management_clause](CREATE-TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2063392) for information on these clauses. 

default_temp_tablespace

Use this clause to create a default shared temporary tablespace or a default
local temporary tablespace. Oracle Database will assign to these temporary
tablespaces any users for whom you do not specify different temporary
tablespaces.

  * Specify `DEFAULT` `TEMPORARY` `TABLESPACE` to create a default shared temporary tablespace for the database. Shared temporary tablespaces were available in prior releases of Oracle Database and were called "temporary tablespaces." Elsewhere in this guide, the term "temporary tablespace" refers to a shared temporary tablespace unless specified otherwise. If you do not specify this clause, and if the database does not create a default shared temporary tablespace automatically in the process of creating a locally managed `SYSTEM` tablespace, then the `SYSTEM` tablespace is the default shared temporary tablespace. 

  * Starting with Oracle Database 12c Release 2 (12.2), you can specify `DEFAULT` `LOCAL` `TEMPORARY` `TABLESPACE` to create a default local temporary tablespace. Local temporary tablespaces are useful for Oracle Real Application Clusters and Oracle Flex Clusters. They store a separate, nonshared temp file for each database instance, which can improve I/O performance. A local temporary tablespace must be a `BIGFILE` tablespace. 

    * Specify `FOR` `ALL` to instruct the database to create separate, nonshared temp files for all HUB and LEAF nodes. 

    * Specify `FOR` `LEAF` to instruct the database to create separate nonshared temp files for only LEAF nodes. If you specify this clause, then HUB nodes will use the default shared temporary tablespace. For SQL operations that span both HUB and LEAF nodes, HUB nodes will use the default shared temporary tablespace and LEAF nodes will use the default local temporary tablespace. 

If you do not create a local temporary tablespace, then HUB and LEAF nodes
will use the default shared temporary tablespace.

Specify `BIGFILE` or `SMALLFILE` to determine whether the default temporary
tablespace is a bigfile or smallfile tablespace. These clauses have the same
semantics as in the "[SET DEFAULT TABLESPACE Clause](CREATE-
DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__I2177341)".

The `TEMPFILE` clause part of this clause is optional if you have enabled
Oracle Managed Files by setting the `DB_CREATE_FILE_DEST` initialization
parameter. If you have not specified a value for this parameter, then the
`TEMPFILE` clause is required. If you have specified `BIGFILE`, then you can
specify only one temp file in this clause.

The syntax for specifying temp files for the default temporary tablespace is
the same as that for specifying temp files during temporary tablespace
creation using the `CREATE` `TABLESPACE` statement, whether you are storing
files using Oracle ASM or in a file system.

The `extent_management_clause` clause has the same semantics in `CREATE`
`DATABASE` and `CREATE` `TABLESPACE` statements. For complete information,
refer to the `CREATE` `TABLESPACE` ... [extent_management_clause](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2063392).

See Also:

[CREATE TABLESPACE](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9) for information on
specifying temp files

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

Restrictions on Default Temporary Tablespaces

Default temporary tablespaces are subject to the following restrictions:

  * You cannot specify the `SYSTEM` tablespace in this clause. 

  * The default temporary tablespace must have a standard block size.

undo_tablespace

If you have opened the instance in automatic undo mode (the `UNDO_MANAGEMENT`
initialization parameter is set to `AUTO`, which is the default), then you can
specify the `undo_tablespace` to create a tablespace to be used for undo data.
Oracle strongly recommends that you use automatic undo mode. However, if you
want undo space management to be handled by way of rollback segments, then you
must omit this clause. You can also omit this clause if you have set a value
for the `UNDO_TABLESPACE` initialization parameter. If that parameter has been
set, and if you specify this clause, then `tablespace` must be the same as
that parameter value.

  * Specify `BIGFILE` if you want the undo tablespace to be a bigfile tablespace. A bigfile tablespace contains only one data file, which can be up to 8 exabytes (8 million terabytes) in size. 

Tablespaces `SYSAUX`, `SYSTEM`, and `USER` are `BIGFILE` by default.

  * Specify `SMALLFILE` if you want the undo tablespace to be a smallfile tablespace. A smallfile tablespace is a traditional Oracle Database tablespace, which can contain 1022 data files or temp files, each of which can contain up to approximately 4 million (222) blocks. 

  * The `DATAFILE` clause part of this clause is optional if you have enabled Oracle Managed Files by setting the `DB_CREATE_FILE_DEST` initialization parameter. If you have not specified a value for this parameter, then the `DATAFILE` clause is required. If you have specified `BIGFILE`, then you can specify only one data file in this clause. 

The syntax for specifying data files for the undo tablespace is the same as
that for specifying data files during tablespace creation using the `CREATE`
`TABLESPACE` statement, whether you are storing files using Oracle ASM or in a
file system.

See Also:

[CREATE TABLESPACE](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9) for information on
specifying data files

If you specify this clause, then Oracle Database creates an undo tablespace
named `tablespace`, creates the specified data file(s) as part of the undo
tablespace, and assigns this tablespace as the undo tablespace of the
instance. Oracle Database will manage undo data using this undo tablespace.
The `DATAFILE` clause of this clause has the same behavior as described in
"[DATAFILE Clause](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2150088)".

If you have specified a value for the `UNDO_TABLESPACE` initialization
parameter in your initialization parameter file before mounting the database,
then you must specify the same name in this clause. If these names differ,
then Oracle Database will return an error when you open the database.

If you omit this clause, then Oracle Database creates a default database with
a default smallfile undo tablespace named `SYS_UNDOTBS` and assigns this
default tablespace as the undo tablespace of the instance. This undo
tablespace allocates disk space from the default files used by the `CREATE`
`DATABASE` statement, and it has an initial extent of 10M. Oracle Database
handles the system-generated data file as described in "[DATAFILE
Clause](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2150088)". If Oracle Database is unable
to create the undo tablespace, then the entire `CREATE` `DATABASE` operation
fails.

See Also:

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN013) for information on automatic undo management and undo tablespaces 

  * [CREATE TABLESPACE](CREATE-TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9) for information on creating an undo tablespace after database creation 

set_time_zone_clause

Use the `SET` `TIME_ZONE` clause to set the time zone of the database. You can
specify the time zone in two ways:

  * By specifying a displacement from UTC (Coordinated Universal Timeâformerly Greenwich Mean Time). The valid range of `hh:mi` is -12:00 to +14:00. 

  * By specifying a time zone region. To see a listing of valid time zone region names, query the `TZNAME` column of the `V$TIMEZONE_NAMES` dynamic performance view. 

Note:

Oracle recommends that you set the database time zone to UTC (`0:00`). Doing
so can improve performance, especially across databases, as no conversion of
time zones will be required.

See Also:

[Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN003) for information on the dynamic performance
views

Oracle Database normalizes all `TIMESTAMP` `WITH` `LOCAL` `TIME` `ZONE` data
to the time zone of the database when the data is stored on disk. If you do
not specify the `SET` `TIME_ZONE` clause, then the database uses the operating
system time zone of the server. If the operating system time zone is not a
valid Oracle Database time zone, then the database time zone defaults to UTC.

USER_DATA TABLESPACE Clause

This clause lets you create a tablespace that is used for storing user data
and database options such as Oracle XML DB.

If you specify this clause when creating a multitenant container database
(CDB), then the tablespace is created as part of the seed. Pluggable databases
(PDBs) subsequently created using the seed will include this tablespace and
its data file. The tablespace and data file specified in this clause are not
used by the root.

Specify `BIGFILE` or `SMALLFILE` to determine whether the tablespace is a
bigfile or smallfile tablespace. If you omit these clauses, then Oracle
Database creates a tablespace of the type that you specify with the `SET`
`DEFAULT` `TABLESPACE` clause. If you do not specify the `SET` `DEFAULT`
`TABLESPACE` clause, then Oracle Database creates a smallfile tablespace.
These clauses have the same semantics as in the "[SET DEFAULT TABLESPACE
Clause](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__I2177341)".

Use the `datafile_tempfile_spec` clause to specify one or more data files for
the tablespace. Refer to
[datafile_tempfile_spec](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1030551)
for the full semantics of this clause.

enable_pluggable_database

Starting with Oracle Database 21c, the `ENABLE_PLUGGABLE_DATABASE`
initialization parameter is set to `TRUE` by default. If you set the
`ENABLE_PLUGGABLE_DATABASE` initialization parameter to `FALSE`, the command
will fail.

The `CREATE` `DATABASE` `enable_pluggable_database` statement creates a CDB
that contains a root and a seed container. You then create PDBs in the CDB by
using the `CREATE PLUGGABLE DATABASE` statement.

See Also:

  * [Creating and configuring a cdb](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MULTI-GUID-77D4BBA7-2A64-46D9-A2B8-C56060772215). 

  * [CREATE PLUGGABLE DATABASE](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC)

  * "[Creating a CDB: Example](CREATE-DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__BGEDGEGE)"

file_name_convert

Use the `file_name_convert` clause to determine how the database generates the
names of files (such as data files and wallet files) associated with the seed
by using the names of files associated with the root.

  * For `filename_pattern`, specify a string found in file names associated with the root. 

  * For `replacement_filename_pattern`, specify a replacement string. 

Oracle Database will replace `filename_pattern` with
`replacement_filename_pattern` when generating the names of files associated
with the seed.

File name patterns cannot match files or directories managed by Oracle Managed
Files.

You can specify `FILE_NAME_CONVERT` `=` `NONE`, which is the same as omitting
this clause. If you omit this clause, then the database first attempts to use
Oracle Managed Files to generate seed file names. If you are not using Oracle
Managed Files, then the database uses the `PDB_FILE_NAME_CONVERT`
initialization parameter to generate file names. If this parameter is not set,
then an error occurs.

tablespace_datafile_clauses

Use these clauses to specify attributes for all data files comprising the
`SYSTEM` and `SYSAUX` tablespaces in the seed PDB. If you do not specify
`SIZE` `size_clause`, then the data file size for a given tablespace will be
set to a predetermined fraction of the size of the corresponding root data
file. If you do not specify the `autoextend_clause`, then those values are
inherited from the root.

Refer to
[size_clause](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517) and
[autoextend_clause](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJAJIHDC)
for the full semantics of these clauses.

undo_mode_clause

This clause lets you specify local undo mode or shared undo mode for the CDB.

  * Use `LOCAL` `UNDO` `ON` to specify local undo mode for the CDB. In this mode, every container in the CDB uses local undo. 

  * Use `LOCAL` `UNDO` `OFF` to specify shared undo mode for the CDB. In this mode, there is one active undo tablespace for a single-instance CDB, or for an Oracle RAC CDB, there is one active undo tablespace for each instance. 

If you omit this clause, then the default is `LOCAL` `UNDO` `OFF`.

USING MIRROR COPY

Use this clause to create a database with `new_database_name` using the
prepared files of the mirror copy, identified by `mirror_name`.

Examples

Creating a Database: Example

The following statement creates a database and fully specifies each argument:

    
    
    CREATE DATABASE sample
       CONTROLFILE REUSE 
       LOGFILE
          GROUP 1 ('diskx:log1.log', 'disky:log1.log') SIZE 50K, 
          GROUP 2 ('diskx:log2.log', 'disky:log2.log') SIZE 50K 
       MAXLOGFILES 5 
       MAXLOGHISTORY 100 
       MAXDATAFILES 10 
       MAXINSTANCES 2 
       ARCHIVELOG 
       CHARACTER SET AL32UTF8
       NATIONAL CHARACTER SET AL16UTF16
       DATAFILE  
          'disk1:df1.dbf' AUTOEXTEND ON,
          'disk2:df2.dbf' AUTOEXTEND ON NEXT 10M MAXSIZE UNLIMITED
       DEFAULT TEMPORARY TABLESPACE temp_ts
       UNDO TABLESPACE undo_ts 
       SET TIME_ZONE = '+02:00';
    

This example assumes that you have enabled Oracle Managed Files by specifying
a value for the `DB_CREATE_FILE_DEST` parameter in your initialization
parameter file. Therefore no file specification is needed for the `DEFAULT`
`TEMPORARY` `TABLESPACE` and `UNDO` `TABLESPACE` clauses.

Creating a CDB: Example

The following statement creates a CDB `newcdb`. The `ENABLE PLUGGABLE
DATABASE` clause indicates that a CDB is being created. The CDB will contain a
root (`CDB$ROOT`) and a seed (`PDB$SEED`). The `FILE_NAME_CONVERT` clause
specifies that names of files for the seed will be generated by replacing
`/u01/app/oracle/oradata/newcdb` in the names of files associated with the
root with `/u01/app/oracle/oradata/pdbseed`.

    
    
    CREATE DATABASE newcdb
      USER SYS IDENTIFIED BY sys_password
      USER SYSTEM IDENTIFIED BY system_password
      LOGFILE GROUP 1 ('/u01/logs/my/redo01a.log','/u02/logs/my/redo01b.log')
                 SIZE 100M BLOCKSIZE 512,
              GROUP 2 ('/u01/logs/my/redo02a.log','/u02/logs/my/redo02b.log')
                 SIZE 100M BLOCKSIZE 512,
              GROUP 3 ('/u01/logs/my/redo03a.log','/u02/logs/my/redo03b.log')
                 SIZE 100M BLOCKSIZE 512
      MAXLOGHISTORY 1
      MAXLOGFILES 16
      MAXLOGMEMBERS 3
      MAXDATAFILES 1024
      CHARACTER SET AL32UTF8
      NATIONAL CHARACTER SET AL16UTF16
      EXTENT MANAGEMENT LOCAL
      DATAFILE '/u01/app/oracle/oradata/newcdb/system01.dbf'
        SIZE 700M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
      SYSAUX DATAFILE '/u01/app/oracle/oradata/newcdb/sysaux01.dbf'
        SIZE 550M REUSE AUTOEXTEND ON NEXT 10240K MAXSIZE UNLIMITED
      DEFAULT TABLESPACE deftbs
        DATAFILE '/u01/app/oracle/oradata/newcdb/deftbs01.dbf'
        SIZE 500M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED
      DEFAULT TEMPORARY TABLESPACE tempts1
        TEMPFILE '/u01/app/oracle/oradata/newcdb/temp01.dbf'
        SIZE 20M REUSE AUTOEXTEND ON NEXT 640K MAXSIZE UNLIMITED
      UNDO TABLESPACE undotbs1
        DATAFILE '/u01/app/oracle/oradata/newcdb/undotbs01.dbf'
        SIZE 200M REUSE AUTOEXTEND ON NEXT 5120K MAXSIZE UNLIMITED
      ENABLE PLUGGABLE DATABASE
        SEED
        FILE_NAME_CONVERT = ('/u01/app/oracle/oradata/newcdb/',
                             '/u01/app/oracle/oradata/pdbseed/')
        SYSTEM DATAFILES SIZE 125M AUTOEXTEND ON NEXT 10M MAXSIZE UNLIMITED
        SYSAUX DATAFILES SIZE 100M
      USER_DATA TABLESPACE usertbs
        DATAFILE '/u01/app/oracle/oradata/pdbseed/usertbs01.dbf'
        SIZE 200M REUSE AUTOEXTEND ON MAXSIZE UNLIMITED;


[← Previous](CREATE-CONTROLFILE.md)

[Next →](CREATE-DATABASE-LINK.md)
