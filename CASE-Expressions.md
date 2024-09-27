[Previous](Compound-Expressions.md) [Next](Column-Expressions.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Expressions](Expressions.md)
  3. CASE Expressions 

## CASE Expressions

`CASE` expressions let you use `IF` ... `THEN` ... `ELSE` logic in SQL
statements without having to invoke procedures. The syntax is:

![Description of case_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/case_expression.gif)  
[Description of the illustration
case_expression.eps](img_text/case_expression.md)

simple_case_expression::=

![Description of simple_case_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/simple_case_expression.gif)  
[Description of the illustration
simple_case_expression.eps](img_text/simple_case_expression.md)

searched_case_expression::=

![Description of searched_case_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/searched_case_expression.gif)  
[Description of the illustration
searched_case_expression.eps](img_text/searched_case_expression.md)

else_clause::=

![Description of else_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/else_clause.gif)  
[Description of the illustration else_clause.eps](img_text/else_clause.md)

In a simple `CASE` expression, Oracle Database searches for the first `WHEN`
... `THEN` pair for which `expr` is equal to `comparison_expr` and returns
`return_expr`. If none of the `WHEN` ... `THEN` pairs meet this condition, and
an `ELSE` clause exists, then Oracle returns `else_expr`. Otherwise, Oracle
returns null.

In a searched `CASE` expression, Oracle searches from left to right until it
finds an occurrence of `condition` that is true, and then returns
`return_expr`. If no `condition` is found to be true, and an `ELSE` clause
exists, then Oracle returns `else_expr`. Otherwise, Oracle returns null.

Oracle Database uses short-circuit evaluation. For a simple `CASE` expression,
the database evaluates each `comparison_expr` value only before comparing it
to `expr`, rather than evaluating all `comparison_expr` values before
comparing any of them with `expr`. Consequently, Oracle never evaluates a
`comparison_expr` if a previous `comparison_expr` is equal to `expr`. For a
searched `CASE` expression, the database evaluates each `condition` to
determine whether it is true, and never evaluates a `condition` if the
previous `condition` was true.

For a simple `CASE` expression, the `expr` and all `comparison_expr` values
must either have the same data type (`CHAR`, `VARCHAR2`, `NCHAR`, or
`NVARCHAR2`, `NUMBER`, `BINARY_FLOAT`, or `BINARY_DOUBLE`) or must all have a
numeric data type. If all expressions have a numeric data type, then Oracle
determines the argument with the highest numeric precedence, implicitly
converts the remaining arguments to that data type, and returns that data
type.

For both simple and searched `CASE` expressions, all of the `return_expr`s
must either have the same data type (`CHAR`, `VARCHAR2`, `NCHAR`, or
`NVARCHAR2`, `NUMBER`, `BINARY_FLOAT`, or `BINARY_DOUBLE`) or must all have a
numeric data type. If all return expressions have a numeric data type, then
Oracle determines the argument with the highest numeric precedence, implicitly
converts the remaining arguments to that data type, and returns that data
type.

The maximum number of arguments in a `CASE` expression is 65535. All
expressions count toward this limit, including the initial expression of a
simple `CASE` expression and the optional `ELSE` expression. Each `WHEN` ...
`THEN` pair counts as two arguments. To avoid exceeding this limit, you can
nest `CASE` expressions so that the `return_expr` itself is a `CASE`
expression.

The comparison performed by the simple `CASE` expression is collation-
sensitive if the compared arguments have a character data type (`CHAR`,
`VARCHAR2`, `NCHAR`, or `NVARCHAR2`). The collation determination rules
determine the collation to use.

See Also:

  * [Table 2-9](Data-Type-Comparison-Rules.md#GUID-98BE3A78-6E33-4181-B5CB-D96FD9DC1694__G195937 "An X in a cell indicates implicit conversion of the data types") for more information on implicit conversion 

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation derivation and determination rules for the `CASE` expression 

  * [Numeric Precedence](Data-Types.md#GUID-4C0B65DB-E751-4957-A1ED-5044BAFA7812) for information on numeric precedence 

  * [COALESCE](COALESCE.md#GUID-3F9007A7-C0CA-4707-9CBA-1DBF2CDE0C87) and [NULLIF](NULLIF.md#GUID-445FC268-7FFA-4850-98C9-D53D88AB2405) for alternative forms of `CASE` logic 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG02012) for examples using various forms of the `CASE` expression 

Simple CASE Example

For each customer in the sample `oe.customers` table, the following statement
lists the credit limit as "Low" if it equals $100, "High" if it equals $5000,
and "Medium" if it equals anything else.

    
    
    SELECT cust_last_name,
       CASE credit_limit WHEN 100 THEN 'Low'
       WHEN 5000 THEN 'High'
       ELSE 'Medium' END AS credit
       FROM customers
       ORDER BY cust_last_name, credit;
    
    CUST_LAST_NAME       CREDIT
    -------------------- ------
    Adjani               Medium
    Adjani               Medium
    Alexander            Medium
    Alexander            Medium
    Altman               High
    Altman               Medium
    . . .

Searched CASE Example

The following statement finds the average salary of the employees in the
sample table `oe.employees`, using $2000 as the lowest salary possible:

    
    
    SELECT AVG(CASE WHEN e.salary > 2000 THEN e.salary
       ELSE 2000 END) "Average Salary" FROM employees e;
    
    Average Salary
    --------------
        6461.68224


[← Previous](Compound-Expressions.md)

[Next →](Column-Expressions.md)
