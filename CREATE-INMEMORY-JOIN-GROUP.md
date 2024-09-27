[Previous](CREATE-INDEXTYPE.md) [Next](CREATE-JAVA.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE INMEMORY JOIN GROUP

## CREATE INMEMORY JOIN GROUP

Purpose

Use the `CREATE` `INMEMORY` `JOIN` `GROUP` statement to create a join group,
which is an object that specifies frequently joined columns from the same
table or different tables. Such columns typically contain values of compatible
data types that fall in similar ranges. When you create a join group, Oracle
Database stores special metadata for the columns in the global dictionary,
which enables the database to optimize join queries for the columns. In order
to achieve this optimization, the table columns must be populated in the In-
Memory Column Store (IM column store).

Creating a join group for tables causes the current In-Memory contents of
these tables to be invalidated. Subsequent repopulation causes the In-Memory
Compression Units (IMCUs) of the tables to be re-encoded with the global
dictionary. Thus, Oracle recommends that you first create the join group, and
then populate the tables.

See Also:

  * [ALTER INMEMORY JOIN GROUP](ALTER-INMEMORY-JOIN-GROUP.md#GUID-AF24F413-BB14-4B5D-93BF-9EB31ACFEBEC) and [DROP INMEMORY JOIN GROUP](DROP-INMEMORY-JOIN-GROUP.md#GUID-520D0E9A-B577-4BCD-B6CB-8EB448C0686D)

  * [Oracle Database In-Memory Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=INMEM-GUID-3E5491C4-B345-4A8E-8B1B-8DC150C8A797) for more information on join groups 

Prerequisites

To create a join group in another user's schema, or to include in the join
group a column in a table in another userâs schema, you must have the
`CREATE` `ANY` `TABLE` system privilege.

Syntax

create_inmemory_join_group::=

![Description of create_inmemory_join_group.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_inmemory_join_group.gif)  
[Description of the illustration
create_inmemory_join_group.eps](img_text/create_inmemory_join_group.md)

Semantics

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the object does not exist, a new obejct is created at the end of the statement.

  * If the object exists, this is the object you have at the end of the statement. A new one is not created because the older object is detected.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement.`

schema

Specify the schema to contain the join group. If you omit `schema`, then the
database creates the join group in your own schema.

join_group

Specify the name of the join group to be created. The name must satisfy the
requirements listed in â[Database Object Naming Rules](Database-Object-
Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)â.

schema

Specify the schema of the table that contains a column to be included in the
join group If you omit `schema`, then Oracle Database assumes the table is in
your own schema.

table

Specify the name of the table that contains a column to be included in the
join group.

column

Specify the name of a column to be included in the join group. A join group
can contain columns in the same table or different tables.

Restrictions on Join Groups

The following restrictions apply to join groups:

  * A join group must contain at least 1 column.

  * A join group can contain at most 255 columns.

  * A table column can be a member of at most one join group.

  * Oracle Active Data Guard does not support join groups.

Examples

The following statement creates a join group named `prod_id1` in the `oe`
schema. Both tables involved in this join group reside in the `oe` schema.

    
    
    CREATE INMEMORY JOIN GROUP prod_id1
      (inventories(product_id), order_items(product_id));

The following statement creates a join group named `prod_id2` in the `oe`
schema. The table `inventories` resides in the `oe` schema and the table
`online_media` resides in the `pm` schema.

    
    
    CREATE INMEMORY JOIN GROUP prod_id2
      (inventories(product_id), pm.online_media(product_id));
    


[← Previous](CREATE-INDEXTYPE.md)

[Next →](CREATE-JAVA.md)
