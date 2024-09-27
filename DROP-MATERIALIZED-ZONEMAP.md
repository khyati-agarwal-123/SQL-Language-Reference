[Previous](DROP-MATERIALIZED-VIEW-LOG.md) [Next](drop-mle-env.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP LIBRARY to DROP SYNONYM](SQL-Statements-DROP-LIBRARY-to-DROP-SYNONYM.md)
  3. DROP MATERIALIZED ZONEMAP

## DROP MATERIALIZED ZONEMAP

Purpose

Use the `DROP` `MATERIALIZED` `ZONEMAP` statement to remove an existing zone
map from the database.

Prerequisites

The zone map must be in your own schema or you must have the `DROP` `ANY`
`MATERIALIZED` `VIEW` system privilege. You must also have the privileges to
drop the internal table and indexes that the database uses to maintain the
zone map data.

See Also:

[DROP TABLE](DROP-TABLE.md#GUID-39D89EDC-155D-4A24-837E-D45DDA757B45) and
[DROP INDEX](DROP-INDEX.md#GUID-F60F75DF-2866-4F93-BB7F-8FCE64BF67B6) for
information on privileges required to drop objects that the database uses to
maintain the zone map

Syntax

drop_materialized_zonemap::=

![Description of drop_materialized_zonemap.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_materialized_zonemap.gif)  
[Description of the illustration
drop_materialized_zonemap.eps](img_text/drop_materialized_zonemap.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the zone map. If you omit `schema`, then Oracle
Database assumes the zone map is in your own schema.

zonemap_name

Specify the name of the existing zone map to be dropped.

Example

Dropping a Zone Map: Examples

The following statement drops the zone map `sales_zmap`:

    
    
    DROP MATERIALIZED ZONEMAP sales_zmap; 


[← Previous](DROP-MATERIALIZED-VIEW-LOG.md)

[Next →](drop-mle-env.md)
