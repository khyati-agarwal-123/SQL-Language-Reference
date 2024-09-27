[Previous](CREATE-DATABASE-LINK.md) [Next](CREATE-DIRECTORY.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE DIMENSION 

## CREATE DIMENSION

Purpose

Use the `CREATE` `DIMENSION` statement to create a dimension. A dimension
defines a parent-child relationship between pairs of column sets, where all
the columns of a column set must come from the same table. However, columns in
one column set (called a level) can come from a different table than columns
in another set. The optimizer uses these relationships with materialized views
to perform query rewrite. The SQL Access Advisor uses these relationships to
recommend creation of specific materialized views.

Note:

Oracle Database does not automatically validate the relationships you declare
when creating a dimension. To validate the relationships specified in the
`hierarchy_clause` and the `dimension_join_clause` of `CREATE` `DIMENSION`,
you must run the `DBMS_OLAP`.`VALIDATE_DIMENSION` procedure.

See Also:

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) for more information on materialized views 

  * [Oracle Database SQL Tuning Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=TGSQL591) for more information on query rewrite, the optimizer and the SQL Access Advisor 

Prerequisites

To create a dimension in your own schema, you must have the `CREATE`
`DIMENSION` system privilege. To create a dimension in another user's schema,
you must have the `CREATE` `ANY` `DIMENSION` system privilege. In either case,
you must have the `READ` or `SELECT` object privilege on any objects
referenced in the dimension.

Syntax

create_dimension::=

![Description of create_dimension.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_dimension.gif)  
[Description of the illustration
create_dimension.eps](img_text/create_dimension.md)

level_clause::=

![Description of level_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/level_clause.gif)  
[Description of the illustration level_clause.eps](img_text/level_clause.md)

hierarchy_clause::=

![Description of hierarchy_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/hierarchy_clause.gif)  
[Description of the illustration
hierarchy_clause.eps](img_text/hierarchy_clause.md)

dimension_join_clause::=

![Description of dimension_join_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dimension_join_clause.gif)  
[Description of the illustration
dimension_join_clause.eps](img_text/dimension_join_clause.md)

attribute_clause::=

![Description of attribute_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/attribute_clause.gif)  
[Description of the illustration
attribute_clause.eps](img_text/attribute_clause.md)

extended_attribute_clause::=

![Description of extended_attribute_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/extended_attribute_clause.gif)  
[Description of the illustration
extended_attribute_clause.eps](img_text/extended_attribute_clause.md)

Semantics

schema

Specify the schema in which the dimension will be created. If you do not
specify `schema`, then Oracle Database creates the dimension in your own
schema.

dimension

Specify the name of the dimension. The name must satisfy the requirements
listed in "[Database Object Naming Rules](Database-Object-Names-and-
Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

level_clause

The `level_clause` defines a level in the dimension. A level defines dimension
hierarchies and attributes.

level

Specify the name of the level.

level_table . level_column

Specify the columns in the level. You can specify up to 32 columns. The tables
you specify in this clause must already exist.

SKIP WHEN NULL

Specify this clause to indicate that if the specified level is `NULL`, then
the level is to be skipped. This clause lets you preserve the hierarchical
chain of parent-child relationship by an alternative path that skips over the
specified level. See [hierarchy_clause](CREATE-
DIMENSION.md#GUID-E6CD4CFC-5D06-4A8F-9DF1-C609A7EB8413__I2061857).

Restrictions on Dimension Level Columns

Dimension level columns are subject to the following restrictions:

  * All of the columns in a level must come from the same table.

  * If columns in different levels come from different tables, then you must specify the `dimension_join_clause`. 

  * The set of columns you specify must be unique to this level.

  * The columns you specify cannot be specified in any other dimension.

  * Each `level_column` must be non-null unless the level is specified with `SKIP` `WHEN` `NULL`. The non-null columns need not have `NOT` `NULL` constraints. The column for which you specify `SKIP` `WHEN` `NULL` cannot have a `NOT` `NULL` constraint). 

hierarchy_clause

The `hierarchy_clause` defines a linear hierarchy of levels in the dimension.
Each hierarchy forms a chain of parent-child relationships among the levels in
the dimension. Hierarchies in a dimension are independent of each other. They
may, but need not, have columns in common.

Each level in the dimension should be specified at most once in this clause,
and each level must already have been named in the `level_clause.`

hierarchy

Specify the name of the hierarchy. This name must be unique in the dimension.

child_level

Specify the name of a level that has an n:1 relationship with a parent level.
The `level_columns` of `child_level` cannot be null, and each `child_level`
value uniquely determines the value of the next named `parent_level`.

If the child `level_table` is different from the parent `level_table`, then
you must specify a join relationship between them in the
`dimension_join_clause`.

parent_level

Specify the name of a level.

dimension_join_clause

The `dimension_join_clause` lets you specify an inner equijoin relationship
for a dimension whose columns are contained in multiple tables. This clause is
required and permitted only when the columns specified in the hierarchy are
not all in the same table.

child_key_column

Specify one or more columns that are join-compatible with columns in the
parent level.

If you do not specify the schema and table of each `child_column`, then the
schema and table are inferred from the `CHILD` `OF` relationship in the
`hierarchy_clause`. If you do specify the schema and column of a
`child_key_column`, then the schema and table must match the schema and table
of columns in the child of `parent_level` in the `hierarchy_clause`.

parent_level

Specify the name of a level.

Restrictions on Join Dimensions

Join dimensions are subject to the following restrictions:

  * You can specify only one `dimension_join_clause` for a given pair of levels in the same hierarchy. 

  * The `child_key_columns` must be non-null, and the parent key must be unique and non-null. You need not define constraints to enforce these conditions, but queries may return incorrect results if these conditions are not true. 

  * Each child key must join with a key in the `parent_level` table. 

  * Self-joins are not permitted. The `child_key_columns` cannot be in the same table as `parent_level`. 

  * All of the child key columns must come from the same table. 

  * The number of child key columns must match the number of columns in `parent_level`, and the columns must be joinable. 

  * You cannot specify multiple child key columns unless the parent level consists of multiple columns.

attribute_clause

The `attribute_clause` lets you specify the columns that are uniquely
determined by a hierarchy level. The columns in `level` must all come from the
same table as the `dependent_columns`. The `dependent_columns` need not have
been specified in the `level_clause`.

For example, if the hierarchy levels are `city`, `state`, and `country`, then
`city` might determine `mayor`, `state` might determine `governor`, and
`country` might determine `president`.

extended_attribute_clause

This clause lets you specify an attribute name for one or more level-to-column
relations. The type of attribute you create with this clause is not different
from the type of attribute created using the `attribute_clause`. The only
difference is that this clause lets you assign a name to the attribute that is
different from the level name.

Examples

Creating a Dimension: Examples

This statement was used to create the `customers_dim` dimension in the sample
schema `sh`:

    
    
    CREATE DIMENSION customers_dim 
       LEVEL customer   IS (customers.cust_id)
       LEVEL city       IS (customers.cust_city) 
       LEVEL state      IS (customers.cust_state_province) 
       LEVEL country    IS (countries.country_id) 
       LEVEL subregion  IS (countries.country_subregion) 
       LEVEL region     IS (countries.country_region) 
       HIERARCHY geog_rollup (
          customer      CHILD OF
          city          CHILD OF 
          state         CHILD OF 
          country       CHILD OF 
          subregion     CHILD OF 
          region 
       JOIN KEY (customers.country_id) REFERENCES country
       )
       ATTRIBUTE customer DETERMINES
       (cust_first_name, cust_last_name, cust_gender, 
        cust_marital_status, cust_year_of_birth, 
        cust_income_level, cust_credit_limit) 
       ATTRIBUTE country DETERMINES (countries.country_name)
    ;

Creating a Dimension with Extended Attributes: Example

Alternatively, the `extended_attribute_clause` could have been used instead of
the `attribute_clause`, as shown in the following example:

    
    
    CREATE DIMENSION customers_dim 
       LEVEL customer   IS (customers.cust_id)
       LEVEL city       IS (customers.cust_city) 
       LEVEL state      IS (customers.cust_state_province) 
       LEVEL country    IS (countries.country_id) 
       LEVEL subregion  IS (countries.country_subregion) 
       LEVEL region     IS (countries.country_region) 
       HIERARCHY geog_rollup (
          customer      CHILD OF
          city          CHILD OF 
          state         CHILD OF 
          country       CHILD OF 
          subregion     CHILD OF 
          region 
       JOIN KEY (customers.country_id) REFERENCES country
       )
       ATTRIBUTE customer_info LEVEL customer DETERMINES
       (cust_first_name, cust_last_name, cust_gender, 
        cust_marital_status, cust_year_of_birth, 
        cust_income_level, cust_credit_limit) 
       ATTRIBUTE country DETERMINES (countries.country_name);

Creating a Dimension with NULL Column Values: Example

The following example shows how to create the dimension if one of the level
columns is null and you want to preserve the hierarchical chain. The example
uses the `cust_marital_status` column for simplicity because it is not a `NOT`
`NULL` column. If it had such a constraint, then you would have to disable the
constraint before using the `SKIP` `WHEN` `NULL` clause.

    
    
    CREATE DIMENSION customers_dim
       LEVEL customer IS (customers.cust_id)
       LEVEL status IS (customers.cust_marital_status) SKIP WHEN NULL
       LEVEL city IS (customers.cust_city)
       LEVEL state IS (customers.cust_state_province)
       LEVEL country IS (countries.country_id)
       LEVEL subregion IS (countries.country_subregion) SKIP WHEN NULL
       LEVEL region IS (countries.country_region)
       HIERARCHY geog_rollup (
          customer CHILD OF
          city CHILD OF
          state CHILD OF
          country CHILD OF
          subregion CHILD OF
          region
       JOIN KEY (customers.country_id) REFERENCES country
       )
       ATTRIBUTE customer DETERMINES
       (cust_first_name, cust_last_name, cust_gender,
        cust_marital_status, cust_year_of_birth,
        cust_income_level, cust_credit_limit)
       ATTRIBUTE country DETERMINES (countries.country_name)
    ;


[← Previous](CREATE-DATABASE-LINK.md)

[Next →](CREATE-DIRECTORY.md)
