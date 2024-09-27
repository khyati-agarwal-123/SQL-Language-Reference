[Previous](Datetime-Expressions.md) [Next](Interval-Expressions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Expressions](Expressions.md)
  3. Function Expressions 

## Function Expressions

You can use any built-in SQL function or user-defined function as an
expression. Some valid built-in function expressions are:

    
    
    LENGTH('BLAKE') 
    ROUND(1234.567*43) 
    SYSDATE 

See Also:

[About SQL Functions](About-SQL-
Functions.md#GUID-D51AB228-518C-4213-8BD4-F919623D105E)' and [Aggregate
Functions](Aggregate-Functions.md#GUID-62BE676B-AF18-4E63-BD14-25206FEA0848)
for information on built-in functions

A user-defined function expression specifies a call to:

  * A function in an Oracle-supplied package (see [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS001)) 

  * A function in a user-defined package or type or in a standalone user-defined function (see [About User-Defined Functions](About-User-Defined-Functions.md#GUID-4EB3E236-8216-471C-BA44-23D87BDFEA67)) 

  * A user-defined function or operator (see [CREATE OPERATOR](CREATE-OPERATOR.md#GUID-62676C58-6F57-4572-8C09-7984A8E3EE9F), [CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306), and [Oracle Database Data Cartridge Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADDCI2100)) 

Some valid user-defined function expressions are:

    
    
    circle_area(radius)
    payroll.tax_rate(empno)
    hr.employees.comm_pct@remote(dependents, empno)
    DBMS_LOB.getlength(column_name)
    my_function(a_column)
    

In a user-defined function being used as an expression, positional, named, and
mixed notation are supported. For example, all of the following notations are
correct:

    
    
    CALL my_function(arg1 => 3, arg2 => 4) ...
    
    
    
    CALL my_function(3, 4) ...
    
    CALL my_function(3, arg2 => 4) ...

Restriction on User-Defined Function Expressions

You cannot pass arguments of object type or `XMLType` to remote functions and
procedures.


[← Previous](Datetime-Expressions.md)

[Next →](Interval-Expressions.md)
