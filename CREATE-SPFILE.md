[Previous](CREATE-SEQUENCE.md) [Next](CREATE-SYNONYM.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. CREATE SPFILE 

## CREATE SPFILE

Purpose

Use the `CREATE` `SPFILE` statement to create a server parameter file either
from a traditional plain-text initialization parameter file or from the
current system-wide settings. Server parameter files are binary files that
exist only on the server and are called from client locations to start up the
database.

Server parameter files let you make persistent changes to individual
parameters. When you use a server parameter file, you can specify in an
`ALTER` `SYSTEM` `SET` `parameter` statement that the new parameter value
should be persistent. This means that the new value applies not only in the
current instance, but also to any instances that are started up subsequently.
Traditional plain-text parameter files do not let you make persistent changes
to parameter values.

Server parameter files are located on the server, so they allow for automatic
database tuning by Oracle Database and for backup by Recovery Manager (RMAN).

To use a server parameter file when starting up the database, you must create
it using the `CREATE` `SPFILE` statement.

All instances in an Oracle Real Application Clusters environment must use the
same server parameter file. However, when otherwise permitted, individual
instances can have different settings of the same parameter within this one
file. Instance-specific parameter definitions are specified as `SID.parameter
= value`, where `SID` is the instance identifier.

The method of starting up the database with a server parameter file depends on
whether you create a default or nondefault server parameter file. Refer to
"[Creating a Server Parameter File: Examples](CREATE-
SPFILE.md#GUID-D3E295B7-A3A4-43D3-8BBD-5CBE171A2E52__I2087518)" for examples
of how to use server parameter files.

Note on Creating Server Parameter Files in a CDB

When you create a server parameter file in a multitenant container database
(CDB), the current container can be the root or a PDB.

  * If the current container is the root, then the values that you set for initialization parameters in the root are used as default values for all other containers.

  * If the current container is a PDB, then the database stores the PDB's initialization parameter values internally, rather than in a file. Therefore, you cannot specify an `spfile_name`. The values that you set for initialization parameters in the PDB are persistent and override any values set for those parameters in the root. 

When PDB is in `MOUNT` state, any query on `V$parameter` ( show parameter)
shows the values from `ROOT` parameter table.

When PDB is in `OPEN` state, any query on `V$parameter` ( show parameter)
shows the values from PDB parameter table.

You can subsequently use the `ALTER` `SYSTEM` statement to modify
initialization parameter values for the root or a PDB.

See Also:

  * [CREATE PFILE](CREATE-PFILE.md#GUID-C01CBA1C-F477-49BE-AD58-F2FED046D561) for information on creating a regular text parameter file from a binary server parameter file 

  * [Oracle Database Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN00202) for information on traditional plain-text initialization parameter files and server parameter files 

  * [Oracle Real Application Clusters Administration and Deployment Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=RACAD815) for information on using server parameter files in an Oracle Real Application Clusters environment 

Prerequisites

You must have the `SYSBACKUP`, `SYSDBA`, `SYSDG`, or `SYSOPER` system
privilege to execute this statement. You can execute this statement before or
after instance startup. However, if you have already started an instance using
`spfile_name`, you cannot specify the same `spfile_name` in this statement.

To create a server parameter file in a CDB, the current container must be the
root and you must have the commonly granted `SYSBACKUP`, `SYSDBA`, `SYSDG`, or
`SYSOPER` system privilege.

Syntax

create_spfile::=

![Description of create_spfile.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_spfile.gif)  
[Description of the illustration
create_spfile.eps](img_text/create_spfile.md)

Semantics

spfile_name

This clause lets you specify a name for the server parameter file you are
creating.

If you specify `spfile_name`, then Oracle Database creates a nondefault server
parameter file.

  * For `spfile_name`, you can specify a traditional filename, a file in an Oracle ACFS (Oracle Advanced Cluster File System) file system, or an Oracle Storage Management (Oracle ASM) filename. 

  * If you specify a traditional filename or a file in an Oracle ACFS file system, then `spfile_name` can include a path prefix. If you do not specify such a path prefix, then the database adds the path prefix for the default storage location, which is platform dependent. 

  * If you specify the Oracle ASM filename syntax, then the database creates the spfile in an Oracle ASM disk group.

  * When using a nondefault server parameter file, you must specify the server parameter filename in the `STARTUP` command when you start up the database. The exception to this rule is as follows: 

    * If the database is defined as a resource in Oracle Clusterware, the instance from which the command is issued is running, and you specify the `spfile_name`, specify the `FROM` `PFILE` clause, and omit the `AS` `COPY` clause, then this statement automatically updates the SPFILE in the database resource. In this case, you can start up the database without referring to the server parameter file by name. If the instance from which the command is issued is not running, then the SPFILE in the database resource must be updated manually using `srvctl` `modify` `database` `-d` `dbname` `-spfile` `spfile_path`. 

If you omit `spfile_name`, then Oracle Database uses the platform-specific
default server parameter filename. If such a file already exists on the
server, then this statement overwrites it. When using a default server
parameter file, you can start up the database without referring to the file by
name.

Restriction on spfile_name

You cannot specify `spfile_name` when creating a server parameter file while
connected to a PDB.

See Also:

  * "[Creating a Server Parameter File: Examples](CREATE-SPFILE.md#GUID-D3E295B7-A3A4-43D3-8BBD-5CBE171A2E52__I2087518)" for information on starting up the database with default and nondefault server parameter files 

  * [file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688) for the syntax of traditional and Oracle ASM filenames and [ALTER DISKGROUP](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557) for information on modifying the characteristics of an Oracle ASM file 

  * The appropriate operating-system-specific documentation for default parameter file names

pfile_name

Specify the traditional plain-text initialization parameter file from which
you want to create a server parameter file. The traditional parameter file
must reside on the server.

  * If you specify `pfile_name` and the traditional parameter file does not reside in the default directory for parameter files on your operating system, then you must specify the full path. 

  * If you do not specify `pfile_name`, then Oracle Database looks in the default directory for parameter files on your operating system for the default parameter filename and uses that file. If that file does not exist in the expected directory, then the database returns an error. 

Note:

In an Oracle Real Application Clusters environment, you must first combine all
instance parameter files into one file before specifying that filename in this
statement to create a server parameter file. For information on accomplishing
this step, see [Oracle Real Application Clusters Administration and Deployment
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=RACAD020).

AS COPY

This clause applies only if the database is defined as a resource in Oracle
Clusterware. By default, if you specify both the `spfile_name` and the `FROM`
`PFILE` clause, then the `CREATE` `SPFILE` statement automatically updates the
SPFILE in the database resource. You can specify `AS` `COPY` to prevent the
database from updating the SPFILE in the database resource.

MEMORY

Specify `MEMORY` to create an spfile using the current system-wide parameter
settings. In an Oracle RAC environment, the created file will contain the
parameter settings from each instance.

Examples

Creating a Server Parameter File: Examples

The following example creates a default server parameter file from a
traditional plain-text parameter file named `t_init1.ora`:

    
    
    CREATE SPFILE 
       FROM PFILE = '$ORACLE_HOME/work/t_init1.ora';

Note:

Typically you will need to specify the full path and filename for parameter
files on your operating system.

When you create a default server parameter file, you subsequently start up the
database using that server parameter file by using the SQL*Plus command
`STARTUP` without the `PFILE` parameter, as follows:

    
    
    STARTUP
    

The following example creates a nondefault server parameter file
`s_params.ora` from a traditional plain-text parameter file named
`t_init1.ora`:

    
    
    CREATE SPFILE = 's_params.ora' 
       FROM PFILE = '$ORACLE_HOME/work/t_init1.ora';
    

When you create a nondefault server parameter file, you subsequently start up
the database by first creating a traditional parameter file containing the
following single line:

    
    
    spfile = 's_params.ora'
    

The name of this parameter file must comply with the naming conventions of
your operating system. You then use the single-line parameter file in the
`STARTUP` command. The following example shows how to start up the database,
assuming that the single-line parameter file is named `new_param.ora`:

    
    
    STARTUP PFILE=new_param.ora
    


[← Previous](CREATE-SEQUENCE.md)

[Next →](CREATE-SYNONYM.md)
