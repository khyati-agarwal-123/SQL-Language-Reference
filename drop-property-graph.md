[Previous](DROP-PROFILE.md) [Next](DROP-RESTORE-POINT.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP PROPERTY GRAPH

## DROP PROPERTY GRAPH

Purpose

You can drop property graphs with `DROP PROPERTY GRAPH`.

Prerequistes

Like tables and views, you can drop a property graph in your own schema. To
drop a property graph in any schema except `SYS` and `AUDSYS`, you must have
the `DROP ANY PROPERTY GRAPH` privilege.

Syntax

drop_property_graph::=

  

![Description of drop_property_graph.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_property_graph.gif)  
[Description of the illustration
drop_property_graph.eps](img_text/drop_property_graph.md)

  

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing property graph.

If you specify `IF NOT EXISTS` with `DROP`, the command fails with the error
message: `Incorrect IF EXISTS clause for ALTER/DROP statement`.


[← Previous](DROP-PROFILE.md)

[Next →](DROP-RESTORE-POINT.md)
