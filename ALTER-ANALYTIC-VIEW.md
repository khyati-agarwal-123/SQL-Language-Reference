[Previous](ADMINISTER-KEY-MANAGEMENT.md) [Next](ALTER-ATTRIBUTE-
DIMENSION.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER ANALYTIC VIEW

## ALTER ANALYTIC VIEW

Purpose

Use the `ALTER` `ANALYTIC` `VIEW` statement to rename or compile an analytic
view. Additionally, you can modify grouping level caches by adding or dropping
a new level grouping cache to a specifed analytic view.

For other alterations, use `CREATE` `OR` `REPLACE` `ANALYTIC` `VIEW`.

Prerequisites

To alter an analytic view in your own schema, you must have the `ALTER`
`ANALYTIC` `VIEW` system privilege. To alter an analytic view in another
user's schema, you must have the `ALTER` `ANY` `ANALYTIC` `VIEW` system
privilege or `ALTER` `ANY` `TABLE` granted on the analytic view.

Syntax

alter_analytic_view::=

![Description of alter_analytic_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_analytic_view.gif)  
[Description of the illustration
alter_analytic_view.eps](img_text/alter_analytic_view.md)

alter_add_cache_clause::=

  

![Description of alter_add_cache_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_add_cache_clause.gif)  
[Description of the illustration
alter_add_cache_clause.eps](img_text/alter_add_cache_clause.md)

  

alter_drop_cache_clause::=

  

![Description of alter_drop_cache_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_drop_cache_clause.gif)  
[Description of the illustration
alter_drop_cache_clause.eps](img_text/alter_drop_cache_clause.md)

  

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema in which the analytic view exists. If you do not specify a
schema, then Oracle Database looks for the analytic view in your own schema.

analytic_view_name

Specify the name of the analytic view.

RENAME TO

Specify `RENAME` `TO` to change the name of the analytic view. For
`new_av_name`, specify a new name for the analytic view.

COMPILE

Specify `COMPILE` to compile the analytic view.

alter_add_cache_clause

Use this clause to add a new level grouping cache to a specified analytic view
like the measure group, level clause and the cache type. Before you add a new
level grouping cache, you must ensure that it does not match a previously
defined cache with the same measures and levels.

alter_drop_cache_clause

Use this clause to drop an existent level grouping cache from an analytic
view. You must specify the attributes of the level grouping you are about to
drop, like the measure group and the level clause.

Example: Change the Name of an Analytic View

    
    
    ALTER ANALYTIC VIEW sales_av RENAME TO mysales_av;

Example: Add a New Level Grouping Cache to an Analytic View

    
    
    ALTER ANALYTIC VIEW TKHCSGL308_UNITS_AVIEW_CACHE ADD CACHE
        MEASURE GROUP (sales, units, cost)
        LEVELS (TIME.FISCAL.FISCAL_QUARTER, WAREHOUSE);
    
    


[← Previous](ADMINISTER-KEY-MANAGEMENT.md)

[Next →](ALTER-ATTRIBUTE-DIMENSION.md)
