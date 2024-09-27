[Previous](CREATE-AUDIT-POLICY-Unified-Auditing.md) [Next](CREATE-
CONTEXT.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE CLUSTER 

## CREATE CLUSTER

Purpose

Use the `CREATE` `CLUSTER` statement to create a cluster. A cluster is a
schema object that contains data from one or more tables.

  * An indexed cluster must contain more than one table, and all of the tables in the cluster have one or more columns in common. Oracle Database stores together all the rows from all the tables that share the same cluster key. 

  * In a hash cluster, which can contain one or more tables, Oracle Database stores together rows that have the same hash key value. 

For information on existing clusters, query the `USER_CLUSTERS`,
`ALL_CLUSTERS`, and `DBA_CLUSTERS` data dictionary views.

See Also:

  * [Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=CNCPT608) for general information on clusters 

  * [Oracle Database SQL Tuning Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=TGSQL850) for suggestions on when to use clusters 

  * [Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN002) for information on the data dictionary views 

Prerequisites

To create a cluster in your own schema, you must have `CREATE` `CLUSTER`
system privilege. To create a cluster in another user's schema, you must have
`CREATE` `ANY` `CLUSTER` system privilege. Also, the owner of the schema to
contain the cluster must have either space quota on the tablespace containing
the cluster or the `UNLIMITED` `TABLESPACE` system privilege.

Oracle Database does not automatically create an index for a cluster when the
cluster is initially created. Data manipulation language (DML) statements
cannot be issued against cluster tables in an indexed cluster until you create
a cluster index with a `CREATE` `INDEX` statement.

Syntax

create_cluster::=

![Description of create_cluster.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_cluster.gif)  
[Description of the illustration
create_cluster.eps](img_text/create_cluster.md)

([physical_attributes_clause::=](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2127411),
[size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID),
[cluster_range_partitions::=](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__CACHDBII))

physical_attributes_clause::=

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB))

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

cluster_range_partitions::=

![Description of cluster_range_partitions.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/cluster_range_partitions.gif)  
[Description of the illustration
cluster_range_partitions.eps](img_text/cluster_range_partitions.md)

([range_values_clause::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2125922),
[table_partition_description::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2127282))

Semantics

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the cluster does not exist, a new cluster is created at the end of the statement.

  * If the cluster exists, this is the cluster you have at the end of the statement. A new one is not created because the older cluster is detected.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement.`

schema

Specify the schema to contain the cluster. If you omit `schema`, then Oracle
Database creates the cluster in your current schema.

cluster

Specify is the name of the cluster to be created. The name must satisfy the
requirements listed in "[Database Object Naming Rules](Database-Object-Names-
and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

After you create a cluster, you add tables to it. A cluster can contain a
maximum of 32 tables. Object tables and tables containing LOB columns or
columns of the `Any*` Oracle-supplied types cannot be part of a cluster. After
you create a cluster and add tables to it, the cluster is transparent. You can
access clustered tables with SQL statements just as you can access
nonclustered tables.

See Also:

[CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6)
for information on adding tables to a cluster, "[Creating a Cluster:
Example](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2105033)", and
"[Adding Tables to a Cluster: Example](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2129354)"

SHARING

Use the sharing clause if you want to create the cluster in an application
root in the context of an application maintenance. This type of object is
called an application common object and it can be shared with the application
PDBs that belong to the application root.

You can specify how the object is shared using one of the following sharing
attributes:

  * `METADATA` \- A metadata link shares the metadata, but its data is unique to each container. This type of object is referred to as a metadata-linked application common object. 

  * `NONE` \- The object is not shared and can only be accessed in the application root. 

column

Specify one or more names of columns in the cluster key. You can specify up to
16 cluster key columns. These columns must correspond in both data type and
size to columns in each of the clustered tables, although they need not
correspond in name.

You cannot specify integrity constraints as part of the definition of a
cluster key column. Instead, you can associate integrity constraints with the
tables that belong to the cluster.

See Also:

"[Cluster Keys: Example](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2129341)"

datatype

Specify the data type of each cluster key column.

Restrictions on Cluster Data Types

Cluster data types are subject to the following restrictions:

  * You cannot specify a cluster key column of data type `LONG`, `LONG` `RAW`, `REF`, nested table, varray, `BLOB`, `CLOB`, `BFILE`, the `Any*` Oracle-supplied types, or user-defined object type. 

  * You can specify a column of type `ROWID`, but Oracle Database does not guarantee that the values in such columns are valid rowids. 

See Also:

"[Data Types](Data-Types.md#GUID-A3C0D836-BADB-44E5-A5D4-265BA5968483)" for
information on data types

COLLATE

Use this clause to specify the data-bound collation for character data type
columns in the cluster key.

For `column_collation_name`, specify the collation as follows:

  * When creating an indexed cluster or a sorted hash cluster, you can specify one of the following collations: `BINARY`, `USING_NLS_COMP`, `USING_NLS_SORT`, or `USING_NLS_SORT_CS`. 

  * When creating a hash cluster that is not sorted, you can specify any valid named collation or pseudo-collation.

If you omit this clause, then columns in the cluster key inherit the effective
schema default collation of the schema containing the cluster. Refer to the
[DEFAULT_COLLATION](ALTER-
SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B__DEFAULT_COLLATION-39CF7241)
clause of `ALTER` `SESSION` for more information on the effective schema
default collation.

The collations of cluster key columns must match the collations of the
corresponding columns in the tables created in the cluster.

You can specify the `COLLATE` clause only if the `COMPATIBLE` initialization
parameter is set to `12.2` or greater, and the `MAX_STRING_SIZE`
initialization parameter is set to `EXTENDED`.

To change the collation of a cluster key column, you must recreate the
cluster.

SORT

The `SORT` keyword is valid only if you are creating a hash cluster. Table
rows are hashed into buckets on cluster key columns without `SORT`, and then
sorted in each bucket on the columns with this clause. This may improve
response time during subsequent queries on the clustered data.

All columns without the `SORT` clause must come before all columns with the
`SORT` clause in the `CREATE CLUSTER` statement.

Restriction on Sorted Hash Clusters

Row dependency is not supported for sorted hash clusters.

See Also:

  * See "[HASHKEYS Clause](CREATE-CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2143441)" for information on creating a hash cluster. 

  * [Managing Hash Clusters](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-ADB821B7-70D2-4829-956A-F74436754BCF) for more information. 

physical_attributes_clause

The `physical_attributes_clause` lets you specify the storage characteristics
of the cluster. Each table in the cluster uses these storage characteristics
as well. If you do not specify values for these parameters, then Oracle
Database uses the following defaults:

  * `PCTFREE`: 10 

  * `PCTUSED`: 40 

  * `INITRANS`: 2 or the default value of the tablespace to contain the cluster, whichever is greater 

See Also:

[physical_attributes_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393)
and
[storage_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393__I1026834)
for a complete description of these clauses

SIZE

Specify the amount of space in bytes reserved to store all rows with the same
cluster key value or the same hash value. This space determines the maximum
number of cluster or hash values stored in a data block. If `SIZE` is not a
divisor of the data block size, then Oracle Database uses the next largest
divisor. If `SIZE` is larger than the data block size, then the database uses
the operating system block size, reserving at least one data block for each
cluster or hash value.

The database also considers the length of the cluster key when determining how
much space to reserve for the rows having a cluster key value. Larger cluster
keys require larger sizes. To see the actual size, query the `KEY_SIZE` column
of the `USER_CLUSTERS` data dictionary view. (This value does not apply to
hash clusters, because hash values are not actually stored in the cluster.)

If you omit this parameter, then the database reserves one data block for each
cluster key value or hash value.

TABLESPACE

Specify the tablespace in which the cluster is to be created.

INDEX Clause

Specify `INDEX` to create an indexed cluster. In an indexed cluster, Oracle
Database stores together rows having the same cluster key value. Each distinct
cluster key value is stored only once in each data block, regardless of the
number of tables and rows in which it occurs. If you specify neither `INDEX`
nor `HASHKEYS`, then Oracle Database creates an indexed cluster by default.

After you create an indexed cluster, you must create an index on the cluster
key before you can issue any data manipulation language (DML) statements
against a table in the cluster. This index is called the cluster index.

You cannot create a cluster index for a hash cluster, and you need not create
an index on a hash cluster key.

See Also:

[CREATE INDEX](CREATE-INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE)
for information on creating a cluster index and [Oracle Database Concepts
](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=CNCPT608)for general information in indexed clusters

HASHKEYS Clause

Specify the `HASHKEYS` clause to create a hash cluster and specify the number
of hash values for the hash cluster. In a hash cluster, Oracle Database stores
together rows that have the same hash key value. The hash value for a row is
the value returned by the hash function of the cluster.

Oracle Database rounds up the `HASHKEYS` value to the nearest prime number to
obtain the actual number of hash values. The minimum value for this parameter
is 2. If you omit both the `INDEX` clause and the `HASHKEYS` parameter, then
the database creates an indexed cluster by default.

When you create a hash cluster, the database immediately allocates space for
the cluster based on the values of the `SIZE` and `HASHKEYS` parameters.

See Also:

[Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=CNCPT609) for more information on how Oracle Database
allocates space for clusters and "[Hash Clusters: Examples](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2129365)"

SINGLE TABLE

`SINGLE` `TABLE` indicates that the cluster is a type of hash cluster
containing only one table. This clause can provide faster access to rows in
the table.

Restriction on Single-table Clusters

Only one table can be present in the cluster at a time. However, you can drop
the table and create a different table in the same cluster.

See Also:

"[Single-Table Hash Clusters: Example](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__I2129381)"

HASH IS expr

Specify an expression to be used as the hash function for the hash cluster.
The expression:

  * Must evaluate to a positive value

  * Must contain at least one column, with referenced columns of any data type as long as the entire expression evaluates to a number of scale 0. For example: `number_column` * `LENGTH`(`varchar2_column`) 

  * Cannot reference user-defined PL/SQL functions

  * Cannot reference the pseudocolumns `LEVEL` or `ROWNUM`

  * Cannot reference the user-related functions `USERENV`, `UID`, or `USER` or the datetime functions `CURRENT_DATE`, `CURRENT_TIMESTAMP`, `DBTIMEZONE`, `EXTRACT` (datetime), `FROM_TZ`, `LOCALTIMESTAMP`, `NUMTODSINTERVAL`, `NUMTOYMINTERVAL`, `SESSIONTIMEZONE`, `SYSDATE`, `SYSTIMESTAMP`, `TO_DSINTERVAL`, `TO_TIMESTAMP`, `TO_DATE`, `TO_TIMESTAMP_TZ`, `TO_YMINTERVAL`, and `TZ_OFFSET`. 

  * Cannot evaluate to a constant

  * Cannot be a scalar subquery expression

  * Cannot contain columns qualified with a schema or object name (other than the cluster name)

If you omit the `HASH` `IS` clause, then Oracle Database uses an internal hash
function for the hash cluster.

For information on existing hash functions, query the `USER_`, `ALL_`, and
`DBA_CLUSTER_HASH_EXPRESSIONS` data dictionary tables.

The cluster key of a hash column can have one or more columns of any data
type. Hash clusters with composite cluster keys or cluster keys made up of
noninteger columns must use the internal hash function.

See Also:

[Oracle Database Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN002) for information on the data dictionary views

parallel_clause

The `parallel_clause` lets you parallelize the creation of the cluster.

For complete information on this clause, refer to [parallel_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) in the
documentation on `CREATE` `TABLE`.

NOROWDEPENDENCIES | ROWDEPENDENCIES

This clause has the same behavior for a cluster that it has for a table. Refer to "[NOROWDEPENDENCIES | ROWDEPENDENCIES](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__CJAEEGDA)" in `CREATE` `TABLE` for information. 

CACHE | NOCACHE

CACHE

Specify `CACHE` if you want the blocks retrieved for this cluster to be placed
at the most recently used end of the least recently used (LRU) list in the
buffer cache when a full table scan is performed. This clause is useful for
small lookup tables.

NOCACHE

Specify `NOCACHE` if you want the blocks retrieved for this cluster to be
placed at the least recently used end of the LRU list in the buffer cache when
a full table scan is performed. This is the default behavior.

`NOCACHE` has no effect on clusters for which you specify `KEEP` in the
`storage_clause`.

cluster_range_partitions

Specify the `cluster_range_partitions` clause to create a range-partitioned
hash cluster. If you specify this clause, then you must also specify the
`HASHKEYS` clause.

Use the `cluster_range_partitions` clause to partition the cluster on ranges
of values from the column list. When you add a table to a range-partitioned
hash cluster, it is automatically partitioned on the same columns, with the
same number of partitions, and on the same partition bounds as the cluster.
Oracle Database assigns system-generated names to the table partitions.

Each partitioning key column with a character data type must have one of the
following declared collations: `BINARY`, `USING_NLS_COMP`, `USING_NLS_SORT`,
or `USING_NLS_SORT_CS`.

The `cluster_range_partitions` clause has the same semantics as the
`range_partitions` clause of `CREATE` `TABLE`, except that here you cannot
specify the `INTERVAL` clause. For complete information, refer to
[range_partitions](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__BABJDACD) in the
documentation on `CREATE` `TABLE`.

See Also:

"[Range-Partitioned Hash Clusters: Example](CREATE-
CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7__CACCJEAG)"

Examples

Creating a Cluster: Example

The following statement creates a cluster named `personnel` with the cluster
key column `department`, a cluster size of 512 bytes, and storage parameter
values:

    
    
    CREATE CLUSTER personnel
       (department NUMBER(4))
    SIZE 512 
    STORAGE (initial 100K next 50K);

Cluster Keys: Example

The following statement creates the cluster index on the cluster key of
`personnel`:

    
    
    CREATE INDEX idx_personnel ON CLUSTER personnel;
    

After creating the cluster index, you can add tables to the index and perform
DML operations on those tables.

Adding Tables to a Cluster: Example

The following statements create some departmental tables from the sample
`hr.employees` table and add them to the personnel cluster created in the
earlier example:

    
    
    CREATE TABLE dept_10
       CLUSTER personnel (department_id)
       AS SELECT * FROM employees WHERE department_id = 10;
    
    CREATE TABLE dept_20
       CLUSTER personnel (department_id)
       AS SELECT * FROM employees WHERE department_id = 20;

Hash Clusters: Examples

The following statement creates a hash cluster named `language` with the
cluster key column `cust_language`, a maximum of 10 hash key values, each of
which is allocated 512 bytes, and storage parameter values:

    
    
    CREATE CLUSTER language (cust_language VARCHAR2(3))
       SIZE 512 HASHKEYS 10
       STORAGE (INITIAL 100k next 50k);
    

Because the preceding statement omits the `HASH` `IS` clause, Oracle Database
uses the internal hash function for the cluster.

The following statement creates a hash cluster named `address` with the
cluster key made up of the columns `postal_code` and `country_id`, and uses a
SQL expression containing these columns for the hash function:

    
    
    CREATE CLUSTER address
       (postal_code NUMBER, country_id CHAR(2))
       HASHKEYS 20
       HASH IS MOD(postal_code + country_id, 101);

Single-Table Hash Clusters: Example

The following statement creates a single-table hash cluster named
`cust_orders` with the cluster key `customer_id` and a maximum of 100 hash key
values, each of which is allocated 512 bytes:

    
    
    CREATE CLUSTER cust_orders (customer_id NUMBER(6))
       SIZE 512 SINGLE TABLE HASHKEYS 100;

Range-Partitioned Hash Clusters: Example

The following statement creates a range-partitioned hash cluster named `sales`
with five range partitions based on the amount sold. The cluster key is made
up of the columns `amount_sold` and `prod_id`. The cluster uses the hash
function `(amount_sold * 10 + prod_id)` and has a maximum of 100000 hash key
values, each of which is allocated 300 bytes.

    
    
    CREATE CLUSTER sales (amount_sold NUMBER, prod_id NUMBER)
      HASHKEYS 100000
      HASH IS (amount_sold * 10 + prod_id)
      SIZE 300
      TABLESPACE example
      PARTITION BY RANGE (amount_sold)
        (PARTITION p1 VALUES LESS THAN (2001),
         PARTITION p2 VALUES LESS THAN (4001),
         PARTITION p3 VALUES LESS THAN (6001),
         PARTITION p4 VALUES LESS THAN (8001),
         PARTITION p5 VALUES LESS THAN (MAXVALUE));

Create Cluster Tables: Example

The following statement creates a cluster named `emp_dept` with the default
key size (600):

    
    
    CREATE CLUSTER emp_dept (deptno NUMBER(3))  
       SIZE 600  
       TABLESPACE USERS 
       STORAGE (INITIAL 200K  
          NEXT 300K  
          MINEXTENTS 2  
          PCTINCREASE 33);

The following statement creates a cluster table named `dept` under `emp_dept`
cluster:

    
    
    CREATE TABLE dept (  
       deptno NUMBER(3) PRIMARY KEY)  
       CLUSTER emp_dept (deptno);

The following statement creates another cluster table named `empl` under
`emp_dept` cluster:

    
    
    CREATE TABLE empl (  
       emplno NUMBER(5) PRIMARY KEY,  
       emplname VARCHAR2(15) NOT NULL,  
       deptno NUMBER(3) REFERENCES dept)  
       CLUSTER emp_dept (deptno);

The following statement creates an index for the `emp_dept` cluster:

    
    
    CREATE INDEX emp_dept_index 
       ON CLUSTER emp_dept 
       TABLESPACE USERS 
       STORAGE (INITIAL 50K 
          NEXT 50K 
          MINEXTENTS 2 
          MAXEXTENTS 10 
          PCTINCREASE 33);

The following statement queries `USER_CLUSTERS` to display the cluster
metadata:

    
    
    SELECT CLUSTER_NAME, TABLESPACE_NAME, CLUSTER_TYPE, PCT_INCREASE, MIN_EXTENTS, MAX_EXTENTS FROM USER_CLUSTERS;
    
    CLUSTER_NAME	TABLESPACE CLUST PCT_INCREASE MIN_EXTENTS MAX_EXTENTS
    --------------- ---------- ----- ------------ ----------- -----------
    EMP_DEPT	USERS	   INDEX			1  2147483645

The following statement queries `USER_CLU_COLUMNS` to display the cluster
metadata:

    
    
    SELECT * FROM USER_CLU_COLUMNS;
    
    CLUSTER_NAME	CLU_COLUMN_NAME      TABLE_NAME TAB_COLUMN_NAME
    --------------- -------------------- ---------- --------------------
    EMP_DEPT	DEPTNO		     DEPT	DEPTNO
    EMP_DEPT	DEPTNO		     EMPL	DEPTNO

The following statement queries `USER_INDEXES` to display the index attributes
of the `emp_dept` cluster:

    
    
    SELECT INDEX_NAME, INDEX_TYPE, PCT_INCREASE, MIN_EXTENTS, MAX_EXTENTS FROM USER_INDEXES WHERE TABLE_NAME='EMP_DEPT';
    
    INDEX_NAME	INDEX_TYPE	PCT_INCREASE MIN_EXTENTS MAX_EXTENTS
    --------------- --------------- ------------ ----------- -----------
    EMP_DEPT_INDEX	CLUSTER 			       1  2147483645
    


[← Previous](CREATE-AUDIT-POLICY-Unified-Auditing.md)

[Next →](CREATE-CONTEXT.md)
