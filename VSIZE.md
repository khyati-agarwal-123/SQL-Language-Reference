##  VSIZE {#GUID-CDDB2A17-9398-4AF8-96FB-4297DDA2665B} 

Syntax 

![Description of vsize.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vsize.gif)[ Description of the illustration vsize.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/vsize.md)

Purpose 

` VSIZE ` returns the number of bytes in the internal representation of *expr* . If *expr* is null, then this function returns null. 

This function does not support ` CLOB ` data directly. However, ` CLOB ` s can be passed in as arguments through implicit data conversion. 

> **note:** See Also: 

" [ Data Type Comparison Rules ](Data-Type-Comparison-Rules.md#GUID-1563C817-86BF-430B-99AB-322EE2E29187) "  for more information 

Examples 

The following example returns the number of bytes in the ` last_name ` column of the employees in department 10: 
    
    
    ```
    SELECT last_name, VSIZE (last_name) "BYTES"      
      FROM employees
      WHERE department_id = 10
      ORDER BY employee_id;
     
    LAST_NAME            BYTES
    --------------- ----------
    Whalen                   6
    ```
