[Previous](COMPOSE.html) [Next](CON_GUID_TO_ID.html) JavaScript must be enabled to correctly display this content 

  1. [SQL Language Reference ](index.html)2. [Functions](Functions.html)
  3. CON_DBID_TO_ID



## CON_DBID_TO_ID

Syntax

![Description of con_dbid_to_id.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/con_dbid_to_id.gif)[Descriptionof the illustration con_dbid_to_id.eps](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/con_dbid_to_id.md)

Purpose

`CON_DBID_TO_ID` takes as its argument a container DBID and returns the container ID. For `container_dbid`, specify a `NUMBER` value or any value that can be implicitly converted to `NUMBER`. The function returns a `NUMBER` value. 

This function is useful in a multitenant container database (CDB). If you use this function in a non-CDB, then it returns 0.

Example

The following query displays the ID and DBID for all containers in a CDB. The sample output shown is for the purpose of this example.
    
    
    SELECT CON_ID, DBID
      FROM V$CONTAINERS;
    
        CON_ID       DBID
    ---------- ----------
             1 1930093401
             2 4054529501
             4 2256797992
    

The following statement returns the ID for the container with DBID 2256797992:
    
    
    SELECT CON_DBID_TO_ID(2256797992) "Container ID"
      FROM DUAL;
    
    Container ID
    ------------
               4

[← Previous](COMPOSE.md)

[Next →](CON_GUID_TO_ID.md)
