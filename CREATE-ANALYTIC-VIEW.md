[Previous](COMMIT.md) [Next](CREATE-ATTRIBUTE-DIMENSION.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE ANALYTIC VIEW

## CREATE ANALYTIC VIEW

Purpose

Use the `CREATE` `ANALYTIC` `VIEW` statement to create an analytic view. An
analytic view specifies the source of its fact data and defines measures that
describe calculations or other analytic operations to perform on the data. An
analytic view also specifies the attribute dimensions and hierarchies that
define the rows of the analytic view.

Prerequisites

To create an analytic view in your own schema, you must have the `CREATE`
`ANALYTIC` `VIEW` system privilege. To create an analytic view in another
user's schema, you must have the `CREATE` `ANY` `ANALYTIC` `VIEW` system
privilege.

Syntax

create_analytic_view::=

![Description of create_analytic_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_analytic_view.gif)  
[Description of the illustration
create_analytic_view.eps](img_text/create_analytic_view.md)

classification_clause::=

![Description of classification_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/classification_clause.gif)  
[Description of the illustration
classification_clause.eps](img_text/classification_clause.md)

using_clause::=

![Description of using_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/using_clause.gif)  
[Description of the illustration using_clause.eps](img_text/using_clause.md)

source_clause::=

  

![Description of source_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/source_clause.gif)  
[Description of the illustration
source_clause.eps](img_text/source_clause.md)

  

dim_by_clause::=

![Description of dim_by_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dim_by_clause.gif)  
[Description of the illustration
dim_by_clause.eps](img_text/dim_by_clause.md)

dim_key::=

![Description of dim_key.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dim_key.gif)  
[Description of the illustration dim_key.eps](img_text/dim_key.md)

dim_ref::=

![Description of dim_ref.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dim_ref.gif)  
[Description of the illustration dim_ref.eps](img_text/dim_ref.md)

hier_ref::=

![Description of hier_ref.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/hier_ref.gif)  
[Description of the illustration hier_ref.eps](img_text/hier_ref.md)

measures_clause::=

![Description of measures_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/measures_clause.gif)  
[Description of the illustration
measures_clause.eps](img_text/measures_clause.md)

av_measure::=

![Description of av_measure.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/av_measure.gif)  
[Description of the illustration av_measure.eps](img_text/av_measure.md)

base_meas_clause::=

![Description of base_meas_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/base_meas_clause.gif)  
[Description of the illustration
base_meas_clause.eps](img_text/base_meas_clause.md)

calc_meas_clause::=

  

![Description of calc_meas_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/calc_meas_clause.gif)  
[Description of the illustration
calc_meas_clause.eps](img_text/calc_meas_clause.md)

  

meas_aggregate_clause::=

![Description of meas_aggregate_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/meas_aggregate_clause.gif)  
[Description of the illustration
meas_aggregate_clause.eps](img_text/meas_aggregate_clause.md)

default_measure_clause::=

![Description of default_measure_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_measure_clause.gif)  
[Description of the illustration
default_measure_clause.eps](img_text/default_measure_clause.md)

default_aggregate_clause::=

![Description of default_aggregate_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_aggregate_clause.gif)  
[Description of the illustration
default_aggregate_clause.eps](img_text/default_aggregate_clause.md)

cache_clause::=

![Description of cache_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cache_clause.gif)  
[Description of the illustration cache_clause.eps](img_text/cache_clause.md)

cache_specification::=

![Description of cache_specification.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cache_specification.gif)  
[Description of the illustration
cache_specification.eps](img_text/cache_specification.md)

levels_clause::=

![Description of levels_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/levels_clause.gif)  
[Description of the illustration
levels_clause.eps](img_text/levels_clause.md)

level_specification::=

![Description of level_specification.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/level_specification.gif)  
[Description of the illustration
level_specification.eps](img_text/level_specification.md)

level_group_type::=

  

![Description of level_group_type.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/level_group_type.gif)  
[Description of the illustration
level_group_type.eps](img_text/level_group_type.md)

  

fact_columns_clause::=

  

![Description of fact_columns_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/fact_columns_clause.gif)  
[Description of the illustration
fact_columns_clause.eps](img_text/fact_columns_clause.md)

  

qry_transform_clause::=

  

![Description of qry_transform_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/qry_transform_clause.gif)  
[Description of the illustration
qry_transform_clause.eps](img_text/qry_transform_clause.md)

  

Semantics

OR REPLACE

Specify `OR` `REPLACE` to replace an existing definition of an analytic view
with a different definition.

FORCE and NOFORCE

Specify `FORCE` to force the creation of the analytic view even if it does not
successfully compile. If you specify `NOFORCE`, then the analytic view must
compile successfully, otherwise an error occurs. The default is `NOFORCE`.

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the analytic view does not exist, a new analytic view is created at the end of the statement.

  * If the analytic view exists, this is the analytic view you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

schema

Specify the schema in which to create the analytic view. If you do not specify
a schema, then Oracle Database creates the analytic view in your own schema.

analytic_view_name

Specify a name for the analytic view.

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

using_clause

Use this clause to declare the sources that you want to use to build the
analytic view.

source_clause

You can specify any of the following sources to build an analytic view:

  * A fact table or a view.

  * External tables and remote tables.

  * A table or a view in another schema. You can specify an alias for the table or the view.

REMOTE

Specify `REMOTE` on a given source to indicate to the analytic view that the
given source is backed by remote data and should be optimized as remote data.

dim_by_clause

Specify the attribute dimensions of the analytic view.

dim_key

Specify an attribute dimension, columns of the fact table, columns of the
attribute dimension, and hierarchies that are related in the analytic view.

With the `KEY` keyword, specify one or more columns in the fact table.

With the `REFERENCES` keyword, specify attributes of the attribute dimensions
that the analytic view is dimensioned by. Each attribute must be a level key.
The `DISTINCT` keyword supports the use of denormalized fact tables, in which
the attribute dimension and fact data are in the same table. Use `REFERENCES`
`DISTINCT` when an attribute dimension is defined using the fact table.

With the `HIERARCHIES` keyword, specify the hierarchies in the analytic view
that use the attribute dimension.

dim_ref

Specify an attribute dimension. You can specify an alias for an attribute
dimension, which is required if you use the same dimension more than once or
if you use multiple dimensions with the same name from different schemas.

hier_ref

Specify a hierarchy. You can specify an alias for a hierarchy. You can specify
one of the hierarchies in the list as the default. If you do not specify a
default, the first hierarchy in the list is the default.

measures_clause

Specify the measures for the analytic view.

av_measure

Define a measure using either a single fact column or an expression over
measures in this analytic view. A measure can be either a base measure or a
calculated measure.

base_measure_clause

Define a base measure by optionally specifying a fact column or a
`meas_aggregate_clause`, or both. If you do not specify a fact column, then
the analytic view uses the column of the fact table that has the same name as
the measure. If a column by the same name does not exist, an error is raised.

calc_measure_clause

Define a calculated measure by specifying an analytic view expression. The
expression may reference other measures in the analytic view, but may not
reference fact columns. Calculated measures do not have an aggregate clause
because they're computed over the aggregated base measures.

For the syntax and descriptions of analytic view expressions, see [Analytic
View Expressions](analytic-view-measure-
expressions.md#GUID-F8C7ED67-A4EC-479C-975F-12F1F4B8CBA0 "You can use
analytic view expressions to create calculated measures within the definition
of an analytic view or in a query that selects from an analytic view.").

default_measure_clause

Specify a measure to use as the default measure for the analytic view. If you
do not specify a measure, the first measure defined is the default.

meas_aggregate_clausÃ¨

Specify a default aggregation function for a base measure. If you do not
specify an aggregation function, then the function specified by the
`default_aggregate_clause` is used.

aggr_function

The functions that you can aggregate by in the `meas_aggregate_clause` and
`default_aggregate_clause ` are the following: `APPROX_COUNT_DISTINCT`,
`APPROX_COUNT_DISTINCT_AGG`, `AVG`, `COUNT`, `MAX`, `MIN`, `STDDEV`,
`STDDEV_POP`, `STDDEV_SAMP`, `SUM`, `VAR_POP`, `VAR_SAMP`, and `VARIANCE`.

default_aggregate_clause

Specify a default aggregation function for all of the base measures in the
analytic view. If you do not specify a default aggregation function, then the
default value is `SUM`.

cache_clause

Specify a cache clause to improve query response time when an appropriate
materialized view is available. You can specify one or more cache
specifications.

cache_specification

Specify one or more measure groups for a cache clause. To include all measure
groups, specify `ALL`. Each measure group can contain one or more measures and
one or more level groupings. A level grouping can contain one or more level
specifications.

level_specification

Specify one or more levels for a level grouping of a measure group for a cache
specification. Specify only one level per hierarchy. A materialized view must
exist that contains the aggregated values for the hierarchy level.

level_group_type

If you specify the `USING` clause, then the given table will be directly used
at query time, if the analytic view determines that this is the best cache to
use for the query. The typical shape of the cache is a column for each measure
in the `MEASURE GROUP` plus a column per level key of each level in the cache.
There is one row per member combination, across all given levels, that has at
least one contributing row from the fact table. The column names of the given
table must match a specific format so that the analytic view can identify
which columns line up with which measures and level keys. The names of the
columns can be retrieved from the `DBMS_HIERARCHY` package using the method
`GET_MV_SQL_FOR_AV_CACHE`.

This method takes in the cache to generate SQL for and returns the SQL text
for the cache. This SQL text can be used to create a materialized view for the
cache. It can also be used to create an aggregate table using `CREATE TABLE
AS`.

At compile time of the analytic view, the following checks will be made in
regard to the materialized table:

  * The table must exist and be accessible by the owner of the analytic view
  * The columns of the table must include the expected cache columns

fact_columns_clause

Specify this clause to explictly state the fact columns that can be accessed
by the dervided analytic view. You can aggregate any columns of the fact table
that appear in `fact_columns_clause` at query time with the aggregation
operator specified in the derived analytic view

If an alias is provided for the fact column, then the alias name must be used
in the dervided analytic view. The alias defaults to the fact column name if
not specified.

It is a semantic analysis error, if two or more fact columns are specified
with the same name.

If you do not specify this clause, then no fact columns can be accessed for
aggregation by the derived analytic view. This is the default.

qry_transform_clause

Specify this clause on an analytic view, if you want the view to participate
in detecting queries that match its semantic model and transform it into an
equivalent analytic view query if appropriate.

Restrictions

You cannot use `qry_transform_clause` on an analytic view in the following
cases:

  * When the analytic view contains an attribute dimension with more than one dimension table (either a snowflake or starflake schema)

  * When a dimension table joins to the fact table at a level that is above the leaf level of the dimension (i.e. a `REFERENCES DISTINCT` join) 

  * When `NORELY` is specified and one or more base tables are remote tables 

The new clause allows for an optional `RELY` or `NORELY` keyword. The default
is `NORELY`.

The analytic view metadata can be viewed as a set of constraints on the
underlying data. These constraints are not enforced by the database, but can
be checked using the `DBMS_HIERARCHY.VALIDATE_ANALYTIC_VIEW` procedure.

The `RELY` keyword indicates that the constraints implied on the data by the
analytic view metadata can be relied upon without validation when being
considered for base table transform. If `NORELY` is specified, then the data
must be in a valid state in relation to the metadata in order for the base
table transform to take place.

Examples

The following is a description of the `SALES_FACT` table:

    
    
    desc SALES_FACT
    Name              Null? Type          
    ----------------- ----- ------------- 
    MONTH_ID                VARCHAR2(10)  
    CATEGORY_ID             NUMBER(6)     
    STATE_PROVINCE_ID       VARCHAR2(120) 
    UNITS                   NUMBER(6)     
    SALES                   NUMBER(12,2)

The following example creates the `SALES_AV` analytic view using the
`SALES_FACT` table:

    
    
    CREATE OR REPLACE ANALYTIC VIEW sales_av
    USING sales_fact
    DIMENSION BY
      (time_attr_dim                         -- An attribute dimension of time data
        KEY month_id REFERENCES month_id
        HIERARCHIES (
          time_hier DEFAULT),
       product_attr_dim                      -- An attribute dimension of product data
        KEY category_id REFERENCES category_id
        HIERARCHIES (
          product_hier DEFAULT),
       geography_attr_dim                    -- An attribute dimension of store data
        KEY state_province_id 
        REFERENCES state_province_id HIERARCHIES (
          geography_hier DEFAULT)
       )
    MEASURES
     (sales FACT sales,                      -- A base measure
      units FACT units,                      -- A base measure
      sales_prior_period AS                  -- Calculated measures
        (LAG(sales) OVER (HIERARCHY time_hier OFFSET 1)),
      sales_year_ago AS
        (LAG(sales) OVER (HIERARCHY time_hier OFFSET 1
         ACROSS ANCESTOR AT LEVEL year)),
      chg_sales_year_ago AS
        (LAG_DIFF(sales) OVER (HIERARCHY time_hier OFFSET 1
         ACROSS ANCESTOR AT LEVEL year)),
      pct_chg_sales_year_ago AS
        (LAG_DIFF_PERCENT(sales) OVER (HIERARCHY time_hier OFFSET 1
         ACROSS ANCESTOR AT LEVEL year)),
      sales_qtr_ago AS
        (LAG(sales) OVER (HIERARCHY time_hier OFFSET 1
         ACROSS ANCESTOR AT LEVEL quarter)),
      chg_sales_qtr_ago AS
        (LAG_DIFF(sales) OVER (HIERARCHY time_hier OFFSET 1
         ACROSS ANCESTOR AT LEVEL quarter)),
      pct_chg_sales_qtr_ago AS
        (LAG_DIFF_PERCENT(sales) OVER (HIERARCHY time_hier OFFSET 1
         ACROSS ANCESTOR AT LEVEL quarter))
      )
    DEFAULT MEASURE SALES;


[← Previous](COMMIT.md)

[Next →](CREATE-ATTRIBUTE-DIMENSION.md)
