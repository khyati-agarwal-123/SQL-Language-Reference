[Previous](ALTER-ANALYTIC-VIEW.md) [Next](ALTER-AUDIT-POLICY-Unified-
Auditing.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER ATTRIBUTE DIMENSION

## ALTER ATTRIBUTE DIMENSION

Purpose

Use the `ALTER` `ATTRIBUTE` `DIMENSION` statement to rename or compile an
attribute dimension. For other alterations, use `CREATE` `OR` `REPLACE`
`ATTRIBUTE` `DIMENSION`.

Prerequisites

To alter an attribute dimension in your own schema, you must have the `ALTER`
`ATTRIBUTE` `DIMENSION` system privilege. To alter an attribute dimension in
another user's schema, you must have the `ALTER` `ANY` `ATTRIBUTE` `DIMENSION`
system privilege or have been granted `ALTER` on the attribute dimension
directly.

Syntax

alter_attribute_dimension::=

![Description of alter_attribute_dimension.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_attribute_dimension.gif)  
[Description of the illustration
alter_attribute_dimension.eps](img_text/alter_attribute_dimension.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema in which the attribute dimension exists. If you do not
specify a schema, then Oracle Database looks for the attribute dimension in
your own schema.

attr_dim_name

Specify the name of the attribute dimension.

RENAME TO

Specify `RENAME` `TO` to change the name of the attribute dimension. For
`new_attr_dim_name`, specify a new name for the attribute dimension.

COMPILE

Specify `COMPILE` to compile the attribute dimension.

Example

The following statement changes the name of an attribute dimension:

    
    
    ALTER ATTRIBUTE DIMENSION product_attr_dim RENAME TO my_product_attr_dim;


[← Previous](ALTER-ANALYTIC-VIEW.md)

[Next →](ALTER-AUDIT-POLICY-Unified-Auditing.md)
