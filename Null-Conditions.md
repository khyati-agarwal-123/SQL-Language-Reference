##  Null Conditions {#GUID-657F2BA6-5687-4A00-8C2F-57515FD2DAEB} 

A ` NULL ` condition tests for nulls. This is the only condition that you should use to test for nulls. 

*null_condition* ::= 

![Description of null_condition.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/null_condition.gif)[ Description of the illustration null_condition.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/null_condition.md)[ Table 6-9 ](Null-Conditions.md#GUID-657F2BA6-5687-4A00-8C2F-57515FD2DAEB__CJAFCIGE) lists the null conditions. 

**Table: Null Condition ** 

Type of Condition  |  Operation  |  Example   
---|---|---  
      
    
    ```
    IS [NOT] NULL 
    ```

|  Tests for nulls.  See Also:  [ Nulls ](Nulls.md#GUID-B0BA4751-9D88-426A-84AD-BCDBD5584071) | 
    
    
    ```
    SELECT last_name
      FROM employees
      WHERE commission_pct
      IS NULL
      ORDER BY last_name;
    ```
