##  EXISTS Condition {#GUID-20259A83-C42B-4E0D-8DF4-9A2A66ACA8E7} 

An ` EXISTS ` condition tests for existence of rows in a subquery. 

![Description of exists_condition.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/exists_condition.gif)[ Description of the illustration exists_condition.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/exists_condition.md)[ Table 6-11 ](EXISTS-Condition.md#GUID-20259A83-C42B-4E0D-8DF4-9A2A66ACA8E7__CJADBJFF) shows the ` EXISTS ` condition. 

**Table: EXISTS Condition ** 

Type of Condition  |  Operation  |  Example   
---|---|---  
      
    
    ```
    EXISTS 
    ```

|  ` TRUE ` if a subquery returns at least one row.  | 
    
    
    ```
    SELECT department_id
      FROM departments d
      WHERE EXISTS
      (SELECT * FROM employees e
        WHERE d.department_id 
        = e.department_id)
       ORDER BY department_id;
    ```
