[Previous](DROP-ANALYTIC-VIEW.md) [Next](DROP-AUDIT-POLICY-Unified-
Auditing.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. DROP ATTRIBUTE DIMENSION

## DROP ATTRIBUTE DIMENSION

Purpose

Use the `DROP` `ATTRIBUTE` `DIMENSION` statement to drop an attribute
dimension. An `ATTRIBUTE` `DIMENSION` object is a component of analytic views.

Prerequisites

To drop an attribute dimension in your own schema, you must have the `DROP`
`ATTRIBUTE` `DIMENSION` system privilege. To drop an analytic view in another
user's schema, you must have the `DROP` `ANY` `ATTRIBUTE` `DIMENSION` system
privilege.

Syntax

drop_attribute_dimension::=

![Description of drop_attribute_dimension.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_attribute_dimension.gif)  
[Description of the illustration
drop_attribute_dimension.eps](img_text/drop_attribute_dimension.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema in which the attribute dimension exists. If you do not
specify a schema, then Oracle Database looks for the attribute dimension in
your own schema.

attr_dimension_name

Specify the name of the attribute dimension to drop.

Example

The following statement drops the specified attribute dimension object:

    
    
    DROP ATTRIBUTE DIMENSION product_attr_dim;


[← Previous](DROP-ANALYTIC-VIEW.md)

[Next →](DROP-AUDIT-POLICY-Unified-Auditing.md)
