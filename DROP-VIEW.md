[Previous](DROP-USER.md) [Next](EXPLAIN-PLAN.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: DROP TABLE to LOCK TABLE](SQL-Statements-DROP-TABLE-to-LOCK-TABLE.md)
  3. DROP VIEW 

## DROP VIEW

Purpose

Use the `DROP` `VIEW` statement to remove a view or an object view from the
database. You can change the definition of a view by dropping and re-creating
it.

See Also:

[CREATE VIEW](CREATE-VIEW.md#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30) and
[ALTER VIEW](ALTER-VIEW.md#GUID-0DEDE960-B481-4B55-8027-EA9E4C863625) for
information on creating and modifying a view

Prerequisites

The view must be in your own schema or you must have the `DROP` `ANY` `VIEW`
system privilege.

Syntax

drop_view::=

![Description of drop_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_view.gif)  
[Description of the illustration drop_view.eps](img_text/drop_view.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the view. If you omit `schema`, then Oracle
Database assumes the view is in your own schema.

view

Specify the name of the view to be dropped.

Oracle Database does not drop views, materialized views, and synonyms that are
dependent on the view but marks them `INVALID`. You can drop them or redefine
views and synonyms, or you can define other views in such a way that the
invalid views and synonyms become valid again.

If any subviews have been defined on `view`, then the database invalidates the
subviews as well. To determine whether the view has any subviews, query the
`SUPERVIEW_NAME` column of the `USER_`, `ALL_`, or `DBA_VIEWS` data dictionary
views.

See Also:

  * [CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6) and [CREATE SYNONYM](CREATE-SYNONYM.md#GUID-A806C82F-1171-478E-A910-F9C6C42739B2)

  * [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233) for information on revalidating invalid materialized views 

CASCADE CONSTRAINTS

Specify `CASCADE` `CONSTRAINTS` to drop all referential integrity constraints
that refer to primary and unique keys in the view to be dropped. If you omit
this clause, and such constraints exist, then the `DROP` statement fails.

Examples

Dropping a View: Example

The following statement drops the `emp_view` view, which was created in
"[Creating a View: Example](CREATE-
VIEW.md#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30__I2102873)":

    
    
    DROP VIEW emp_view; 


[← Previous](DROP-USER.md)

[Next →](EXPLAIN-PLAN.md)
