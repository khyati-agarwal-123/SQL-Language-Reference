[Previous](Comparison-Conditions.md) [Next](Logical-Conditions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Conditions](Conditions.md)
  3. Floating-Point Conditions 

## Floating-Point Conditions

The floating-point conditions let you determine whether an expression is
infinite or is the undefined result of an operation (is not a number or
`NaN`).

floating_point_condition::=

![Description of floating_point_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/floating_point_condition.gif)  
[Description of the illustration
floating_point_condition.eps](img_text/floating_point_condition.md)

In both forms of floating-point condition, `expr` must resolve to a numeric
data type or to any data type that can be implicitly converted to a numeric
data type. [Table 6-3](Floating-Point-
Conditions.md#GUID-D7707649-2C93-4553-BF78-F461F17A634E__CJAFFCAE "The first
column lists the floating-point condition, the second column describes what
the condition does, and the third column provides an example.") describes the
floating-point conditions.

Table 6-3 Floating-Point Conditions

Type of Condition | Operation | Example  
---|---|---  
      
    
    IS [NOT] NAN

|  Returns `TRUE` if `expr` is the special value `NaN` when `NOT` is not specified. Returns `TRUE` if `expr` is not the special value `NaN` when `NOT` is specified.  | 
    
    
    SELECT COUNT(*) FROM employees
      WHERE commission_pct IS NOT NAN;  
      
    
    IS [NOT] INFINITE

|  Returns `TRUE` if `expr` is the special value +`INF` or -`INF` when `NOT` is not specified. Returns `TRUE` if `expr` is neither +`INF` nor -`INF` when `NOT` is specified.  | 
    
    
    SELECT last_name FROM employees
      WHERE salary IS NOT INFINITE;  
  
See Also:

  * [Floating-Point Numbers](Data-Types.md#GUID-F579F4B8-EF13-4CAF-9B06-03B076861C41) for more information on the Oracle implementation of floating-point numbers 

  * [Implicit Data Conversion](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694) for more information on how Oracle converts floating-point data types 


[← Previous](Comparison-Conditions.md)

[Next →](Logical-Conditions.md)
