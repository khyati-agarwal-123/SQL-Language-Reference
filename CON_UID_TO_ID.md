[Previous](CON_NAME_TO_ID.md) [Next](CONCAT.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. CON_UID_TO_ID

## CON_UID_TO_ID

Syntax

![Description of con_uid_to_id.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/con_uid_to_id.gif)  
[Description of the illustration
con_uid_to_id.eps](img_text/con_uid_to_id.md)

Purpose

`CON_UID_TO_ID` takes as its argument a container UID (unique identifier) and
returns the container ID. For `container_uid`, specify a `NUMBER` value or any
value that can be implicitly converted to `NUMBER`. The function returns a
`NUMBER` value.

This function is useful in a multitenant container database (CDB). If you use
this function in a non-CDB, then it returns 0.

Example

The following query displays the ID and UID for all containers in a CDB. The
sample output shown is for the purpose of this example.

    
    
    SELECT CON_ID, CON_UID
      FROM V$CONTAINERS;
    
        CON_ID    CON_UID
    ---------- ----------
             1          1
             2 4054529501
             4 2256797992
    

The following query returns the ID for the container with UID 2256797992:

    
    
    SELECT CON_UID_TO_ID(2256797992) "Container ID"
      FROM DUAL;
    
    Container ID
    ------------
               4


[← Previous](CON_NAME_TO_ID.md)

[Next →](CONCAT.md)
