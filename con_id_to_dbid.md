[Previous](con_id_to_con_name.md) [Next](con_id_to_guid.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CON_ID_TO_DBID

## CON_ID_TO_DBID

Syntax

  

![Description of con_id_to_dbid.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/con_id_to_dbid.gif)  
[Description of the illustration
con_id_to_dbid.eps](img_text/con_id_to_dbid.md)

  

Purpose

`CON_ID_TO_DBID` takes as an argument a container `CON_ID` and returns the
container `DBID`. For `CON_ID` you must specify a number or an expression that
resolves to a number. The function returns a `NUMBER` value.

This function is useful in a multitentant container database (CDB). If you use
this function in a non-CDB, then it returns 0.

Example

    
    
    SELECT CON_ID, NAME, DBID FROM V$CONTAINERS;
    
    CON_ID      NAME           DBID
    –------     –-----------   –--------------
       1        CDB$ROOT       2048400776
       2        PDB$SEED       2929762556
       3        CDB1_PDB1      3483444080
       4        SALESPDB       2221053340 

The following statement returns the container `DBID` given the container
`CON_ID` 4:

    
    
    SELECT CON_ID_TO_DBID(4) FROM DUAL;
        DBID
        –------------
        2221053340


[← Previous](con_id_to_con_name.md)

[Next →](con_id_to_guid.md)
