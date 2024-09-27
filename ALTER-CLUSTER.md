[Previous](ALTER-AUDIT-POLICY-Unified-Auditing.md) [Next](ALTER-
DATABASE.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER CLUSTER 

## ALTER CLUSTER

Purpose

Use the `ALTER` `CLUSTER` statement to redefine storage and parallelism
characteristics of a cluster.

Note:

You cannot use this statement to change the number or the name of columns in
the cluster key, and you cannot change the tablespace in which the cluster is
stored.

See Also:

[CREATE CLUSTER](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7) for information on
creating a cluster, [DROP CLUSTER](DROP-
CLUSTER.md#GUID-531F7DE2-AA2A-400E-BC9A-4CBEEA7B7156) and [DROP TABLE](DROP-
TABLE.md#GUID-39D89EDC-155D-4A24-837E-D45DDA757B45) for information on
removing tables from a cluster, and [CREATE TABLE](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6) ...
[physical_properties](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2128663) for
information on adding a table to a cluster

Prerequisites

The cluster must be in your own schema or you must have the `ALTER` `ANY`
`CLUSTER` system privilege.

Syntax

alter_cluster::=

![Description of alter_cluster.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_cluster.gif)  
[Description of the illustration
alter_cluster.eps](img_text/alter_cluster.md)

([physical_attributes_clause::](ALTER-
CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D__I2128460),
[size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID),
[MODIFY PARTITION](ALTER-
CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D__BGBHGICA),
[allocate_extent_clause::=](ALTER-
CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D__I2128438),
[deallocate_unused_clause::=](ALTER-
CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D__I2129829),
[parallel_clause::=](ALTER-
CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D__I2129840))

physical_attributes_clause::

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB))

allocate_extent_clause::=

![Description of allocate_extent_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/allocate_extent_clause.gif)  
[Description of the illustration
allocate_extent_clause.eps](img_text/allocate_extent_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

deallocate_unused_clause::=

![Description of deallocate_unused_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/deallocate_unused_clause.gif)  
[Description of the illustration
deallocate_unused_clause.eps](img_text/deallocate_unused_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing table.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the cluster. If you omit `schema`, then Oracle
Database assumes the cluster is in your own schema.

cluster

Specify the name of the cluster to be altered.

physical_attributes_clause

Use this clause to change the values of the `PCTUSED`, `PCTFREE`, and
`INITRANS` parameters of the cluster.

Use the `STORAGE` clause to change the storage characteristics of the cluster.

See Also:

  * [physical_attributes_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393) for information on the parameters 

  * [storage_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393__I1026834) for a full description of that clause 

Restriction on Physical Attributes

You cannot change the values of the storage parameters `INITIAL` and
`MINEXTENTS` for a cluster.

SIZE

integer

Use the `SIZE` clause to specify the number of cluster keys that will be
stored in data blocks allocated to the cluster.

Restriction on SIZE

You can change the `SIZE` parameter only for an indexed cluster, not for a
hash cluster.

See Also:

[CREATE CLUSTER](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7) for a description of
the `SIZE` parameter and "[Modifying a Cluster: Example](ALTER-
CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D__I2135513)"

MODIFY PARTITION

Specify `MODIFY` `PARTITION` `partition` `allocate_extent_clause` to
explicitly allocate a new extent for a cluster partition. This operation is
valid only for range-partitioned hash clusters. For `partition`, specify the
cluster partition name.

allocate_extent_clause

Specify `allocate_extent_clause` to explicitly allocate a new extent for a
cluster. This operation is valid only for indexed clusters and nonpartitioned
hash clusters.

When you explicitly allocate an extent with the `allocate_extent_clause`,
Oracle Database does not evaluate the storage parameters of the cluster and
determine a new size for the next extent to be allocated (as it does when you
create a table). Therefore, specify `SIZE` if you do not want Oracle Database
to use a default value.

See Also:

[allocate_extent_clause](allocate_extent_clause.md#GUID-
DA6B3DC2-84B5-4404-AD96-5ABF7341580F) for a full description of this clause

deallocate_unused_clause

Use the `deallocate_unused_clause` to explicitly deallocate unused space at
the end of the cluster and make the freed space available for other segments.

See Also:

[deallocate_unused_clause](deallocate_unused_clause.md#GUID-016A106B-47D4-4FFF-8A3B-2DF19A5FE9FF)
for a full description of this clause and "[Deallocating Unused Space:
Example](ALTER-
CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D__I2135524)"

parallel_clause

Specify the `parallel_clause` to change the default degree of parallelism for
queries on the cluster.

See Also:

[parallel_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) in the
documentation on `CREATE` `TABLE` for complete information on this clause

Examples

The following examples modify the clusters that were created in the `CREATE`
`CLUSTER` "[Examples](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2105031)".

Modifying a Cluster: Example

The next statement alters the `personnel` cluster:

    
    
    ALTER CLUSTER personnel
       SIZE 1024 CACHE;
    

Oracle Database allocates 1024 bytes for each cluster key value and enables
the cache attribute. Assuming a data block size of 2 kilobytes, future data
blocks within this cluster contain 2 cluster keys in each data block, or 2
kilobytes divided by 1024 bytes.

Deallocating Unused Space: Example

The following statement deallocates unused space from the `language` cluster,
keeping 30 kilobytes of unused space for future use:

    
    
    ALTER CLUSTER language 
       DEALLOCATE UNUSED KEEP 30 K;

Altering Clusters: Example

The following statement creates a cluster with the default key size (600):

    
    
    CREATE CLUSTER EMP_DEPT (DEPTNO NUMBER(3))   
       SIZE 600   
       TABLESPACE USERS   
       STORAGE (INITIAL 200K   
          NEXT 300K   
          MINEXTENTS 2   
          PCTINCREASE 33);

The following statement queries `USER_CLUSTERS` to display the cluster
metadata:

    
    
    SELECT CLUSTER_NAME, TABLESPACE_NAME, KEY_SIZE, CLUSTER_TYPE, AVG_BLOCKS_PER_KEY, MIN_EXTENTS, MAX_EXTENTS FROM USER_CLUSTERS;
    
    CLUSTER_NAME    TABLESPACE_NAME                  KEY_SIZE CLUST AVG_BLOCKS_PER_KEY MIN_EXTENTS MAX_EXTENTS
    --------------- ------------------------------ ---------- ----- ------------------ ----------- -----------
    EMP_DEPT        USERS                                 600 INDEX                              1  2147483645
    

The following statement modifies the cluster key size:

    
    
    ALTER CLUSTER EMP_DEPT SIZE 1024;

The following statement displays the metadata of the modified cluster:

    
    
    SELECT CLUSTER_NAME, TABLESPACE_NAME, KEY_SIZE, CLUSTER_TYPE, AVG_BLOCKS_PER_KEY, MIN_EXTENTS, MAX_EXTENTS FROM USER_CLUSTERS;
    
    CLUSTER_NAME    TABLESPACE_NAME                  KEY_SIZE CLUST AVG_BLOCKS_PER_KEY MIN_EXTENTS MAX_EXTENTS
    --------------- ------------------------------ ---------- ----- ------------------ ----------- -----------
    EMP_DEPT        USERS                                1024 INDEX                              1  2147483645
    

The following statement deallocates unused space from the `EMP_DEPT` cluster,
keeping 30 kilobytes of unused space for future use:

    
    
    ALTER CLUSTER EMP_DEPT DEALLOCATE UNUSED KEEP 30 K;

The following statement displays the metadata of the modified cluster:

    
    
    SELECT CLUSTER_NAME, TABLESPACE_NAME, KEY_SIZE, CLUSTER_TYPE, AVG_BLOCKS_PER_KEY, MIN_EXTENTS, MAX_EXTENTS FROM USER_CLUSTERS;
    
    CLUSTER_NAME    TABLESPACE_NAME                  KEY_SIZE CLUST AVG_BLOCKS_PER_KEY MIN_EXTENTS MAX_EXTENTS
    --------------- ------------------------------ ---------- ----- ------------------ ----------- -----------
    EMP_DEPT        USERS                                1024 INDEX                              1  2147483645
    

Live SQL:

View and run a related example on Oracle Live SQL at [Creating and Altering
Clusters](https://livesql.oracle.com/apex/livesql/docs/sqlrf/alter-
cluster/key-size.md)


[← Previous](ALTER-AUDIT-POLICY-Unified-Auditing.md)

[Next →](ALTER-DATABASE.md)
