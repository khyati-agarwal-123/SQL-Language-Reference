[Previous](CREATE-ANALYTIC-VIEW.md) [Next](CREATE-AUDIT-POLICY-Unified-
Auditing.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE ATTRIBUTE DIMENSION

## CREATE ATTRIBUTE DIMENSION

Purpose

Use the `CREATE` `ATTRIBUTE` `DIMENSION` statement to create an attribute
dimension. An attribute dimension specifies dimension members for one or more
analytic view hierarchies. It specifies the data source it is using and the
members it includes. It specifies levels for its members and determines
attribute relationships between levels.

Prerequisites

To create an attribute dimension in your own schema, you must have the
`CREATE` `ATTRIBUTE` `DIMENSION` system privilege. To create an attribute
dimension in another user's schema, you must have the `CREATE` `ANY`
`ATTRIBUTE` `DIMENSION` system privilege.

Syntax

create_attribute_dimension::=

![Description of create_attribute_dimension.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_attribute_dimension.gif)  
[Description of the illustration
create_attribute_dimension.eps](img_text/create_attribute_dimension.md)

classification_clause::=

![Description of classification_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/classification_clause.gif)  
[Description of the illustration
classification_clause.eps](img_text/classification_clause.md)

attr_dim_using_clause::=

![Description of attr_dim_using_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/attr_dim_using_clause.gif)  
[Description of the illustration
attr_dim_using_clause.eps](img_text/attr_dim_using_clause.md)

source_clause::=

  

![Description of source_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/source_clause.gif)  
[Description of the illustration
source_clause.eps](img_text/source_clause.md)

  

join_path_clause::=

![Description of join_path_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/join_path_clause.gif)  
[Description of the illustration
join_path_clause.eps](img_text/join_path_clause.md)

join_condition::=

![Description of join_condition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/join_condition.gif)  
[Description of the illustration
join_condition.eps](img_text/join_condition.md)

join_condition_elem ::=

![Description of join_condition_elem.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/join_condition_elem.gif)  
[Description of the illustration
join_condition_elem.eps](img_text/join_condition_elem.md)

attributes_clause::=

![Description of attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/attributes_clause.gif)  
[Description of the illustration
attributes_clause.eps](img_text/attributes_clause.md)

attr_dim_attributes_clause::=

![Description of attr_dim_attribute_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/attr_dim_attribute_clause.gif)  
[Description of the illustration
attr_dim_attribute_clause.eps](img_text/attr_dim_attribute_clause.md)

attr_dim_level_clause::=

![Description of attr_dim_level_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/attr_dim_level_clause.gif)  
[Description of the illustration
attr_dim_level_clause.eps](img_text/attr_dim_level_clause.md)

key_clause::=

![Description of key_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/key_clause.gif)  
[Description of the illustration key_clause.eps](img_text/key_clause.md)

alternate_key_clause::=

![Description of alternate_key_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alternate_key_clause.gif)  
[Description of the illustration
alternate_key_clause.eps](img_text/alternate_key_clause.md)

dim_order_clause::=

![Description of dim_order_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dim_order_clause.gif)  
[Description of the illustration
dim_order_clause.eps](img_text/dim_order_clause.md)

all_clause::=

![Description of all_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/all_clause.gif)  
[Description of the illustration all_clause.eps](img_text/all_clause.md)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to replace an existing definition of an attribute
dimension with a different definition.

FORCE and NOFORCE

Specify `FORCE` to force the creation of the attribute dimension even if it
does not successfully compile. If you specify `NOFORCE`, then the attribute
dimension must compile successfully, otherwise an error occurs. The default is
`NOFORCE`.

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the attribute dimension does not exist, a new attribute dimension is created at the end of the statement.

  * If the attribute dimension exists, this is the attribute dimension you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

schema

Specify the schema in which to create the attribute dimension. If you do not
specify a schema, then Oracle Database creates the attribute dimension in your
own schema.

attr_dimension

Specify a name for the attribute dimension.

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

DIMENSION TYPE

An attribute dimension may be either a `STANDARD` or a `TIME` type. A
`STANDARD` type attribute dimension has `STANDARD` type levels. Each level of
a `TIME` type attribute dimension is one of the time types. The default
`DIMENSION TYPE` is `STANDARD`.

attr_dim_using_clause

Use this clause to declare the sources that you want to use to create the
attribute dimension.

source_clause

You may specify the following sources:

  * A table or a view.

  * An alias for the table or the view by using the `AS` keyword. 

  * A join path. Use join paths to specify joins when the attribute dimension uses tables organized in a snowflake schema.

REMOTE

Specify `REMOTE` on a given source to indicate that the source is backed by
remote data and should be optimized as remote data.

join_path_clause

The join path clause specifies a join condition between columns in different
tables. The name for the join path specified by the join_path_name argument
must be unique for each join path included in the `USING` clause.

join_condition

A join condition consists of one or more join condition elements; each
additional join condition element is included by an `AND` operation.

join_condition_element

In a join condition element, the column references on the left-hand-side must
come from a different table than the column references on the right-hand-side.

attributes_clause

Specify one or more `attr_dim_attribute_clause` clauses.

attr_dim_attribute_clause

Specify a column from the `attr_dim_using_clause` source. The attribute has
the name of the column unless you specify an alias using the `AS` keyword. You
may specify classifications for each attribute.

attr_dim_level_clause

Specify a level in the attribute dimension. A level specifies key and optional
alternate key attributes that provide the members of the level.

If the key attribute has no `NULL` values, then you may specify `NOT` `NULL`,
which is the default. If it does have one or more `NULL` values, then specify
`SKIP` `WHEN` `NULL`.

LEVEL TYPE

A `STANDARD` type attribute dimension has `STANDARD` type levels. You do not
need to specify a `LEVEL TYPE` for a `STANDARD` type attribute dimension.

In a `TIME` type attribute dimension, you must specify a level type. The type
of the level may be one of the time types. You must specify a time type even
if the values of the level members are not of that type. For example, you may
have a SEASON level with values that are the names of seasons. In defining the
level, you must specify any one of the time level types, such as `QUARTERS`.
An application may use the level type designations for whatever purpose it
chooses.

DETERMINES

With the `DETERMINES` keyword, you may specify other attributes of the
attribute dimension that this level determines. If an attribute has only one
value for each value of another attribute, then the value of the first
attribute determines the value of the other attribute. For example, the
QUARTER_ID attribute has only one value for each value of the MONTH_ID
attribute, so you can include the the QUARTER_ID attribute in the `DETERMINES`
phrase of the MONTHS level.

key_clause

Specify one or more attributes as the key for the level.

alternate_key_clause

Specify one or more attributes as the alternate key for the level.

dim_order_clause

Specify the ordering of the members of the level.

all_clause

Optionally specify `MEMBER` `NAME`, `MEMBER` `CAPTION`, and `MEMBER`
`DESCRIPTION` values for the implicit ALL level. By default, the `MEMBER`
`NAME` value is ALL.

Examples

The following example describes the TIME_DIM table:

    
    
    desc TIME_DIM
    
    Name              Null?   Type          
    ----------------- -----   ------------- 
    MONTH_ID                  VARCHAR2(10)  
    CATEGORY_ID               NUMBER(6)     
    STATE_PROVINCE_ID         VARCHAR2(120) 
    UNITS                     NUMBER(6)     
    SALES                     NUMBER(12,2)  
    YEAR_ID          NOT NULL VARCHAR2(30) 
    YEAR_NAME        NOT NULL VARCHAR2(40) 
    YEAR_END_DATE             DATE         
    QUARTER_ID       NOT NULL VARCHAR2(30) 
    QUARTER_NAME     NOT NULL VARCHAR2(40) 
    QUARTER_END_DATE          DATE         
    QUARTER_OF_YEAR           NUMBER       
    MONTH_ID         NOT NULL VARCHAR2(30) 
    MONTH_NAME       NOT NULL VARCHAR2(40) 
    MONTH_END_DATE            DATE         
    MONTH_OF_YEAR             NUMBER       
    MONTH_LONG_NAME           VARCHAR2(30) 
    SEASON                    VARCHAR2(10) 
    SEASON_ORDER              NUMBER(38)   
    MONTH_OF_QUARTER          NUMBER(38) 

The following example creates a `TIME` type attribute dimension, using columns
from the TIME_DIM table:

    
    
    CREATE OR REPLACE ATTRIBUTE DIMENSION time_attr_dim
    DIMENSION TYPE TIME
    USING time_dim
    ATTRIBUTES
     (year_id
       CLASSIFICATION caption VALUE 'YEAR_ID'
       CLASSIFICATION description VALUE 'YEAR ID',
      year_name
        CLASSIFICATION caption VALUE 'YEAR_NAME'
        CLASSIFICATION description VALUE 'Year',
      year_end_date
        CLASSIFICATION caption VALUE 'YEAR_END_DATE'
        CLASSIFICATION description VALUE 'Year End Date',
      quarter_id
        CLASSIFICATION caption VALUE 'QUARTER_ID'
        CLASSIFICATION description VALUE 'QUARTER ID',
      quarter_name
        CLASSIFICATION caption VALUE 'QUARTER_NAME'
        CLASSIFICATION description VALUE 'Quarter',
      quarter_end_date
        CLASSIFICATION caption VALUE 'QUARTER_END_DATE'
        CLASSIFICATION description VALUE 'Quarter End Date',
      quarter_of_year
        CLASSIFICATION caption VALUE 'QUARTER_OF_YEAR'
        CLASSIFICATION description VALUE 'Quarter of Year',    
      month_id
        CLASSIFICATION caption VALUE 'MONTH_ID'
        CLASSIFICATION description VALUE 'MONTH ID',
      month_name
        CLASSIFICATION caption VALUE 'MONTH_NAME'
        CLASSIFICATION description VALUE 'Month',
      month_long_name
        CLASSIFICATION caption VALUE 'MONTH_LONG_NAME'
        CLASSIFICATION description VALUE 'Month Long Name',
      month_end_date
        CLASSIFICATION caption VALUE 'MONTH_END_DATE'
        CLASSIFICATION description VALUE 'Month End Date',
      month_of_quarter
        CLASSIFICATION caption VALUE 'MONTH_OF_QUARTER'
        CLASSIFICATION description VALUE 'Month of Quarter',
      month_of_year
        CLASSIFICATION caption VALUE 'MONTH_OF_YEAR'
        CLASSIFICATION description VALUE 'Month of Year',
      season
        CLASSIFICATION caption VALUE 'SEASON'
        CLASSIFICATION description VALUE 'Season',
      season_order
        CLASSIFICATION caption VALUE 'SEASON_ORDER'
        CLASSIFICATION description VALUE 'Season Order')
    LEVEL month
      LEVEL TYPE MONTHS
      CLASSIFICATION caption VALUE 'MONTH'
      CLASSIFICATION description VALUE 'Month'
      KEY month_id
      MEMBER NAME month_name
      MEMBER CAPTION month_name
      MEMBER DESCRIPTION month_long_name
      ORDER BY month_end_date
      DETERMINES (month_end_date,
        quarter_id,
        season,
        season_order,
        month_of_year,
        month_of_quarter)
    LEVEL quarter
      LEVEL TYPE QUARTERS
      CLASSIFICATION caption VALUE 'QUARTER'
      CLASSIFICATION description VALUE 'Quarter'
      KEY quarter_id
      MEMBER NAME quarter_name
      MEMBER CAPTION quarter_name
      MEMBER DESCRIPTION quarter_name
      ORDER BY quarter_end_date
      DETERMINES (quarter_end_date,
        quarter_of_year,
        year_id)
    LEVEL year
      LEVEL TYPE YEARS
      CLASSIFICATION caption VALUE 'YEAR'
      CLASSIFICATION description VALUE 'Year'
      KEY year_id
      MEMBER NAME year_name
      MEMBER CAPTION year_name
      MEMBER DESCRIPTION year_name
      ORDER BY year_end_date
      DETERMINES (year_end_date)
    LEVEL season
      LEVEL TYPE QUARTERS
      CLASSIFICATION caption VALUE 'SEASON'
      CLASSIFICATION description VALUE 'Season'
      KEY season
      MEMBER NAME season
      MEMBER CAPTION season
      MEMBER DESCRIPTION season
    LEVEL month_of_quarter
      LEVEL TYPE MONTHS
      CLASSIFICATION caption VALUE 'MONTH_OF_QUARTER'
      CLASSIFICATION description VALUE 'Month of Quarter'
      KEY month_of_quarter;

The following example describes the PRODUCT_DIM table:

    
    
    desc PRODUCT_DIM
    
    Name            Null?    Type          
    --------------- -------- ------------- 
    DEPARTMENT_ID   NOT NULL NUMBER        
    DEPARTMENT_NAME NOT NULL VARCHAR2(100) 
    CATEGORY_ID     NOT NULL NUMBER        
    CATEGORY_NAME   NOT NULL VARCHAR2(100)

The following example creates a `STANDARD` type attribute dimension, using
columns from the PRODUCT_DIM table:

    
    
    CREATE OR REPLACE ATTRIBUTE DIMENSION product_attr_dim
    USING product_dim 
    ATTRIBUTES
     (department_id,
      department_name,
      category_id,
      category_name)
    LEVEL DEPARTMENT
      KEY department_id
      ALTERNATE KEY department_name
      MEMBER NAME department_name
      MEMBER CAPTION department_name
      ORDER BY department_name
    LEVEL CATEGORY
      KEY category_id
      ALTERNATE KEY category_name
      MEMBER NAME category_name
      MEMBER CAPTION category_name
      ORDER BY category_name
      DETERMINES(department_id)
    ALL MEMBER NAME 'ALL PRODUCTS';

The following example describes the GEOGRAPHY_DIM table:

    
    
    desc GEOGRAPHY_DIM
    
    Name                Null?    Type          
    ---------------     -------- ------------- 
    DEPARTMENT_ID       NOT NULL NUMBER        
    DEPARTMENT_NAME     NOT NULL VARCHAR2(100) 
    CATEGORY_ID         NOT NULL NUMBER        
    CATEGORY_NAME       NOT NULL VARCHAR2(100) 
    REGION_ID           NOT NULL VARCHAR2(120) 
    REGION_NAME         NOT NULL VARCHAR2(100) 
    COUNTRY_ID          NOT NULL VARCHAR2(2)   
    COUNTRY_NAME        NOT NULL VARCHAR2(120) 
    STATE_PROVINCE_ID   NOT NULL VARCHAR2(120) 
    STATE_PROVINCE_NAME NOT NULL VARCHAR2(400)

The following example creates an `STANDARD` type attribute dimension, using
columns from the GEOGRAPHY_DIM table:

    
    
    CREATE OR REPLACE ATTRIBUTE DIMENSION geography_attr_dim
    USING geography_dim
    ATTRIBUTES
     (region_id,
      region_name,
      country_id,
      country_name,
      state_province_id,
      state_province_name)
    LEVEL REGION
      KEY region_id
      ALTERNATE KEY region_name
      MEMBER NAME region_name
      MEMBER CAPTION region_name
      ORDER BY region_name
    LEVEL COUNTRY
      KEY country_id
      ALTERNATE KEY country_name
      MEMBER NAME country_name
      MEMBER CAPTION country_name
      ORDER BY country_name
      DETERMINES(region_id)
    LEVEL STATE_PROVINCE
      KEY state_province_id
      ALTERNATE KEY state_province_name
      MEMBER NAME state_province_name
      MEMBER CAPTION state_province_name
      ORDER BY state_province_name
      DETERMINES(country_id)
    ALL MEMBER NAME 'ALL CUSTOMERS';


[← Previous](CREATE-ANALYTIC-VIEW.md)

[Next →](CREATE-AUDIT-POLICY-Unified-Auditing.md)
