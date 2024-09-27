[Previous](About-Queries-and-Subqueries.md) [Next](Hierarchical-
Queries.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Queries and Subqueries](SQL-Queries-and-Subqueries.md)
  3. Creating Simple Queries 

## Creating Simple Queries

The list of expressions that appears after the `SELECT` keyword and before the
`FROM` clause is called the select list. Within the select list, you specify
one or more columns in the set of rows you want Oracle Database to return from
one or more tables, views, or materialized views. The number of columns, as
well as their data type and length, are determined by the elements of the
select list.

If two or more tables have some column names in common, then you must qualify
column names with names of tables. Otherwise, fully qualified column names are
optional. However, it is always a good idea to qualify table and column
references explicitly. Oracle often does less work with fully qualified table
and column names.

You can use a column alias, `c_alias`, to label the immediately preceding
expression in the select list so that the column is displayed with a new
heading. The alias effectively renames the select list item for the duration
of the query. The alias can be used in the `ORDER` `BY` clause, but not other
clauses in the query.

You can use comments in a `SELECT` statement to pass instructions, or hints,
to the Oracle Database optimizer. The optimizer uses hints to choose an
execution plan for the statement. Refer to
"[Hints](Comments.md#GUID-D316D545-89E2-4D54-977F-FC97815CD62E)" for more
information on hints.


[← Previous](About-Queries-and-Subqueries.md)

[Next →](Hierarchical-Queries.md)
