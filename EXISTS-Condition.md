[Previous](BETWEEN-Condition.md) [Next](IN-Condition.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Conditions](Conditions.md)
  3. EXISTS Condition 

## EXISTS Condition

An `EXISTS` condition tests for existence of rows in a subquery.

![Description of exists_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/exists_condition.gif)  
[Description of the illustration
exists_condition.eps](img_text/exists_condition.md)

[Table 6-11](EXISTS-
Condition.md#GUID-20259A83-C42B-4E0D-8DF4-9A2A66ACA8E7__CJADBJFF "The first
column lists the single EXISTS condition, the second describes its operation,
and the third provides an example.") shows the `EXISTS` condition.

Table 6-11 EXISTS Condition

Type of Condition | Operation | Example  
---|---|---  
      
    
    EXISTS 

|  `TRUE` if a subquery returns at least one row.  | 
    
    
    SELECT department_id
      FROM departments d
      WHERE EXISTS
      (SELECT * FROM employees e
        WHERE d.department_id 
        = e.department_id)
       ORDER BY department_id;


[← Previous](BETWEEN-Condition.md)

[Next →](IN-Condition.md)
