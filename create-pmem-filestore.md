[Previous](CREATE-PLUGGABLE-DATABASE.md) [Next](CREATE-PROCEDURE.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE PMEM FILESTORE

## CREATE PMEM FILESTORE

Purpose

You can create a persistent memory file store with this statement.

Prerequistes

You must have `SYSDBA` privileges to execute `CREATE PMEM FILESTORE` .

You must execute this statement from `CDB$ROOT`.

Syntax

create_pmem_filestore::=

  

![Description of create_pmem_fs.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pmem_fs.gif)  
[Description of the illustration
create_pmem_fs.eps](img_text/create_pmem_fs.md)

  

Semantics

MOUNTPOINT

`file_path` contains the final directory name and must match the PMEM file
store name. If there is no match, the statement will fail.

You must start database instance with at least `NOMOUNT` mode.

It is recommeded to use a `spfile` for the database `init.ora` file.

When you use a `spfile` , the `CREATE PMEM FILESTORE` command automatically
writes the necessary `init.ora` parameters into the `spfile` to remember the
configuration. If you do not use a `spfile` , you must explicitly add the
required parameters to `init.ora` so that the next database instance startup
will automatically mount the PMEM file store.

Example

    
    
    CREATE PMEM FILESTORE cloud_db_1 MOUNTPOINT â/corp/db/cloud_db_1â 
        BACKINGFILE â/var/pmem/foo_1.â SIZE 2T BLOCKSIZE 8K 
        AUTOEXTEND ON NEXT 10G MAXSIZE 3T 


[← Previous](CREATE-PLUGGABLE-DATABASE.md)

[Next →](CREATE-PROCEDURE.md)
