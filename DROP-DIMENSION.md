[Previous](DROP-DATABASE-LINK.md) [Next](DROP-DIRECTORY.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP DIMENSION 

## DROP DIMENSION

Purpose

Use the `DROP` `DIMENSION` statement to remove the named dimension.

This statement does not invalidate materialized views that use relationships
specified in dimensions. However, requests that have been rewritten by query
rewrite may be invalidated, and subsequent operations on such views may
execute more slowly.

See Also:

  * [CREATE DIMENSION](CREATE-DIMENSION.md#GUID-E6CD4CFC-5D06-4A8F-9DF1-C609A7EB8413) and [ALTER DIMENSION](ALTER-DIMENSION.md#GUID-16B451F9-FF21-4E44-ACCA-2CFFA6F3F0F9) for information on creating and modifying a dimension 

  * [Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT511) for general information about dimensions 

Prerequisites

The dimension must be in your own schema or you must have the `DROP` `ANY`
`DIMENSION` system privilege to use this statement.

Syntax

drop_dimension::=

![Description of drop_dimension.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_dimension.gif)  
[Description of the illustration
drop_dimension.eps](img_text/drop_dimension.md)

Semantics

schema

Specify the name of the schema in which the dimension is located. If you omit
`schema`, then Oracle Database assumes the dimension is in your own schema.

dimension

Specify the name of the dimension you want to drop. The dimension must already
exist.

Examples

Dropping a Dimension: Example

This example drops the `sh.customers_dim` dimension:

    
    
    DROP DIMENSION customers_dim;

See Also:

"[Creating a Dimension: Examples](CREATE-
DIMENSION.md#GUID-E6CD4CFC-5D06-4A8F-9DF1-C609A7EB8413__I2092402)" and
"[Modifying a Dimension: Examples](ALTER-
DIMENSION.md#GUID-16B451F9-FF21-4E44-ACCA-2CFFA6F3F0F9__I2091224)" for
examples of creating and modifying this dimension


[← Previous](DROP-DATABASE-LINK.md)

[Next →](DROP-DIRECTORY.md)
