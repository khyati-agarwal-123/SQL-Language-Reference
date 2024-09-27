[Previous](Unnesting-of-Nested-Subqueries.md) [Next](Distributed-
Queries.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Queries and Subqueries](SQL-Queries-and-Subqueries.md)
  3. Selecting from the DUAL Table 

## Selecting from the DUAL Table

`DUAL` is a table automatically created by Oracle Database along with the data
dictionary. `DUAL` is in the schema of the user `SYS` but is accessible by the
name `DUAL` to all users. It has one column, `DUMMY`, defined to be
`VARCHAR2(1)`, and contains one row with a value `X`. Selecting from the
`DUAL` table is useful for computing a constant expression with the `SELECT`
statement. Because `DUAL` has only one row, the constant is returned only
once. Alternatively, you can select a constant, pseudocolumn, or expression
from any table, but the value will be returned as many times as there are rows
in the table. Refer to "[About SQL Functions](About-SQL-
Functions.md#GUID-D51AB228-518C-4213-8BD4-F919623D105E)" for many examples
of selecting a constant value from `DUAL`.

Beginning with Oracle Database Release 23, it is now optional to select
expressions using the `FROM DUAL` clause.

Note:

Beginning with Oracle Database 10g Release 1, logical I/O is not performed on
the `DUAL` table when computing an expression that does not include the
`DUMMY` column. This optimization is listed as `FAST` `DUAL` in the execution
plan. If you `SELECT` the `DUMMY` column from `DUAL`, then this optimization
does not take place and logical I/O occurs.


[← Previous](Unnesting-of-Nested-Subqueries.md)

[Next →](Distributed-Queries.md)
