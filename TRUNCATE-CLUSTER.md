[Previous](SET-TRANSACTION.md) [Next](TRUNCATE-TABLE.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: MERGE to UPDATE](SQL-Statements-MERGE-to-UPDATE.md)
  3. TRUNCATE CLUSTER 

## TRUNCATE CLUSTER

Purpose

Note:

You cannot roll back a `TRUNCATE CLUSTER` statement.

Use the `TRUNCATE CLUSTER` statement to remove all rows from a cluster. By
default, Oracle Database also performs the following tasks:

  * Deallocates all space used by the removed rows except that specified by the `MINEXTENTS` storage parameter 

  * Sets the `NEXT` storage parameter to the size of the last extent removed from the segment by the truncation process 

Removing rows with the `TRUNCATE` statement can be more efficient than
dropping and re-creating a cluster. Dropping and re-creating a cluster
invalidates dependent objects of the cluster, requires you to regrant object
privileges on the cluster, and requires you to re-create the indexes and
cluster on the table and respecify its storage parameters. Truncating has none
of these effects.

Removing rows with the `TRUNCATE CLUSTER` statement can be faster than
removing all rows with the `DELETE` statement, especially if the cluster has
numerous indexes and other dependencies.

See Also:

  * [DELETE](DELETE.md#GUID-156845A5-B626-412B-9F95-8869B988ABD7) and [DROP CLUSTER](DROP-CLUSTER.md#GUID-531F7DE2-AA2A-400E-BC9A-4CBEEA7B7156) for information on other ways of dropping data from a cluster 

  * [TRUNCATE TABLE](TRUNCATE-TABLE.md#GUID-B76E5846-75B5-4876-98EC-439E15E4D8A4) for information on truncating a table 

Prerequisites

To truncate a cluster, the cluster must be in your schema or you must have
`DROP` `ANY` `TABLE` system privilege.

See Also:

"[Restrictions on Truncating Tables](TRUNCATE-
TABLE.md#GUID-B76E5846-75B5-4876-98EC-439E15E4D8A4__CHDDGIHF)"

Syntax

truncate_cluster::=

![Description of truncate_cluster.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/truncate_cluster.gif)  
[Description of the illustration
truncate_cluster.eps](img_text/truncate_cluster.md)

Semantics

CLUSTER Clause

Specify the schema and name of the cluster to be truncated. You can truncate
only an indexed cluster, not a hash cluster. If you omit `schema`, then the
database assumes the cluster is in your own schema.

When you truncate a cluster, the database also automatically deletes all data
in the indexes of the cluster tables.

STORAGE Clauses

The `STORAGE` clauses let you determine what happens to the space freed by the
truncated rows. The `DROP` `STORAGE` clause and `REUSE` `STORAGE` clause also
apply to the space freed by the data deleted from associated indexes.

DROP STORAGE

Specify `DROP` `STORAGE` to deallocate all space from the deleted rows from
the cluster except the space allocated by the `MINEXTENTS` parameter of the
cluster. This space can subsequently be used by other objects in the
tablespace. Oracle Database also sets the `NEXT` storage parameter to the size
of the last extent removed from the segment in the truncation process. This is
the default.

REUSE STORAGE

Specify `REUSE` `STORAGE` to retain the space from the deleted rows allocated
to the cluster. Storage values are not reset to the values when the table or
cluster was created. This space can subsequently be used only by new data in
the cluster resulting from insert or update operations. This clause leaves
storage parameters at their current settings.

If you have specified more than one free list for the object you are
truncating, then the `REUSE` `STORAGE` clause also removes any mapping of free
lists to instances and resets the high-water mark to the beginning of the
first extent.

Examples

Truncating a Cluster: Example

The following statement removes all rows from all tables in the `personnel`
cluster, but leaves the freed space allocated to the tables:

    
    
    TRUNCATE CLUSTER personnel REUSE STORAGE;
    

The preceding statement also removes all data from all indexes on the tables
in the `personnel` cluster.


[← Previous](SET-TRANSACTION.md)

[Next →](TRUNCATE-TABLE.md)
