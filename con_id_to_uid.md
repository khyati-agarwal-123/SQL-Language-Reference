[Previous](con_id_to_guid.html) [Next](CON_NAME_TO_ID.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. CON_ID_TO_UID



## CON_ID_TO_UID

Syntax

  


![Description of con_id_to_uid.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/con_id_to_uid.gif)[Descriptionof the illustration con_id_to_uid.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/con_id_to_uid.md)

  


Purpose

`CON_ID_TO_UID` takes as an argument a container `CON_ID` and returns the container's `UNIQUE ID` ( `UID`). For `CON_ID` you must specify a number or an expression that resolves to a number. The function returns a `NUMBER` value. 

This function is useful in a multitentant container database (CDB). 

Example

The following query displays the `CON_ID`, `NAME` and `CON_UID` for all containers in a CDB: 
    
    
    SELECT CON_ID, NAME, CON_UID FROM V$CONTAINERS;
    
    CON_ID      NAME           CON_UID
    –------     –-----------   –--------------
       1        CDB$ROOT       1
       2        PDB$SEED       2929762556
       3        CDB1_PDB1      3483444080
       4        SALESPDB       2221053340 

The following statement returns the container `CON_UID` given the container `CON_ID` 4: 
    
    
    SELECT CON_ID_TO_UID(4) "PDB_UID" FROM DUAL;
        PDB_UID
        –------------
        2221053340

[← Previous](con_id_to_guid.md)

[Next →](CON_NAME_TO_ID.md)
