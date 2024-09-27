[Previous](con_id_to_dbid.md) [Next](con_id_to_uid.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CON_ID_TO_GUID

## CON_ID_TO_GUID

Syntax

  

![Description of con_id_to_guid.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/con_id_to_guid.gif)  
[Description of the illustration
con_id_to_guid.eps](img_text/con_id_to_guid.md)

  

Purpose

`CON_ID_TO_GUID` takes as an argument a container `CON_ID` and returns the
container's `GLOBAL UNIQUE ID` ( `GUID`). For `CON_ID` you must specify a
number or an expression that resolves to a number. The function returns a
`NUMBER` value.

This function is useful in a multitentant container database (CDB).

Example

The following query displays the `CON_ID`, `NAME` and `GUID` for all
containers in a CDB:

    
    
    SELECT CON_ID, NAME, GUID FROM V$CONTAINERS;
    
    CON_ID      NAME           GUID
    –------     –-----------   –--------------
       1        CDB$ROOT       A8C0E03CB11A132FE0532684E80A96B3
       2        PDB$SEED       A8DA5D32F8F5590DE053C4E15A0A6EED
       3        CDB1_PDB1      A8DA63CEAD385A5BE053C4E15A0A774A
       4        SALESPDB       A8DA9AB18CE85BD0E053C4E15A0AE2C3
     

The following statement returns the container `GUID` given the container
`CON_ID` 4:

    
    
    SELECT CON_ID_TO_GUID(4) "CON_GUID" FROM DUAL;
        CON_GUID
        –----------------
        A8DA9AB18CE85BD0E053C4E15A0AE2C3 
        


[← Previous](con_id_to_dbid.md)

[Next →](con_id_to_uid.md)
