[Previous](ALTER-PLUGGABLE-DATABASE.md) [Next](ALTER-PROCEDURE.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER PMEM FILESTORE

## ALTER PMEM FILESTORE

Purpose

Use this command to change the attributes of a PMEM file store.

Prerequisites

You cannot change the block size of a PMEM file store.

Syntax

alter_pmem_filestore  
![Description of alter_pmem_fs.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_pmem_fs.gif)  
[Description of the illustration
alter_pmem_fs.eps](img_text/alter_pmem_fs.md)  

Semantics

MOUNT

Use this command to mount a PMEM file store. If you have already specified the
mount point and backing file paths in the `init.ora` file you can issue the
command like this:

    
    
    ALTER PMEM FILESTORE 'filestore_name' MOUNT

You can also specify the mount point and backing file paths in the command
line. In this case, you must ensure that there is no mismatch between the
values in the `init.ora` file and the values you specify in the command line.
The command fails when a mismatch occurs, unless you specify `FORCE` to
override the values in the `init.ora` file. The paths on the command line
become the new paths for the PMEM file store.

If you use a `spfile`, then the parameters are automatically updated with the
new paths specified on the command line.

Use the mount PMEM file store command in cases when the PMEM file store was
not already automatically mounted during database startup.

Specify the mount point path or the backing file path on the command line
when:

  * You have not specified either the mount point path or the backing file path in the `init.ora` file 

  * You want to specify new values for either the mount point path or the backing file path 

Before you can change the mount point and the backing file, you must first
dismount the file store.

DISMOUNT

Use this command to dismount a PMEM file store. You must ensure that the
database instance is in `NOMOUNT` mode.

Examples

Example 1: Resize File Store Named cloud_db_1

    
    
    ALTER PMEM FILESTORE cloud_db_1 RESIZE 5T

Example 2: Mount File Store Named cloud_db_1

    
    
    ALTER  PMEM FILESTORE cloud_db_1 MOUNT  MOUNTPOINT â/corp/db/cloud_db_1â
        BACKINGFILE â/var/pmem/foo_1â

Example 3: Dismount File Store Named cloud_db_1

    
    
    ALTER PMEM FILESTORE cloud_db_1 DISMOUNT


[← Previous](ALTER-PLUGGABLE-DATABASE.md)

[Next →](ALTER-PROCEDURE.md)
