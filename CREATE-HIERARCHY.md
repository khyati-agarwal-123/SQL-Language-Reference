[Previous](CREATE-FUNCTION.md) [Next](CREATE-INDEX.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE HIERARCHY

## CREATE HIERARCHY

Purpose

Use the `CREATE` `HIERARCHY` statement to create a hierarchy. A hierarchy
specifies the hierarchical relationships among the levels of an attribute
dimension.

Prerequisites

To create a hierarchy in your own schema, you must have the `CREATE`
`HIERARCHY` system privilege. To create a hierarchy in another user's schema,
you must have the `CREATE` `ANY` `HIERARCHY` system privilege.

Syntax

create_hierarchy::=

![Description of create_hierarchy.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_hierarchy.gif)  
[Description of the illustration
create_hierarchy.eps](img_text/create_hierarchy.md)

classification_clause::=

![Description of classification_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/classification_clause.gif)  
[Description of the illustration
classification_clause.eps](img_text/classification_clause.md)

hier_using_clause::=

![Description of hier_using_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/hier_using_clause.gif)  
[Description of the illustration
hier_using_clause.eps](img_text/hier_using_clause.md)

level_hier_clause::=

![Description of level_hier_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/level_hier_clause.gif)  
[Description of the illustration
level_hier_clause.eps](img_text/level_hier_clause.md)

hier_attrs_clause::=

![Description of hier_attrs_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/hier_attrs_clause.gif)  
[Description of the illustration
hier_attrs_clause.eps](img_text/hier_attrs_clause.md)

hier_attr_clause::=

![Description of hier_attr_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/hier_attr_clause.gif)  
[Description of the illustration
hier_attr_clause.eps](img_text/hier_attr_clause.md)

hier_attr_name::=

![Description of hier_attr_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/hier_attr_name.gif)  
[Description of the illustration
hier_attr_name.eps](img_text/hier_attr_name.md)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to replace an existing definition of a hierarchy with a
different definition.

FORCE and NOFORCE

Specify `FORCE` to force the creation of the hierarchy even if it does not
successfully compile. If you specify `NOFORCE`, then the hierarchy must
compile successfully, otherwise an error occurs. The default is `NOFORCE`.

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the hierarchy does not exist, a new hierarchy is created at the end of the statement.

  * If the hierarchy exists, this is the hierarchy you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

schema

Specify the schema in which to create the hierarchy. If you do not specify a
schema, then Oracle Database creates the hierarchy in your own schema.

hierarchy

Specify a name for the hierarchy.

SHARING

Use the sharing clause if you want to create the object in an application root
in the context of an application maintenance. This type of object is called an
application common object and it can be shared with the application PDBs that
belong to the application root.

You can specify how the object is shared using one of the following sharing
attributes:

  * `METADATA` \- A metadata link shares the metadata, but its data is unique to each container. This type of object is referred to as a metadata-linked application common object. 

  * `NONE` \- The object is not shared and can only be accessed in the application root. 

classification_clause

Use the classification clause to specify values for the `CAPTION` or
`DESCRIPTION` classifications and to specify user-defined classifications.
Classifications provide descriptive metadata that applications may use to
provide information about analytic views and their components.

You may specify any number of classifications for the same object. A
classification can have a maximum length of 4000 bytes.

For the `CAPTION` and `DESCRIPTION` classifications, you may use the DDL
shortcuts `CAPTION` `'``caption``'` and `DESCRIPTION` `'``description``'` or
the full classification syntax.

You may vary the classification values by language. To specify a language for
the `CAPTION` or `DESCRIPTION` classification, you must use the full syntax.
If you do not specify a language, then the language value for the
classification is `NULL`. The language value must either be `NULL` or a valid
`NLS_LANGUAGE` value.

hier_using_clause

Specify the attribute dimension that has the members of the hierarchy.

level_hier_clause

Specify the organization of the hierarchy levels.

hier_attrs_clause

Specify classifications that contain descriptive metadata for the hierarchical
attributes. A `hier_attr_clause` for a given `hier_attr_name` may appear only
once in the list.

All hierarchies always contain all of the hierarchical attributes, but a
hierarchical attribute does not have descriptive metadata associated with it
unless you specify it with this clause.

hier_attr_clause

Specify a hierarchical attribute and provide one or more classifications for
it.

hier_attr_name

Specify a hierarchical attribute.

Examples

The following example creates the `TIME_HIER` hierarchy:

    
    
    CREATE OR REPLACE HIERARCHY time_hier  -- Hierarchy name
    USING time_attr_dim               -- Refers to TIME_ATTR_DIM attribute dimension
     (month CHILD OF                  -- Months in the attribute dimension
     quarter CHILD OF
     year);

The following example creates the `PRODUCT_HIER` hierarchy:

    
    
    CREATE OR REPLACE HIERARCHY product_hier
    USING product_attr_dim
     (category
      CHILD OF department);

The following example creates the `GEOGRAPHY_HIER` hierarchy:

    
    
    CREATE OR REPLACE HIERARCHY geography_hier
    USING geography_attr_dim
     (state_province
      CHILD OF country
      CHILD OF region);


[← Previous](CREATE-FUNCTION.md)

[Next →](CREATE-INDEX.md)
