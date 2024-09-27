[Previous](About-SQL-Expressions.md) [Next](analytic-view-measure-
expressions.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Expressions](Expressions.md)
  3. Simple Expressions 

## Simple Expressions

A simple expression specifies a column, pseudocolumn, constant, sequence
number, or null.

simple_expression::=

![Description of simple_expression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/simple_expression.gif)  
[Description of the illustration
simple_expression.eps](img_text/simple_expression.md)

In addition to the schema of a user, `schema` can also be "`PUBLIC`" (double
quotation marks required), in which case it must qualify a public synonym for
a table, view, or materialized view. Qualifying a public synonym with
"`PUBLIC`" is supported only in data manipulation language (DML) statements,
not data definition language (DDL) statements.

You can specify `ROWID` only with a table, not with a view or materialized
view. `NCHAR` and `NVARCHAR2` are not valid pseudocolumn data types.

See Also:

[Pseudocolumns](Pseudocolumns.md#GUID-6C65C788-76AA-4A51-B011-51D53DD2521D)
for more information on pseudocolumns and
[subquery_factoring_clause](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2077142) for information on
`query_name`

Some valid simple expressions are:

    
    
    employees.last_name 
    'this is a text string'
    10 
    N'this is an NCHAR string'


[← Previous](About-SQL-Expressions.md)

[Next →](analytic-view-measure-expressions.md)
