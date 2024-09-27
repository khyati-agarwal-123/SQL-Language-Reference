[Previous](DROP-AUDIT-POLICY-Unified-Auditing.md) [Next](SQL-Statements-
DROP-CONTEXT-to-DROP-JAVA.md) JavaScript must be enabled to correctly
display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. DROP CLUSTER 

## DROP CLUSTER

Purpose

Use the `DROP` `CLUSTER` clause to remove a cluster from the database.

Note:

When you drop a cluster, any tables in the recycle bin that were once part of
that cluster are purged from the recycle bin and can no longer be recovered
with a `FLASHBACK TABLE` operation.

You cannot uncluster an individual table. Instead you must perform these
steps:

  1. Create a new table with the same structure and contents as the old one, but with no `CLUSTER` clause. 

  2. Drop the old table.

  3. Use the `RENAME` statement to give the new table the name of the old one. 

  4. Grant privileges on the new unclustered table. Grants on the old clustered table do not apply.

See Also:

[CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6),
[DROP TABLE](DROP-TABLE.md#GUID-39D89EDC-155D-4A24-837E-D45DDA757B45),
[RENAME](RENAME.md#GUID-573347CE-3EB8-42E5-B4D5-EF71CA06FAFC),
[GRANT](GRANT.md#GUID-20B4E2C0-A7F8-4BC8-A5E8-BE61BDC41AC3) for information
on these steps

Prerequisites

The cluster must be in your own schema or you must have the `DROP` `ANY`
`CLUSTER` system privilege.

Syntax

drop_cluster::=

![Description of drop_cluster.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_cluster.gif)  
[Description of the illustration drop_cluster.eps](img_text/drop_cluster.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the cluster. If you omit `schema`, then the
database assumes the cluster is in your own schema.

cluster

Specify the name of the cluster to be dropped. Dropping a cluster also drops
the cluster index and returns all cluster space, including data blocks for the
index, to the appropriate tablespace(s).

INCLUDING TABLES

Specify `INCLUDING` `TABLES` to drop all tables that belong to the cluster.

CASCADE CONSTRAINTS

Specify `CASCADE` `CONSTRAINTS` to drop all referential integrity constraints
from tables outside the cluster that refer to primary and unique keys in
tables of the cluster. If you omit this clause and such referential integrity
constraints exist, then the database returns an error and does not drop the
cluster.

Examples

Dropping a Cluster: Examples

The following examples drop the clusters created in the "[Examples](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2105031)" section of
`CREATE` `CLUSTER`.

The following statements drops the `language` cluster:

    
    
    DROP CLUSTER language;
    

The following statement drops the `personnel` cluster as well as tables
`dept_10` and `dept_20` and any referential integrity constraints that refer
to primary or unique keys in those tables:

    
    
    DROP CLUSTER personnel
       INCLUDING TABLES
       CASCADE CONSTRAINTS;


[← Previous](DROP-AUDIT-POLICY-Unified-Auditing.md)

[Next →](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
