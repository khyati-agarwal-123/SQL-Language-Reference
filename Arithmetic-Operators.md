[Previous](About-SQL-Operators.md) [Next](COLLATE-Operator.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. Arithmetic Operators 

## Arithmetic Operators

You can use an arithmetic operator with one or two arguments to negate, add,
subtract, multiply, and divide numeric values. Some of these operators are
also used in datetime and interval arithmetic. The arguments to the operator
must resolve to numeric data types or to any data type that can be implicitly
converted to a numeric data type.

Unary arithmetic operators return the same data type as the numeric data type
of the argument. For binary arithmetic operators, Oracle determines the
argument with the highest numeric precedence, implicitly converts the
remaining arguments to that data type, and returns that data type. [Table
4-2](Arithmetic-Operators.md#GUID-46CD9FD8-FC94-44BA-
AA62-30A16063EAAE__G1040952 "The first column lists the arithmetic operators,
the second column describes them, and the third column provides examples.")
lists arithmetic operators.

See Also:

[Table 2-9](Data-Type-Comparison-
Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell
indicates implicit conversion of the data types") for more information on
implicit conversion, [Numeric Precedence](Data-
Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812) for information on
numeric precedence, and [Datetime/Interval Arithmetic](Data-
Types.md#GUID-E405BBC7-DA9A-4DF2-9F22-E60CB9EC0705)

Table 4-2 Arithmetic Operators

Operator | Purpose | Example  
---|---|---  
\+ - |  When these denote a positive or negative expression, they are unary operators. | 
    
    
    SELECT *
      FROM order_items
      WHERE quantity = -1
      ORDER BY order_id, 
        line_item_id, product_id;
    
    SELECT *
      FROM employees
      WHERE -salary < 0
      ORDER BY employee_id;  
  
\+ - |  When they add or subtract, they are binary operators. | 
    
    
    SELECT hire_date 
      FROM employees
      WHERE SYSDATE - hire_date > 365
      ORDER BY hire_date;  
  
* / |  Multiply, divide. These are binary operators. | 
    
    
    UPDATE employees
      SET salary = salary * 1.1;  
  
Do not use two consecutive minus signs (--) in arithmetic expressions to
indicate double negation or the subtraction of a negative value. The
characters -- are used to begin comments within SQL statements. You should
separate consecutive minus signs with a space or parentheses. Refer to
[Comments](Comments.md#GUID-79B6B8FD-2DD4-471E-B9E0-0C8D20B058F6) for more
information on comments within SQL statements.


[← Previous](About-SQL-Operators.md)

[Next →](COLLATE-Operator.md)
