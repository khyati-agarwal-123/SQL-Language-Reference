##  UID {#GUID-DFDC8E24-B911-4C42-B4B1-853E964D3644} 

Syntax 

![Description of uid.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/uid.gif)[ Description of the illustration uid.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/uid.md)

Purpose 

` UID ` returns an integer that uniquely identifies the session user (the user who logged on). 

> **note:** See Also: 

[ USER ](USER.md#GUID-AD0B927B-EFD4-4246-89B4-2D55AB3AF531) to learn how Oracle Database determines the session user 

Examples 

The following example returns the UID of the session user: 
    
    
    ```
    SELECT UID FROM DUAL;
    ```
