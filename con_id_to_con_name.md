[Previous](CON_GUID_TO_ID.md) [Next](con_id_to_dbid.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CON_ID_TO_CON_NAME

## CON_ID_TO_CON_NAME

Syntax

  

![Description of con_id_to_con_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/con_id_to_con_name.gif)  
[Description of the illustration
con_id_to_con_name.eps](img_text/con_id_to_con_name.md)

  

Purpose

`CON_ID_TO_CON_NAME` takes as an argument a container `CON_ID` and returns the
container `NAME`.

For `CON_ID` you must specify a number or an expression that resolves to a
number. The function returns a `NUMBER` value.

This function is useful in a multitentant container database (CDB). If you use
this function in a non-CDB, then it returns 0.

Example

    
    
    SELECT CON_ID, NAME FROM V$CONTAINERS;
        CON_ID         NAME 
       –--------       –------------
           1           CDB$ROOT
           2           PDB$SEED
           3           CDB1_PDB1
           4           SALESPDB   
    

The following statement returns the container `NAME` given the container
`CON_ID` 4:

    
    
    SELECT CON_ID_TO_CON_NAME(4) "CON_NAME" FROM DUAL;
         CON_NAME
         –-------
         SALESDB


[← Previous](CON_GUID_TO_ID.md)

[Next →](con_id_to_dbid.md)
