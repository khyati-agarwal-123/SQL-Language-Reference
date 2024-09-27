[Previous](ALTER-MATERIALIZED-VIEW-LOG.md) [Next](alter-mle-env.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER MATERIALIZED ZONEMAP

## ALTER MATERIALIZED ZONEMAP

Purpose

Use the `ALTER` `MATERIALIZED` `ZONEMAP` statement to modify an existing zone
map in one of the following ways:

  * To change its attributes

  * To change its default refresh method and mode

  * To enable or disable its use for pruning

  * To compile it, rebuild it, or make it unusable

See Also:

  * [CREATE MATERIALIZED ZONEMAP](CREATE-MATERIALIZED-ZONEMAP.md#GUID-1E5048FC-3D28-49BC-80FE-7871568B4702) for information on creating zone maps 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG9355) for more information on zone maps 

Prerequisites

The zone map must be in your own schema or you must have the `ALTER` `ANY`
`MATERIALIZED` `VIEW` system privilege.

The user who owns the schema containing the zone map must have access to any
base tables of the zone map that reside outside of that schema, either through
a `READ` or `SELECT` object privilege on each of the tables, or through the
`READ` `ANY` `TABLE` or `SELECT` `ANY` `TABLE` system privilege.

Syntax

alter_materialized_zonemap::=

![Description of alter_materialized_zonemap.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_materialized_zonemap.gif)  
[Description of the illustration
alter_materialized_zonemap.eps](img_text/alter_materialized_zonemap.md)

alter_zonemap_attributes::=

![Description of alter_zonemap_attributes.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_zonemap_attributes.gif)  
[Description of the illustration
alter_zonemap_attributes.eps](img_text/alter_zonemap_attributes.md)

zonemap_refresh_clause::=

![Description of zonemap_refresh_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/zonemap_refresh_clause.gif)  
[Description of the illustration
zonemap_refresh_clause.eps](img_text/zonemap_refresh_clause.md)

Note:

When specifying the `zonemap_refresh_clause`, you must specify at least one
clause after the `REFRESH` keyword.

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the zone map. If you omit `schema`, then Oracle
Database assumes the zone map is in your own schema.

zonemap_name

Specify the name of the zone map to be altered.

alter_zonemap_attributes

Use this clause to modify the following attributes for the zone map: `PCTFREE`, `PCTUSED`, and `CACHE` or `NOCACHE`. These attributes have the same semantics for `ALTER` `MATERIALIZED` `ZONEMAP` and `CREATE` `MATERIALIZED` `ZONEMAP`. For complete information on these attributes, refer to [PCTFREE](CREATE-MATERIALIZED-ZONEMAP.md#GUID-1E5048FC-3D28-49BC-80FE-7871568B4702__CACDIEDG), [PCTUSED](CREATE-MATERIALIZED-ZONEMAP.md#GUID-1E5048FC-3D28-49BC-80FE-7871568B4702__CACJGFEF), and [CACHE | NOCACHE](CREATE-MATERIALIZED-ZONEMAP.md#GUID-1E5048FC-3D28-49BC-80FE-7871568B4702__CACIGEHI) in the documentation on `CREATE` `MATERIALIZED` `ZONEMAP`. 

zonemap_refresh_clause

Use this clause to modify the default refresh method and mode for the zone
map. This clause has the same semantics for `ALTER` `MATERIALIZED` `ZONEMAP`
and `CREATE` `MATERIALIZED` `ZONEMAP`. For complete information on this
clause, refer to [zonemap_refresh_clause](CREATE-MATERIALIZED-
ZONEMAP.md#GUID-1E5048FC-3D28-49BC-80FE-7871568B4702__CACBDIJH) in the
documentation on `CREATE` `MATERIALIZED` `ZONEMAP`.

ENABLE | DISABLE PRUNING

Use this clause to enable or disable use of the zone map for pruning. This clause has the same semantics for `ALTER` `MATERIALIZED` `ZONEMAP` and `CREATE` `MATERIALIZED` `ZONEMAP`. For complete information on this clause, refer to [ENABLE | DISABLE PRUNING](CREATE-MATERIALIZED-ZONEMAP.md#GUID-1E5048FC-3D28-49BC-80FE-7871568B4702__CACEAADH) in the documentation on `CREATE` `MATERIALIZED` `ZONEMAP`

COMPILE

This clause lets you explicitly compile the zone map. This operation validates
the zone map after a DDL operation changes the structure of one or more of its
base tables. It is usually not necessary to issue this clause because Oracle
database automatically compiles a zone map that requires compilation before
using it. However, if you would like to explicitly compile a zone map, then
you can use this clause to do so.

The result of compiling a zone map depends on whether a base table is changed
in a way that affects the zone map. For example, if a column is added to a
base table, then the zone map will be valid after compilation because the
change does not affect the zone map. However, if a column that is included in
the defining subquery of the zone map is dropped from a base table, then the
zone map will be invalid after compilation.

You can determine if a zone map requires compilation by querying the
`COMPILE_STATE` column of the `ALL_`, `DBA_`, and `USER_ZONEMAPS` data
dictionary views. If the value of the column is `NEEDS_COMPILE`, then the zone
map requires compilation.

REBUILD

This clause lets you explicitly rebuild the zone map. This operation refreshes
the data in the zone map. This clause is useful in the following situations:

  * You can use this clause to refresh the data for a refresh-on-demand zone map. Refer to the [ON DEMAND](CREATE-MATERIALIZED-ZONEMAP.md#GUID-1E5048FC-3D28-49BC-80FE-7871568B4702__CACFCGJJ) clause in the documentation on `CREATE` `MATERIALIZED` `ZONEMAP` for more information. 

  * You must issue this clause after an `EXCHANGE` `PARTITION` operation on one of the base tables of a zone map, regardless of the default refresh mode of the zone map. 

  * If a zone map is marked unusable, then you must issue this clause to mark it usable. You can determine if a zone map is marked unusable by querying the `UNUSABLE` column of the `ALL_`, `DBA_`, and `USER_ZONEMAPS` data dictionary views. 

UNUSABLE

Specify this clause to make the zone map unusable. Subsequent queries will not
use the zone map and the database will no longer maintain the zone map. You
can make the zone map usable again by issuing an `ALTER` `MATERIALIZED`
`ZONEMAP` ... `REBUILD` statement.

Examples

Modifying Zone Map Attributes: Example

The following statement modifies the `PCTFREE` and `PCTUSED` attributes of
zone map `sales_zmap`, and modifies the zone map so that it does not use
caching:

    
    
    ALTER MATERIALIZED ZONEMAP sales_zmap
      PCTFREE 20 PCTUSED 50 NOCACHE;

Modifying the Default Refresh Method and Mode for a Zone Map: Example

The following statement changes the default refresh method to `FAST` and the
default refresh mode to `ON` `COMMIT` for zone map `sales_zmap`:

    
    
    ALTER MATERIALIZED ZONEMAP sales_zmap
      REFRESH FAST ON COMMIT;

Disabling Use of a Zone Map for Pruning: Example

The following statement disables use of zone map `sales_zmap` for pruning:

    
    
    ALTER MATERIALIZED ZONEMAP sales_zmap
      DISABLE PRUNING;

Compiling a Zone Map: Example

The following statement compiles zone map `sales_zmap`:

    
    
    ALTER MATERIALIZED ZONEMAP sales_zmap
      COMPILE;

Rebuilding a Zone Map: Example

The following statement rebuilds zone map `sales_zmap`:

    
    
    ALTER MATERIALIZED ZONEMAP sales_zmap
      REBUILD;

Making a Zone Map Unusable: Example

The following statement makes zone map `sales_zmap` unusable:

    
    
    ALTER MATERIALIZED ZONEMAP sales_zmap
      UNUSABLE;


[← Previous](ALTER-MATERIALIZED-VIEW-LOG.md)

[Next →](alter-mle-env.md)
