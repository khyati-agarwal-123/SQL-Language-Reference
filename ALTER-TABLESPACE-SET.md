##  ALTER TABLESPACE SET {#GUID-63FEDE73-C1F1-4B7A-98ED-8C34C4073549} 

> **note:** 

This SQL statement is valid only if you are using Oracle Sharding. For more information on Oracle Sharding, refer to [ *Oracle Database Administrator’s Guide* ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-DE8AF949-9F68-4C0C-9B5A-45401EF3C3D1) . 

Purpose 

Use the ` ALTER ` ` TABLESPACE ` ` SET ` statement to change an attribute of an existing tablespace set. The attribute change is applied to all tablespaces in the tablespace set. 

> **note:** See Also: 

[ CREATE TABLESPACE SET ](CREATE-TABLESPACE-SET.md#GUID-877951F1-B2A5-4907-9F0F-EF4F1884E8C4) and [ DROP TABLESPACE SET ](DROP-TABLESPACE-SET.md#GUID-B14EC4C4-87C2-4E79-AB1A-044B620DF1FE)

Prerequisites 

You must be connected to a shard catalog database as an SDB user. 

If you have the ` ALTER ` ` TABLESPACE ` system privilege, then you can perform any ` ALTER ` ` TABLESPACE ` ` SET ` operation. If you have the ` MANAGE ` ` TABLESPACE ` system privilege, then you can only perform the following operations: 

  * Take all tablespaces in a tablespace set online or offline 

  * Begin or end a backup 

  * Make all tablespaces in a tablespace set read only or read write 

  * Set the default logging mode of all tablespaces in a tablespace set to ` LOGGING ` or ` NOLOGGING `

  * Put all tablespaces in a tablespace set in force logging mode or take them out of force logging mode 

  * Resize all data files for a tablespace set 

  * Enable or disable autoextension of all data files for a tablespace set 




Before you can make a tablespace set read only, the following conditions must be met: 

  * The tablespaces in the tablespace set must be online. 

  * The tablespace set must not contain any active rollback segments. Additionally, because the rollback segments of a read-only tablespace set are not accessible, Oracle recommends that you drop the rollback segments before you make a tablespace set read only. 

  * The tablespace set must not be involved in an open backup, because the end of a backup updates the header file of all data files in the tablespace set. 




Syntax 

*alter_tablespace_set* ::= 

![Description of alter_tablespace_set.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_tablespace_set.gif)[ Description of the illustration alter_tablespace_set.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/alter_tablespace_set.md)

*alter_tablespace_attrs* ::= 

![Description of alter_tablespace_attrs.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_tablespace_attrs.gif)[ Description of the illustration alter_tablespace_attrs.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/alter_tablespace_attrs.md)(See the following clauses of ` ALTER ` ` TABLESPACE ` : *default_tablespace_params::=* , *size_clause::=* , *datafile_tempfile_clauses::=* , *tablespace_logging_clauses::=* , *tablespace_state_clauses::=* , *autoextend_clause::=* , *alter_tablespace_encryption::=* ) 

Semantics 

*tablespace_set* 

Specify the name of the tablespace set to be altered. 

*alter_tablespace_attrs* 

Use this clause to change an attribute for all tablespaces in the tablespace set. 

The subclauses of *alter_tablespace_attrs* have the same semantics here as for the ` ALTER ` ` TABLESPACE ` statement, with the following exceptions: 

  * You cannot specify the following subclauses for tablespace sets: 

    * ` MINIMUM ` ` EXTENT ` *size_clause* 

    * ` SHRINK ` ` SPACE ` ` [ KEEP ` *size_clause* ` ] `

    * *tablespace_group_clause* 

    * *flashback_mode_clause* 

    * *tablespace_retention_clause* 

  * For the *datafile_tempfile_clauses* , only the following subclauses are supported for tablespace sets: 

    * ` RENAME ` ` DATAFILE `

    * ` DATAFILE ` ` { ` ` ONLINE ` ` \| ` ` OFFLINE ` ` } `

  * For the *tablespace_state_clauses* , the ` PERMANENT ` and ` TEMPORARY ` subclauses are not supported for tablespace sets. 




> **note:** See Also: 

*alter_tablespace_attrs* in the documentation on ` ALTER ` ` TABLESPACE ` for the full semantics of this clause 

Examples 

Altering a Tablespace Set: Example 

The following statement puts all tablespaces in tablespace set ` ts1 ` in force logging mode: 
    
    
    ```
    ALTER TABLESPACE SET ts1
      FORCE LOGGING;
    ```
