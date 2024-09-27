[Previous](DISASSOCIATE-STATISTICS.md) [Next](DROP-ATTRIBUTE-DIMENSION.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. DROP ANALYTIC VIEW

## DROP ANALYTIC VIEW

Purpose

Use the `DROP` `ANALYTIC` `VIEW` statement to drop an analytic view. An
`ANALYTIC` `VIEW` object is a component of analytic views.

Prerequisites

To drop an analytic view in your own schema, you must have the `DROP`
`ANALYTIC` `VIEW` system privilege. To drop an analytic view in another user's
schema, you must have the `DROP` `ANY` `ANALYTIC` `VIEW` system privilege.

Syntax

drop_analytic_view::=

![Description of drop_analytic_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_analytic_view.gif)  
[Description of the illustration
drop_analytic_view.eps](img_text/drop_analytic_view.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema in which the analytic view exists. If you do not specify a
schema, then Oracle Database looks for the analytic view in your own schema.

analytic_view_name

Specify the name of the analytic view to drop.

Example

The following statement drops the specified analytic view object:

    
    
    DROP ANALYTIC VIEW sales_av;


[← Previous](DISASSOCIATE-STATISTICS.md)

[Next →](DROP-ATTRIBUTE-DIMENSION.md)
