[Previous](Selecting-from-the-DUAL-Table.md) [Next](SQL-Statements-
ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md) JavaScript must be enabled to
correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Queries and Subqueries](SQL-Queries-and-Subqueries.md)
  3. Distributed Queries 

## Distributed Queries

The Oracle distributed database management system architecture lets you access
data in remote databases using Oracle Net and an Oracle Database server. You
can identify a remote table, view, or materialized view by appending @`dblink`
to the end of its name. The `dblink` must be a complete or partial name for a
database link to the database containing the remote table, view, or
materialized view.

See Also:

[References to Objects in Remote Databases](Syntax-for-Schema-Objects-and-
Parts-in-SQL-Statements.md#GUID-61D0B206-A5EA-473F-AD04-7067D6E3914C) for
more information on referring to database links

Restrictions on Distributed Queries

Distributed queries are currently subject to the restriction that all tables
locked by a `FOR` `UPDATE` clause and all tables with `LONG` columns selected
by the query must be located on the same database. In addition, Oracle
Database currently does not support distributed queries that select user-
defined types or object `REF` data types on remote tables.


[← Previous](Selecting-from-the-DUAL-Table.md)

[Next →](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
