[Previous](DROP-FUNCTION.md) [Next](DROP-INDEX.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP HIERARCHY

## DROP HIERARCHY

Purpose

Use the `DROP` `HIERARCHY` statement to drop a hierarchy. A `HIERARCHY` object
is a component of analytic views.

Prerequisites

To drop a hierarchy in your own schema, you must have the `DROP` `HIERARCHY`
system privilege. To drop a hierarchy in another user's schema, you must have
the `DROP` `ANY` `HIERARCHY` system privilege.

Syntax

drop_hierarchy::=

![Description of drop_hierarchy.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_hierarchy.gif)  
[Description of the illustration
drop_hierarchy.eps](img_text/drop_hierarchy.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema in which the hierarchy exists. If you do not specify a
schema, then Oracle Database looks for the hierarchy in your own schema.

hierarchy_name

Specify the name of the hierarchy to drop.

Example

The following statement drops the specified hierarchy object:

    
    
    DROP HIERARCHY product_hier;


[← Previous](DROP-FUNCTION.md)

[Next →](DROP-INDEX.md)
