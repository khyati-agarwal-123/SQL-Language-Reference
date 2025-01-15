##  CREATE PMEM FILESTORE {#GUID-2518DAF0-E174-4593-86C2-D8E48FBED1FE} 

Purpose 

You can create a persistent memory file store with this statement. 

Prerequistes 

You must have ` SYSDBA ` privileges to execute ` CREATE PMEM FILESTORE ` . 

You must execute this statement from ` CDB$ROOT ` . 

Syntax 

*create_pmem_filestore* ::= 

  


![Description of create_pmem_fs.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pmem_fs.gif)[ Description of the illustration create_pmem_fs.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/create_pmem_fs.md)

  


Semantics 

MOUNTPOINT 

*file_path* contains the final directory name and must match the PMEM file store name. If there is no match, the statement will fail. 

You must start database instance with at least ` NOMOUNT ` mode. 

It is recommeded to use a ` spfile ` for the database ` init.ora ` file. 

When you use a ` spfile ` , the ` CREATE PMEM FILESTORE ` command automatically writes the necessary ` init.ora ` parameters into the ` spfile ` to remember the configuration. If you do not use a ` spfile ` , you must explicitly add the required parameters to ` init.ora ` so that the next database instance startup will automatically mount the PMEM file store. 

Example 
    
    
    ```
    CREATE PMEM FILESTORE cloud_db_1 MOUNTPOINT ‘/corp/db/cloud_db_1’ 
        BACKINGFILE ‘/var/pmem/foo_1.’ SIZE 2T BLOCKSIZE 8K 
        AUTOEXTEND ON NEXT 10G MAXSIZE 3T 
    ```
