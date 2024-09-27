[Previous](create-logical-partition-tracking.md) [Next](CREATE-MATERIALIZED-
VIEW-LOG.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE MATERIALIZED VIEW 

## CREATE MATERIALIZED VIEW

Purpose

Use the `CREATE` `MATERIALIZED` `VIEW` statement to create a materialized
view. A materialized view is a database object that contains the results of a
query. The `FROM` clause of the query can name tables, views, and other
materialized views. Collectively these objects are called master tables (a
replication term) or detail tables (a data warehousing term). This reference
uses "master tables" for consistency. The databases containing the master
tables are called the master databases.

Note:

The keyword `SNAPSHOT` is supported in place of `MATERIALIZED` `VIEW` for
backward compatibility.

For replication purposes, materialized views allow you to maintain read-only
copies of remote data on your local node. You can select data from a
materialized view as you would from a table or view. In replication
environments, the materialized views commonly created are primary key, rowid,
object, and subquery materialized views.

See Also:

[Oracle Database Administratorâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-350A169D-8937-484D-B21F-37B46A024782) for
information on the types of materialized views used to support replication

For data warehousing purposes, the materialized views commonly created are
materialized aggregate views, single-table materialized aggregate views, and
materialized join views. All three types of materialized views can be used by
query rewrite, an optimization technique that transforms a user request
written in terms of master tables into a semantically equivalent request that
includes one or more materialized views.

See Also:

  * [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233)

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG008) for information on the types of materialized views used to support data warehousing 

Prerequisites

The privileges required to create a materialized view should be granted
directly rather than through a role.

To create a materialized view in your own schema:

  * You must have been granted the `CREATE` `MATERIALIZED` `VIEW` system privilege and either the `CREATE` `TABLE` or `CREATE` `ANY` `TABLE` system privilege. 

  * You must also have access to any master tables of the materialized view that you do not own, either through a `READ` or `SELECT` object privilege on each of the tables or through the `READ` `ANY` `TABLE` or `SELECT` `ANY` `TABLE` system privilege. 

To create a materialized view in another user's schema:

  * You must have the `CREATE` `ANY` `MATERIALIZED` `VIEW` system privilege. 

  * The owner of the materialized view must have the `CREATE` `TABLE` system privilege. The owner must also have access to any master tables of the materialized view that the schema owner does not own (for example, if the master tables are on a remote database) and to any materialized view logs defined on those master tables, either through a `READ` or `SELECT` object privilege on each of the tables or through the `READ` `ANY` `TABLE` or `SELECT` `ANY` `TABLE` system privilege. 

To create a refresh-on-commit materialized view (`REFRESH` `ON` `COMMIT`
clause), in addition to the preceding privileges, you must have the `ON`
`COMMIT` `REFRESH` object privilege on any master tables that you do not own
or you must have the `ON` `COMMIT` `REFRESH` system privilege.

To create the materialized view with query rewrite enabled, in addition to the
preceding privileges:

  * If the schema owner does not own the master tables, then the schema owner must have the `GLOBAL` `QUERY` `REWRITE` privilege or the `QUERY` `REWRITE` object privilege on each table outside the schema. 

  * If you are defining the materialized view on a prebuilt container (`ON` `PREBUILT` `TABLE` clause), then you must have the `READ` or `SELECT` privilege `WITH` `GRANT` `OPTION` on the container table. 

The user whose schema contains the materialized view must have sufficient
quota in the target tablespace to store the master table and index of the
materialized view or must have the `UNLIMITED` `TABLESPACE` system privilege.

When you create a materialized view, Oracle Database creates one internal
table and at least one index, and may create one view, all in the schema of
the materialized view. Oracle Database uses these objects to maintain the
materialized view data. You must have the privileges necessary to create these
objects.

You can create the following types of local materialized views (including both
`ON` `COMMIT` and `ON` `DEMAND`) on master tables with commit SCN-based
materialized view logs:

  * Materialized aggregate views, including materialized aggregate views on a single table

  * Materialized join views

  * Primary-key-based and rowid-based single table materialized views

  * `UNION` `ALL` materialized views, where each `UNION` `ALL` branch is one of the above materialized view types 

You cannot create remote materialized views on master tables with commit SCN-
based materialized view logs.

Creating a materialized view on master tables with different types of
materialized view logs (that is, a master table with timestamp-based
materialized view logs and a master table with commit SCN-based materialized
view logs) is not supported and causes `ORA-32414`.

To specify an edition in the `evaluation_edition_clause` or the
`unusable_editions_clause`, you must have the `USE` privilege on the edition.

To perform select from a materialized view, you must have the `SELECT ANY
TABLE` system privilege.

See Also:

  * [CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6), [CREATE VIEW](CREATE-VIEW.md#GUID-61D2D2B4-DACC-4C7C-89EB-7E50D9594D30), and [CREATE INDEX](CREATE-INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE) for information on these privileges 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-A422B474-4BED-4A60-AEDB-E93630746083) for information about the prerequisites that apply to creating replication materialized views 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG008) for information about the prerequisites that apply to creating data warehousing materialized views 

Syntax

create_materialized_view::=

![Description of create_materialized_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_materialized_view.gif)  
[Description of the illustration
create_materialized_view.eps](img_text/create_materialized_view.md)

([scoped_table_ref_constraint::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116388),
[physical_properties::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2147304),
[materialized_view_props::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116410),
[physical_attributes_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116626),
[create_mv_refresh::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116443),
[evaluation_edition_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CCHDHFBH),
[query_rewrite_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CCHGFGAI),
[subquery::=](SELECT.md#GUID-
CFA006CA-6FF1-4972-821E-6996142A51C6__I2126435),
[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052))

annotations_clause::=

For the full syntax and semantics of the `annotations_clause `see
[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052).

scoped_table_ref_constraint::=

![Description of scoped_table_ref_constraint.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/scoped_table_ref_constraint.gif)  
[Description of the illustration
scoped_table_ref_constraint.eps](img_text/scoped_table_ref_constraint.md)

physical_properties::=

![Description of physical_properties.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_properties.gif)  
[Description of the illustration
physical_properties.eps](img_text/physical_properties.md)

([deferred_segment_creation::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACGCCDG),
[segment_attributes_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116465),
[table_compression::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116476),
[inmemory_table_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACIBHAD),
[heap_org_table_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACDACJE),
[index_org_table_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116399))

materialized_view_props::=

![Description of materialized_view_props.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/materialized_view_props.gif)  
[Description of the illustration
materialized_view_props.eps](img_text/materialized_view_props.md)

([column_properties::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116487),
[table_partitioning_clauses::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2129707)âpart of
`CREATE` `TABLE` syntax, [parallel_clause::=](CREATE-MATERIALIZED-
VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2116920),
[build_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116521))

heap_org_table_clause::=

![Description of heap_org_table_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/heap_org_table_clause.gif)  
[Description of the illustration
heap_org_table_clause.eps](img_text/heap_org_table_clause.md)

index_org_table_clause::=

![Description of index_org_table_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/index_org_table_clause.gif)  
[Description of the illustration
index_org_table_clause.eps](img_text/index_org_table_clause.md)

(`mapping_table_clause`: not supported with materialized views,
[prefix_compression::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACDAHIE),
[index_org_overflow_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116560))

prefix_compression::=

![Description of prefix_compression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/prefix_compression.gif)  
[Description of the illustration
prefix_compression.eps](img_text/prefix_compression.md)

index_org_overflow_clause::=

![Description of index_org_overflow_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/index_org_overflow_clause.gif)  
[Description of the illustration
index_org_overflow_clause.eps](img_text/index_org_overflow_clause.md)

([segment_attributes_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116465))

create_mv_refresh::=

![Description of create_mv_refresh.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_mv_refresh.gif)  
[Description of the illustration
create_mv_refresh.eps](img_text/create_mv_refresh.md)

deferred_segment_creation::=

![Description of deferred_segment_creation.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/deferred_segment_creation.gif)  
[Description of the illustration
deferred_segment_creation.eps](img_text/deferred_segment_creation.md)

segment_attributes_clause::=

![Description of segment_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/segment_attributes_clause.gif)  
[Description of the illustration
segment_attributes_clause.eps](img_text/segment_attributes_clause.md)

([physical_attributes_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116626), `TABLESPACE` `SET`: not
supported with `CREATE` `MATERIALIZED` `VIEW`, [logging_clause::=](CREATE-
MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2116596))

physical_attributes_clause::=

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

([logging_clause::=](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E__CJAHABGF))

logging_clause::=

![Description of logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logging_clause.gif)  
[Description of the illustration
logging_clause.eps](img_text/logging_clause.md)

table_compression::=

![Description of table_compression.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/table_compression.gif)  
[Description of the illustration
table_compression.eps](img_text/table_compression.md)

inmemory_table_clause::=

![Description of inmemory_table_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_table_clause.gif)  
[Description of the illustration
inmemory_table_clause.eps](img_text/inmemory_table_clause.md)

([inmemory_attributes::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACJDJAJ),
[inmemory_column_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACIIGGA))

inmemory_attributes::=

![Description of inmemory_attributes.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_attributes.gif)  
[Description of the illustration
inmemory_attributes.eps](img_text/inmemory_attributes.md)

([inmemory_memcompress::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACCCGDI),
[inmemory_priority::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACIFBIC),
[inmemory_distribute::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACIJEAA),
[inmemory_duplicate::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACFCBGA))

inmemory_memcompress::=

![Description of inmemory_memcompress.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_memcompress.gif)  
[Description of the illustration
inmemory_memcompress.eps](img_text/inmemory_memcompress.md)

inmemory_priority::=

![Description of inmemory_priority.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_priority.gif)  
[Description of the illustration
inmemory_priority.eps](img_text/inmemory_priority.md)

inmemory_distribute::=

![Description of inmemory_distribute.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_distribute.gif)  
[Description of the illustration
inmemory_distribute.eps](img_text/inmemory_distribute.md)

inmemory_duplicate::=

![Description of inmemory_duplicate.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_duplicate.gif)  
[Description of the illustration
inmemory_duplicate.eps](img_text/inmemory_duplicate.md)

inmemory_column_clause::=

![Description of inmemory_column_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_column_clause.gif)  
[Description of the illustration
inmemory_column_clause.eps](img_text/inmemory_column_clause.md)

([inmemory_memcompress::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CACCCGDI))

column_properties::=

![Description of column_properties.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/column_properties.gif)  
[Description of the illustration
column_properties.eps](img_text/column_properties.md)

`(`[object_type_col_properties::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116642),
[nested_table_col_properties::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116653),
[varray_col_properties::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116664),
[LOB_partition_storage::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116912),
[LOB_storage_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116856), `XMLType_column_properties`:
not supported for materialized views)

object_type_col_properties::=

![Description of object_type_col_properties.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/object_type_col_properties.gif)  
[Description of the illustration
object_type_col_properties.eps](img_text/object_type_col_properties.md)

([substitutable_column_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116730))

substitutable_column_clause::=

![Description of substitutable_column_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/substitutable_column_clause.gif)  
[Description of the illustration
substitutable_column_clause.eps](img_text/substitutable_column_clause.md)

nested_table_col_properties::=

![Description of nested_table_col_properties.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/nested_table_col_properties.gif)  
[Description of the illustration
nested_table_col_properties.eps](img_text/nested_table_col_properties.md)

([substitutable_column_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116730),
[object_properties::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2126768),
[physical_properties::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2126711)âpart of
`CREATE` `TABLE` syntax, [column_properties::=](CREATE-MATERIALIZED-
VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2116487))

varray_col_properties::=

![Description of varray_col_properties.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/varray_col_properties.gif)  
[Description of the illustration
varray_col_properties.eps](img_text/varray_col_properties.md)

([substitutable_column_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116730),
[varray_storage_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__BABFECCA))

varray_storage_clause::=

![Description of varray_storage_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/varray_storage_clause.gif)  
[Description of the illustration
varray_storage_clause.eps](img_text/varray_storage_clause.md)

([LOB_parameters::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2160265))

LOB_storage_clause::=

![Description of lob_storage_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lob_storage_clause.gif)  
[Description of the illustration
lob_storage_clause.eps](img_text/lob_storage_clause.md)

([LOB_storage_parameters::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__BABCGFBH))

LOB_storage_parameters::=

![Description of lob_storage_parameters.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lob_storage_parameters.gif)  
[Description of the illustration
lob_storage_parameters.eps](img_text/lob_storage_parameters.md)

(`TABLESPACE` `SET`: not supported with `CREATE` `MATERIALIZED` `VIEW`,
[LOB_parameters::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2160265),
[storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB))

LOB_parameters::=

![Description of lob_parameters.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lob_parameters.gif)  
[Description of the illustration
lob_parameters.eps](img_text/lob_parameters.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB),
[logging_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116596))

LOB_partition_storage::=

![Description of lob_partition_storage.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lob_partition_storage.gif)  
[Description of the illustration
lob_partition_storage.eps](img_text/lob_partition_storage.md)

([LOB_storage_clause::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116856),
[varray_col_properties::=](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2116664))

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

build_clause::=

![Description of build_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/build_clause.gif)  
[Description of the illustration build_clause.eps](img_text/build_clause.md)

evaluation_edition_clause::=

![Description of evaluation_edition_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/evaluation_edition_clause.gif)  
[Description of the illustration
evaluation_edition_clause.eps](img_text/evaluation_edition_clause.md)

query_rewrite_clause::=

![Description of query_rewrite_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/query_rewrite_clause.gif)  
[Description of the illustration
query_rewrite_clause.eps](img_text/query_rewrite_clause.md)

unusable_editions_clause::=

![Description of unusable_editions_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/unusable_editions_clause.gif)  
[Description of the illustration
unusable_editions_clause.eps](img_text/unusable_editions_clause.md)

Semantics

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the view does not exist, a new view is created at the end of the statement.

  * If the view exists, this is the view you have at the end of the statement. A new one is not created because the older one is detected.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

annotations_clause

For the full semantics of the annotations clause see
[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052).

schema

Specify the schema to contain the materialized view. If you omit `schema`,
then Oracle Database creates the materialized view in your schema.

materialized_view

Specify the name of the materialized view to be created. The name must satisfy
the requirements listed in "[Database Object Naming Rules](Database-Object-
Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)". Oracle
Database generates names for the table and indexes used to maintain the
materialized view by adding a prefix or suffix to the materialized view name.

column_alias

You can specify a column alias for each column of the materialized view. The
column alias list explicitly resolves any column name conflict, eliminating
the need to specify aliases in the `SELECT` clause of the materialized view.
If you specify any column alias in this clause, then you must specify an alias
for each data source referenced in the `SELECT` clause.

ENCRYPT clause

Use this clause to encrypt this column of the materialized view. Refer to the
`CREATE` `TABLE` clause [encryption_spec](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__CEGDFHBD) for more
information on column encryption.

OF object_type

The `OF` `object_type` clause lets you explicitly create an object
materialized view of type `object_type`.

See Also:

See `CREATE` `TABLE` ... [object_table](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159410) for more
information on the `OF` `type_name` clause

scoped_table_ref_constraint

Use the `SCOPE` `FOR` clause to restrict the scope of references to a single
object table. You can refer either to the table name with `scope_table_name`
or to a column alias. The values in the `REF` column or attribute point to
objects in `scope_table_name` or `c_alias`, in which object instances of the
same type as the `REF` column are stored. If you specify aliases, then they
must have a one-to-one correspondence with the columns in the `SELECT` list of
the defining query of the materialized view.

See Also:

"[SCOPE REF
Constraints](constraint.md#GUID-1055EA97-BA6F-4764-A15F-1024FD5B6DFE__I1002226)"
for more information

DEFAULT COLLATION

Use this clause to specify the default collation for the materialized view.
The default collation is used as the derived collation for all the character
literals included in the defining query of the materialized view. The default
collation is not used by the materialized view columns; the collations for the
materialized view columns are derived from the materialized viewâs defining
subquery. The `CREATE` `MATERIALIZED` `VIEW` statement fails with an error, or
the materialized view is created in an invalid state, if any of its character
columns is based on an expression in the defining subquery that has no derived
collation.

For `collation_name`, specify a valid named collation or pseudo-collation.

If you omit this clause, then the default collation for the materialized view
is set to the effective schema default collation of the schema containing the
materialized view. Refer to the [DEFAULT_COLLATION](ALTER-
SESSION.md#GUID-27186B28-7EFC-4998-B1ED-2B905CC0211B__DEFAULT_COLLATION-39CF7241)
clause of `ALTER` `SESSION` for more information on the effective schema
default collation.

You can specify the `DEFAULT` `COLLATION` clause only if the `COMPATIBLE`
initialization parameter is set to `12.2` or greater, and the
`MAX_STRING_SIZE` initialization parameter is set to `EXTENDED`.

To change the default collation for a materialized view, you must recreate the
materialized view.

Restrictions on the Default Collation for Materialized Views

The following restrictions apply when specifying the default collation for a
materialized view:

  * If the defining query of the materialized view contains the `WITH` `plsql_declarations` clause, then the default collation of the materialized view must be `USING_NLS_COMP`. 

  * If the materialized view is created on a prebuilt table, then the declared collations of the table columns must be the same as the corresponding collations of the materialized view columns, as derived from the defining query.

ON PREBUILT TABLE Clause

The `ON` `PREBUILT` `TABLE` clause lets you register an existing table as a
preinitialized materialized view. This clause is particularly useful for
registering large materialized views in a data warehousing environment. The
table must have the same name and be in the same schema as the resulting
materialized view.

If the materialized view is dropped, then the preexisting table reverts to its
identity as a table.

Note:

This clause assumes that the table object reflects the materialization of a
subquery. Oracle strongly recommends that you ensure that this assumption is
true in order to ensure that the materialized view correctly reflects the data
in its master tables.

The `ON` `PREBUILT` `TABLE` clause could be useful in the following scenarios:

  * You have a table representing the result of a query. Creating the table was an expensive operation that possibly took a long time. You want to create a materialized view on the query. You can use the `ON` `PREBUILT` `TABLE` clause to avoid the expense of executing the query and populating the container for the materialized view. 

  * You temporarily discontinue having a materialized view, but keep its container table, using the `DROP` `MATERIALIZED` `VIEW` ... `PRESERVE` `TABLE` statement. You then decide to recreate the materialized view and you know that the master tables of the view have not changed. You can create the materialized view using the `ON` `PREBUILT` `TABLE` clause. This avoids the expense and time of creating and populating the container table for the materialized view. 

If you specify `ON` `PREBUILT` `TABLE`, then Oracle database does not create
the `I_SNAP$` index. This index improves fast refresh performance. If you want
the benefits of this index, then you can create it manually. Refer to [Oracle
Database Data Warehousing
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG8216) for more information.

WITH REDUCED PRECISION

Specify `WITH` `REDUCED` `PRECISION` to authorize the loss of precision that
will result if the precision of the table or materialized view columns do not
exactly match the precision returned by `subquery`.

WITHOUT REDUCED PRECISION

Specify `WITHOUT` `REDUCED` `PRECISION` to require that the precision of the
table or materialized view columns match exactly the precision returned by
`subquery`, or the create operation will fail. This is the default.

Restrictions on Using Prebuilt Tables

Prebuilt tables are subject to the following restrictions:

  * Each column alias in `subquery` must correspond to a column in the prebuilt table, and corresponding columns must have matching data types. 

  * If you specify this clause, then you cannot specify a `NOT` `NULL` constraint for any column that is not referenced in `subquery` unless you also specify a default value for that column. 

  * You cannot specify the `ON` `PREBUILT` `TABLE` clause when creating a rowid materialized view. 

See Also:

"[Creating Prebuilt Materialized Views: Example](CREATE-MATERIALIZED-
VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2092101)"

physical_properties_clause

The components of the `physical_properties_clause` have the same semantics for
materialized views that they have for tables, with exceptions and additions
described in the sections that follow.

Restriction on the physical_properties_clause

You cannot specify `ORGANIZATION` `EXTERNAL` for a materialized view.

deferred_segment_creation

Use this clause to determine when the segment for this materialized view
should be created. See the `CREATE` `TABLE` clause
[deferred_segment_creation](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__CEGJHDEB) for more
information.

segment_attributes_clause

Use the `segment_attributes_clause` to establish values for the `PCTFREE`,
`PCTUSED`, and `INITRANS` parameters, the storage characteristics for the
materialized view, to assign a tablespace, and to specify whether logging is
to occur. In the `USING` `INDEX` clause, you cannot specify `PCTFREE` or
`PCTUSED`.

TABLESPACE Clause

Specify the tablespace in which the materialized view is to be created. If you
omit this clause, then Oracle Database creates the materialized view in the
default tablespace of the schema containing the materialized view.

See Also:

[physical_attributes_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393)
and
[storage_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393__I1026834)
for a complete description of these clauses, including default values

logging_clause

Specify `LOGGING` or `NOLOGGING` to establish the logging characteristics for
the materialized view. The logging characteristic affects the creation of the
materialized view and any nonatomic refresh that is initiated by way of the
`DBMS_REFRESH` package. The default is the logging characteristic of the
tablespace in which the materialized view resides.

See Also:

[logging_clause](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E)
for a full description of this clause and [Oracle Database PL/SQL Packages and
Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS043) for more information on atomic and nonatomic
refresh

table_compression

Use the `table_compression` clause to instruct the database whether to
compress data segments to reduce disk and memory use. This clause has the same
semantics in `CREATE` `MATERIALIZED` `VIEW` and `CREATE` `TABLE`. Refer to the
[table_compression](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2128733) clause in the
documentation on `CREATE` `TABLE` for the full semantics of this clause.

inmemory_table_clause

Use the `inmemory_table_clause` to enable or disable the materialized view for
the In-Memory Column Store (IM column store). This clause has the same
semantics as the [inmemory_table_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__CEGBCAAE) in the
`CREATE` `TABLE` documentation.

inmemory_column_clause

Use the `inmemory_column_clause` to disable specific materialized view columns
for the IM column store, and to specify the data compression method for
specific columns. This clause has the same semantics here as it has for the
[inmemory_column_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__CEGJEEBB) in the
`CREATE` `TABLE` documentation, with the following addition: If you specify
the `inmemory_column_clause`, then you must also specify a `column_alias` for
each column in the materialized view.

index_org_table_clause

The `ORGANIZATION` `INDEX` clause lets you create an index-organized
materialized view. In such a materialized view, data rows are stored in an
index defined on the primary key of the materialized view. You can specify
index organization for the following types of materialized views:

  * Read-only and updatable object materialized views. You must ensure that the master table has a primary key.

  * Read-only and updatable primary key materialized views.

  * Read-only rowid materialized views.

The keywords and parameters of the `index_org_table_clause` have the same
semantics as described in `CREATE` `TABLE`, with the restrictions that follow.

See Also:

The [index_org_table_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2128766) of `CREATE`
`TABLE`

Restrictions on Index-Organized Materialized Views

Index-organized materialized views are subject to the following restrictions:

  * You cannot specify the following `CREATE` `MATERIALIZED` `VIEW` clauses: `CACHE` or `NOCACHE`, `CLUSTER`, or `ON` `PREBUILT` `TABLE`. 

  * In the `index_org_table_clause`: 

    * You cannot specify the `mapping_table_clause`. 

    * You can specify `COMPRESS` only for a materialized view based on a composite primary key. You can specify `NOCOMPRESS` for a materialized view based on either a simple or composite primary key. 

CLUSTER Clause

The `CLUSTER` clause lets you create the materialized view as part of the
specified cluster. A cluster materialized view uses the space allocation of
the cluster. Therefore, you do not specify physical attributes or the
`TABLESPACE` clause with the `CLUSTER` clause.

Restriction on Cluster Materialized Views

If you specify `CLUSTER`, then you cannot specify the
`table_partitioning_clauses` in `materialized_view_props`.

materialized_view_props

Use these property clauses to describe a materialized view that is not based
on an existing table. To create a materialized view that is based on an
existing table, use the `ON` `PREBUILT` `TABLE` clause.

column_properties

The `column_properties` clause lets you specify the storage characteristics of
a LOB, nested table, varray, or `XMLType` column. The
`object_type_col_properties` are not relevant for a materialized view.

See Also:

[CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6)
for detailed information about specifying the parameters of this clause

table_partitioning_clauses

The `table_partitioning_clauses` let you specify that the materialized view is
partitioned on specified ranges of values or on a hash function. Partitioning
of materialized views is the same as partitioning of tables.

See Also:

[table_partitioning_clauses](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2215406) in the `CREATE
TABLE` documentation

CACHE | NOCACHE

For data that will be accessed frequently, `CACHE` specifies that the blocks
retrieved for this table are placed at the most recently used end of the least
recently used (LRU) list in the buffer cache when a full table scan is
performed. This attribute is useful for small lookup tables. `NOCACHE`
specifies that the blocks are placed at the least recently used end of the LRU
list.

Note:

`NOCACHE` has no effect on materialized views for which you specify `KEEP` in
the `storage_clause`.

See Also:

[CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6)
for information about specifying `CACHE` or `NOCACHE`

parallel_clause

The `parallel_clause` lets you indicate whether parallel operations will be
supported for the materialized view and sets the default degree of parallelism
for queries and DML on the materialized view after creation.

For complete information on this clause, refer to [parallel_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) in the
documentation on `CREATE` `TABLE`.

build_clause

The `build_clause` lets you specify when to populate the materialized view.

IMMEDIATE

Specify `IMMEDIATE` to indicate that the materialized view is to be populated
immediately. This is the default.

DEFERRED

Specify `DEFERRED` to indicate that the materialized view is to be populated
by the next `REFRESH` operation. The first (deferred) refresh must always be a
complete refresh. Until then, the materialized view has a staleness value of
`UNUSABLE`, so it cannot be used for query rewrite.

USING INDEX Clause

The `USING` `INDEX` clause lets you establish the value of the `INITRANS` and
`STORAGE` parameters for the default index Oracle Database uses to maintain
the materialized view data. If `USING` `INDEX` is not specified, then default
values are used for the index. Oracle Database uses the default index to speed
up incremental (`FAST`) refresh of the materialized view.

Restriction on USING INDEX clause

You cannot specify the `PCTUSED` parameter in this clause.

USING NO INDEX Clause

Specify `USING` `NO` `INDEX` to suppress the creation of the default index.
You can create an alternative index explicitly by using the `CREATE` `INDEX`
statement. You should create such an index if you specify `USING` `NO` `INDEX`
and you are creating the materialized view with the fast refresh method
(`REFRESH` `FAST`).

create_mv_refresh

Use the `create_mv_refresh` clause to specify the default methods, modes, and
times for the database to refresh the materialized view. If the master tables
of a materialized view are modified, then the data in the materialized view
must be updated to make the materialized view accurately reflect the data
currently in its master tables. This clause lets you schedule the times and
specify the method and mode for the database to refresh the materialized view.

Restriction on Synchronous Refresh

If you are using the synchronous refresh method, then you must specify `ON`
`DEMAND` and `USING` `TRUSTED` `CONSTRAINTS`.

Note:

This clause only sets the default refresh options. For instructions on
actually implementing the refresh, refer to [Oracle Database Administratorâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-31E1E90D-C565-40EF-BD22-4DB2D13462AA) and
[Oracle Database Data Warehousing
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG015).

See Also:

  * "[Periodic Refresh of Materialized Views: Example](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2098290)" and "[Automatic Refresh Times for Materialized Views: Example](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2119766)"

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS027) for more information on refresh methods 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG-GUID-6AD8879A-0BE5-466E-8D19-1D076C5DDFFB) to learn how to use refresh statistics to monitor the performance of materialized view refresh operations 

FAST Clause

Specify `FAST` to indicate the fast refresh method, which performs the refresh
according to the changes that have occurred to the master tables. The changes
for conventional DML changes are stored in the materialized view log
associated with the master table. The changes for direct-path `INSERT`
operations are stored in the direct loader log.

If you specify `REFRESH` `FAST`, then the `CREATE` statement will fail unless
materialized view logs already exist for the materialized view master tables.
Oracle Database creates the direct loader log automatically when a direct-path
`INSERT` takes place. No user intervention is needed.

For both conventional DML changes and for direct-path `INSERT` operations,
other conditions may restrict the eligibility of a materialized view for fast
refresh.

Restrictions on FAST Refresh

`FAST` refresh is subject to the following restrictions:

  * When you specify `FAST` refresh at create time, Oracle Database verifies that the materialized view you are creating is eligible for fast refresh. When you change the refresh method to `FAST` in an `ALTER` `MATERIALIZED` `VIEW` statement, Oracle Database does not perform this verification. If the materialized view is not eligible for fast refresh, then Oracle Database returns an error when you attempt to refresh this view. 

  * Materialized views are not eligible for fast refresh if the defining query contains an analytic function or the `XMLTable` function. 

  * Materialized views are not eligible for fast refresh if the defining query references a table on which an `XMLIndex` index is defined. 

  * You cannot fast refresh a materialized view if any of its columns is encrypted.

See Also:

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-7B26829E-1389-46CF-81AD-28EA6C2F13A1) for restrictions on fast refresh in replication environments 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG015) for restrictions on fast refresh in data warehousing environments 

  * The `EXPLAIN_MVIEW` procedure of the [`DBMS_MVIEW`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS027) package for help diagnosing problems with fast refresh and the `TUNE_MVIEW` procedure of the [`DBMS_MVIEW`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS027) package for correction of query rewrite problems 

  * "[Analytic Functions](Analytic-Functions.md#GUID-527832F7-63C0-4445-8C16-307FA5084056)"

  * "[Creating a Fast Refreshable Materialized View: Example](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2080820)"

COMPLETE Clause

Specify `COMPLETE` to indicate the complete refresh method, which is
implemented by executing the defining query of the materialized view. If you
request a complete refresh, then Oracle Database performs a complete refresh
even if a fast refresh is possible.

FORCE Clause

Specify `FORCE` to indicate that when a refresh occurs, Oracle Database will
perform a fast refresh if one is possible or a complete refresh if fast
refresh is not possible. If you do not specify a refresh method (`FAST`,
`COMPLETE`, or `FORCE`), then `FORCE` is the default.

ON COMMIT Clause

Specify `ON` `COMMIT` to indicate that a refresh is to occur whenever the
database commits a transaction that operates on a master table of the
materialized view. This clause may increase the time taken to complete the
commit, because the database performs the refresh operation as part of the
commit process.

You can specify only one of the `ON` `COMMIT`, `ON` `DEMAND`, and `ON`
`STATEMENT` clauses. If you specify `ON` `COMMIT`, then you cannot also
specify `START` `WITH` or `NEXT`.

Restrictions on Refreshing ON COMMIT

The following restrictions apply to the `ON` `COMMIT` clause:

  * This clause is not supported for materialized views containing object types or Oracle-supplied types.

  * This clause is not supported for materialized views with remote tables.

  * If you specify this clause, then you cannot subsequently execute a distributed transaction on any master table of this materialized view. For example, you cannot insert into the master by selecting from a remote table. The `ON` `DEMAND` clause does not impose this restriction on subsequent distributed transactions on master tables. 

ON DEMAND Clause

Specify `ON` `DEMAND` to indicate that database will not refresh the
materialized view unless the user manually launches a refresh through one of
the three `DBMS_MVIEW` refresh procedures.

You can specify only one of the `ON` `COMMIT`, `ON` `DEMAND`, and `ON`
`STATEMENT` clauses. If you omit all three of these clauses, then `ON`
`DEMAND` is the default. You can override this default setting by specifying
the `START` `WITH` or `NEXT` clauses, either in the same `CREATE`
`MATERIALIZED` `VIEW` statement or a subsequent `ALTER` `MATERIALIZED` `VIEW`
statement.

`START` `WITH` and `NEXT` take precedence over `ON` `DEMAND`. Therefore, in
most circumstances it is not meaningful to specify `ON` `DEMAND` when you have
specified `START` `WITH` or `NEXT`.

See Also:

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS027) for information on these procedures 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG015) on the types of materialized views you can create by specifying `REFRESH` `ON` `DEMAND`

ON STATEMENT Clause

Specify `ON` `STATEMENT` to indicate that an automatic refresh is to occur
every time a DML operation is performed on any of the materialized view's base
tables.

You can specify only one of the `ON` `COMMIT`, `ON` `DEMAND`, and `ON`
`STATEMENT` clauses. You can specify `ON` `STATEMENT` only when creating a
materialized view. You cannot subsequently alter the materialized view to use
`ON` `STATEMENT` refresh.

Restrictions on Refreshing ON STATEMENT

The following restrictions apply to the `ON` `STATEMENT` clause:

  * This clause can be used only with materialized views that are fast refreshable. The `ON` `STATEMENT` clause must be specified with the `REFRESH` `FAST` clause. 

  * The base tables referenced in the materialized viewâs defining query must be connected in a join graph that uses the star schema or snowflake schema model. The query must contain exactly one centralized fact table and one or more dimension tables, with all pairs of joined tables being related using primary key-foreign key constraints.

    * There is no restriction on the depth of the snowflake model.

    * The constraints can be in `RELY` mode. However, you must include the `USING` `TRUSTED` `CONSTRAINT` clause while creating the materialized view to use the `RELY` constraint. 

  * The materialized viewâs defining query must include the `ROWID` column of the fact table. 

  * The materialized viewâs defining query cannot include any of the following: invisible columns, ANSI join syntax, complex query, inline view as base table, composite primary key, `LONG` columns, and LOB columns. 

  * You cannot alter the definition of an existing materialized view that uses the `ON` `STATEMENT` refresh mode. 

  * You cannot alter an existing materialized view and enable `ON` `STATEMENT` refresh for it. 

  * The following operations cause a materialized view with `ON` `STATEMENT` refresh to become unusable: 

    * `UPDATE` operations on one or more dimension tables on which the materialized view is based 

    * Partition maintenance operations and `TRUNCATE` operations on any base table 

However, a materialized view with the `ON` `STATEMENT` refresh mode can be
partitioned.

  * All the restrictions that apply to the `ON` `COMMIT` clause apply to `ON` `STATEMENT`. 

START WITH Clause

Specify a datetime expression for the first automatic refresh time.

NEXT Clause

Specify a datetime expression for calculating the interval between automatic
refreshes.

Both the `START` `WITH` and `NEXT` values must evaluate to a time in the
future. If you omit the `START` `WITH` value, then the database determines the
first automatic refresh time by evaluating the `NEXT` expression with respect
to the creation time of the materialized view. If you specify a `START` `WITH`
value but omit the `NEXT` value, then the database refreshes the materialized
view only once. If you omit both the `START` `WITH` and `NEXT` values, or if
you omit the `create_mv_refresh` entirely, then the database does not
automatically refresh the materialized view.

WITH PRIMARY KEY Clause

Specify `WITH PRIMARY` `KEY` to create a primary key materialized view. This
is the default and should be used in all cases except those described for
`WITH` `ROWID`. Primary key materialized views allow materialized view master
tables to be reorganized without affecting the eligibility of the materialized
view for fast refresh. The master table must contain an enabled primary key
constraint, and the defining query of the materialized view must specify all
of the primary key columns directly. In the defining query, the primary key
columns cannot be specified as the argument to a function such as `UPPER`.

Restriction on Primary Key Materialized Views

You cannot specify this clause for an object materialized view. Oracle
Database implicitly refreshes objects materialized `WITH` `OBJECT` `ID`.

See Also:

[Oracle Database Administratorâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-31D07B2A-4B42-4B26-BB6F-0BA90FC0FB0D) for
detailed information about primary key materialized views and "[Creating
Primary Key Materialized Views: Example](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2119730)"

WITH ROWID Clause

Specify `WITH` `ROWID` to create a rowid materialized view. Rowid materialized
views are useful if the materialized view does not include all primary key
columns of the master tables. Rowid materialized views must be based on a
single table and cannot contain any of the following:

  * Distinct or aggregate functions

  * `GROUP` `BY` `or` `CONNECT` `BY` clauses 

  * Subqueries

  * Joins

  * Set operations

The `WITH` `ROWID` clause has no effect if there are multiple master tables in
the defining query.

Rowid materialized views are not eligible for fast refresh after a master
table reorganization until a complete refresh has been performed.

Restriction on Rowid Materialized Views

You cannot specify this clause for an object materialized view. Oracle
Database implicitly refreshes objects materialized `WITH` `OBJECT` `ID`.

See Also:

"[Creating Materialized Aggregate Views: Example](CREATE-MATERIALIZED-
VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2092102)" and "[Creating
Rowid Materialized Views: Example](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2098291)"

USING ROLLBACK SEGMENT Clause

This clause is not valid if your database is in automatic undo mode, because
in that mode Oracle Database uses undo tablespaces instead of rollback
segments. Oracle strongly recommends that you use automatic undo mode. This
clause is supported for backward compatibility with replication environments
containing older versions of Oracle Database that still use rollback segments.

For `rollback_segment`, specify the remote rollback segment to be used during
materialized view refresh.

DEFAULT

`DEFAULT` specifies that Oracle Database will choose automatically which
rollback segment to use. If you specify `DEFAULT`, then you cannot specify
`rollback_segment`. `DEFAULT` is most useful when modifying, rather than
creating, a materialized view.

See Also:

[ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233)

MASTER

`MASTER` specifies the remote rollback segment to be used at the remote master
site for the individual materialized view.

LOCAL

`LOCAL` specifies the remote rollback segment to be used for the local refresh
group that contains the materialized view. This is the default.

See Also:

[Oracle Database PL/SQL Packages and Types
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ARPLS043) for information on specifying the local
materialized view rollback segment using the `DBMS_REFRESH` package

If you omit `rollback_segment`, then the database automatically chooses the
rollback segment to be used. One master rollback segment is stored for each
materialized view and is validated during materialized view creation and
refresh. If the materialized view is complex, then the database ignores any
master rollback segment you specify.

USING ... CONSTRAINTS Clause

The `USING` ... `CONSTRAINTS` clause lets Oracle Database choose more rewrite
options during the refresh operation, resulting in more efficient refresh
execution. The clause lets Oracle Database use unenforced constraints, such as
dimension relationships or constraints in the `RELY` state, rather than
relying only on enforced constraints during the refresh operation.

The `USING` `TRUSTED` `CONSTRAINTS` clause enables you to create a
materialized view on top of a table that has a non-NULL Virtual Private
Database (VPD) policy on it. In this case, you must ensure that the
materialized view behaves correctly. Materialized view results are computed
based on the rows and columns filtered by VPD policy. Therefore, you must
coordinate the materialized view definition with the VPD policy to ensure the
correct results. Without the `USING` `TRUSTED` `CONSTRAINTS` clause, any VPD
policy on a master table will prevent a materialized view from being created.

Note:

The `USING` `TRUSTED` `CONSTRAINTS` clause lets Oracle Database use dimension
and constraint information that has been declared trustworthy by the database
administrator but that has not been validated by the database. If the
dimension and constraint information is valid, then performance may improve.
However, if this information is invalid, then the refresh procedure may
corrupt the materialized view even though it returns a success status.

If you omit this clause, then the default is `USING` `ENFORCED` `CONSTRAINTS.`

NEVER REFRESH Clause

Specify `NEVER` `REFRESH` to prevent the materialized view from being
refreshed with any Oracle Database refresh mechanism or packaged procedure.
Oracle Database will ignore any `REFRESH` statement on the materialized view
issued from such a procedure. If you specify this clause, then you can perform
DML operations on the materialized view. To reverse this clause, you must
issue an `ALTER` `MATERIALIZED` `VIEW` ... `REFRESH` statement.

evaluation_edition_clause

You must specify this clause if `subquery` references an editioned object. Use
this clause to specify the edition that is searched during name resolution of
the editioned objectâthe evaluation edition.

  * Specify `CURRENT` `EDITION` to search the edition in which this DDL statement is executed. 

  * Specify `EDITION` `edition` to search `edition`. 

  * Specifying `NULL` `EDITION` is equivalent to omitting the `evaluation_edition_clause`. 

If you omit the `evaluation_edition_clause`, then editioned objects are
invisible during name resolution and an error will result. Dropping the
evaluation edition invalidates the materialized view.

See Also:

[Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS1326) for more information on specifying the
evaluation edition for a materialized view

{ ENABLE | DISABLE } ON QUERY COMPUTATION

This clause lets you create a real-time materialized view or a regular view. A
real-time materialized view provides fresh data to user queries even when the
materialized view is not in sync with its base tables due to data changes.
Instead of modifying the materialized view, the optimizer writes a query that
combines the existing rows in the materialized view with changes recorded in
log files (either materialized view logs or the direct loader logs). This is
called on-query computation.

  * Specify `ENABLE` `ON` `QUERY` `COMPUTATION` to create a real-time materialized view by enabling on-query computation. This allows you to directly query up-to-date data from the materialized view by specifying the `FRESH_MV` hint in the `SELECT` statement. If the materialized view is also enabled for query rewrite, then on-query computation occurs automatically during query rewrite. 

  * Specify `DISABLE` `ON` `QUERY` `COMPUTATION` to create a regular materialized view by disabling on-query computation. This is the default. 

Restrictions on Real-Time Materialized Views

Real-time materialized views are subject to the following restrictions:

  * Real-time materialized views cannot be used when one or more materialized view logs created on the base tables are either unusable or nonexistent.

  * A real-time materialized view must be refreshable using out-of-place refresh, log-based refresh, or partition change tracking (PCT) refresh.

  * A refresh-on-commit materialized view cannot be a real-time materialized view.

  * If a real-time materialized view is a nested materialized view that is defined on top of one or more base materialized views, then query rewrite occurs only if all the base materialized views are fresh. If one or more base materialized views are stale, then query rewrite is not performed using this real-time materialized view.

  * The cursors of queries that directly access real-time materialized views are not shared.

See Also:

  * [FRESH_MV Hint](Comments.md#GUID-5EF4198B-50B3-40D8-B12A-3D3115C69D9B)

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG-GUID-0702359B-D379-4299-86C4-2958BCD4381D) for more information on real-time materialized views 

query_rewrite_clause

The `query_rewrite_clause` lets you specify whether the materialized view is
eligible to be used for query rewrite.

ENABLE Clause

Specify `ENABLE` to enable the materialized view for query rewrite. If you
also specify the `unusable_editions_clause`, then the materialized view is not
enabled for query rewrite in the unusable editions.

Restrictions on Enabling Query Rewrite

Enabling of query rewrite is subject to the following restrictions:

  * You can enable query rewrite only if all user-defined functions in the materialized view are `DETERMINISTIC`. 

  * You can enable query rewrite only if expressions in the statement are repeatable. For example, you cannot include `CURRENT_TIME` or `USER`, sequence values (such as the `CURRVAL` or `NEXTVAL` pseudocolumns), or the `SAMPLE` clause (which may sample different rows as the contents of the materialized view change). 

Note:

  * Query rewrite is disabled by default, so you must specify this clause to make materialized views eligible for query rewrite.

  * After you create the materialized view, you must collect statistics on it using the `DBMS_STATS` package. Oracle Database needs the statistics generated by this package to optimize query rewrite. 

See Also:

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG018) for more information on query rewrite 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG-GUID-6AD8879A-0BE5-466E-8D19-1D076C5DDFFB) to learn how to use refresh statistics to monitor the performance of materialized view refresh operations 

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS059) for information about the `DBMS_STATS` package 

  * The `EXPLAIN_MVIEW` procedure of the [`DBMS_MVIEW`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS027) package for help diagnosing problems with query rewrite and the `TUNE_MVIEW` procedure of the [`DBMS_MVIEW`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS027) package for correction of query rewrite problems 

  * [CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306)

DISABLE Clause

Specify `DISABLE` to indicate that the materialized view is not eligible for
use by query rewrite. A disabled materialized view can be refreshed.

unusable_editions_clause

This clause lets you specify that the materialized view is not eligible for
query rewrite in one or more editions. You can specify this clause regardless
of whether you specify the `ENABLE` or `DISABLE` clause. If you specify the
`DISABLE` clause, then this clause will take effect if the materialized view
is subsequently enabled for query rewrite using the `ALTER` `MATERIALIZED`
`VIEW` ... `ENABLE` `QUERY` `REWRITE` statement.

UNUSABLE BEFORE Clause

This clause lets you specify that the materialized view is not eligible for
query rewrite in the ancestors of an edition.

  * If you specify `CURRENT` `EDITION`, then the materialized view is not eligible for query rewrite in the ancestors of the current edition. 

  * If you specify `EDITION` `edition`, then the materialized view is not eligible for query rewrite in the ancestors of the specified `edition`. 

UNUSABLE BEGINNING WITH Clause

This clause lets you specify that the materialized view is not eligible for
query rewrite in an edition and its descendants.

  * If you specify `CURRENT` `EDITION`, then the materialized view is not eligible for query rewrite in the current edition and its descendants. 

  * If you specify `EDITION` `edition`, then the materialized view is not eligible for query rewrite in the specified edition and its descendants. 

  * Specifying `NULL` `EDITION` is equivalent to omitting the `UNUSABLE` `BEGINNING` `WITH` clause. 

The materialized view has a dependency on each edition in which it is not
eligible for query rewrite. If such an edition is subsequently dropped, then
the dependency is removed. However, the materialized view is not invalidated.

ENABLE | DISABLE CONCURRENT REFRESH 

Enable concurrent refresh to refresh the same on-commit atomic materialized
view across multiple sessions concurrently. The materialized view is refreshed
concurrently when multiple concurrent DML transactions on the same base table
of the materialized view are committed.

There are no limitations on how many materialized views can be refreshed.

Concurrent refresh is disabled by default. You must explictly enable it on the
materialized view. Note that you can enable it only on on-commit materialized
views.

See Also:

[Refreshing Materialized
Views](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG-GUID-64068234-BDB0-4C12-AE70-75571046A586) of the
Oracle Database Data Warehousing Guide.

AS subquery

Specify the defining query of the materialized view. When you create the
materialized view, Oracle Database executes this subquery and places the
results in the materialized view. This subquery is any valid SQL subquery.
However, not all subqueries are fast refreshable, nor are all subqueries
eligible for query rewrite.

Notes on the Defining Query of a Materialized View

The following notes apply to materialized views:

  * Oracle Database does not execute the defining query immediately if you specify `BUILD` `DEFERRED`. 

  * Oracle recommends that you qualify each table and view in the `FROM` clause of the defining query of the materialized view with the schema containing it. 

  * In order to create a materialized view whose defining query selects from a master table that has a Virtual Private Database (VPD) policy, you must specify the `REFRESH` `USING` `TRUSTED` `CONSTRAINTS` clause. 

Restrictions on the Defining Query of a Materialized View

The materialized view query is subject to the following restrictions:

  * The defining query of a materialized view can select from tables, views, or materialized views owned by the user `SYS`, but you cannot enable `QUERY` `REWRITE` on such a materialized view. 

  * The defining query of a materialized view cannot select from a `V$` view or a `GV$` view. 

  * You cannot define a materialized view with a subquery in the select list of the defining query. You can, however, include subqueries elsewhere in the defining query, such as in the `WHERE` clause. 

  * You cannot use the `AS` `OF` clause of the `flashback_query_clause` in the defining query of a materialized view. 

  * Materialized join views and materialized aggregate views with a `GROUP` `BY` clause cannot select from an index-organized table. 

  * Materialized views cannot contain columns of data type `LONG` or `LONG` `RAW`. 

  * Materialized views cannot contain virtual columns.

  * You cannot create a materialized view log on a temporary table. Therefore, if the defining query references a temporary table, then this materialized view will not be eligible for `FAST` refresh, nor can you specify the `QUERY` `REWRITE` clause in this statement. 

  * If the `FROM` clause of the defining query references another materialized view, then you must always refresh the materialized view referenced in the defining query before refreshing the materialized view you are creating in this statement. 

  * Materialized views with join expressions in the defining query cannot have XML data type columns. The XML data types include `XMLType` and URI data type columns. 

If you are creating a materialized view enabled for query rewrite, then:

  * The defining query cannot contain, either directly or through a view, references to `ROWNUM`, `USER`, `SYSDATE`, remote tables, sequences, or PL/SQL functions that write or read database or package state. 

  * Neither the materialized view nor the master tables of the materialized view can be remote.

If you want the materialized view to be eligible for fast refresh using a
materialized view log, or synchronous refresh using a staging log, then some
additional restrictions apply.

See Also:

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG029) for restrictions relating to using [fast refresh](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG8201) and synchronous refresh 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-EF9222CE-A090-4D71-9B94-15B6034F48D6)for more information on restrictions relating to replication 

  * "[Creating Materialized Join Views: Example](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2119687)", "[Creating Subquery Materialized Views: Example](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2119713)", and "[Creating a Nested Materialized View: Example](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2119822)"

Examples

The following examples require the materialized logs that are created in the
"Examples" section of [CREATE MATERIALIZED VIEW LOG](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B).

Creating a Simple Materialized View: Example

The following statement creates a very simple materialized view based on the
`employees` and table in the `hr` schema:

    
    
    CREATE MATERIALIZED VIEW mv1 AS SELECT * FROM hr.employees;
    

By default, Oracle Database creates a primary key materialized view with
refresh on demand only. If a materialized view log exists on `employees`, then
`mv1` can be altered to be capable of fast refresh. If no such log exists,
then only full refresh of `mv1` is possible. Oracle Database uses default
storage properties for `mv1`. The only privileges required for this operation
are the `CREATE` `MATERIALIZED` `VIEW` system privilege, and the `READ` or
`SELECT` object privilege on `hr`.`employees`.

Creating Subquery Materialized Views: Example

The following statement creates a subquery materialized view based on the
`customers` and `countries` tables in the `sh` schema at the `remote`
database:

    
    
    CREATE MATERIALIZED VIEW foreign_customers
       AS SELECT * FROM sh.customers@remote cu
       WHERE EXISTS
         (SELECT * FROM sh.countries@remote co
          WHERE co.country_id = cu.country_id);

Creating Materialized Aggregate Views: Example

The following statement creates and populates a materialized aggregate view on
the sample `sh.sales` table and specifies the default refresh method, mode,
and time. It uses the materialized view log created in "[Creating a
Materialized View Log for Fast Refresh: Examples](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2098404)", as well as the
two additional logs shown here:

    
    
    CREATE MATERIALIZED VIEW LOG ON times
       WITH ROWID, SEQUENCE (time_id, calendar_year)
       INCLUDING NEW VALUES;
    
    CREATE MATERIALIZED VIEW LOG ON products
       WITH ROWID, SEQUENCE (prod_id)
       INCLUDING NEW VALUES;
    
    CREATE MATERIALIZED VIEW sales_mv
       BUILD IMMEDIATE
       REFRESH FAST ON COMMIT
       AS SELECT t.calendar_year, p.prod_id, 
          SUM(s.amount_sold) AS sum_sales
          FROM times t, products p, sales s
          WHERE t.time_id = s.time_id AND p.prod_id = s.prod_id
          GROUP BY t.calendar_year, p.prod_id;

Creating Materialized Join Views: Example

The following statement creates and populates the materialized aggregate view
`sales_by_month_by_state` using tables in the sample `sh` schema. The
materialized view will be populated with data as soon as the statement
executes successfully. By default, subsequent refreshes will be accomplished
by reexecuting the defining query of the materialized view:

    
    
    CREATE MATERIALIZED VIEW sales_by_month_by_state
         TABLESPACE example
         PARALLEL 4
         BUILD IMMEDIATE
         REFRESH COMPLETE
         ENABLE QUERY REWRITE
         AS SELECT t.calendar_month_desc, c.cust_state_province,
            SUM(s.amount_sold) AS sum_sales
            FROM times t, sales s, customers c
            WHERE s.time_id = t.time_id AND s.cust_id = c.cust_id
            GROUP BY t.calendar_month_desc, c.cust_state_province;

Creating Prebuilt Materialized Views: Example

The following statement creates a materialized aggregate view for the
preexisting summary table, `sales_sum_table`:

    
    
    CREATE TABLE sales_sum_table
       (month VARCHAR2(8), state VARCHAR2(40), sales NUMBER(10,2));
    
    CREATE MATERIALIZED VIEW sales_sum_table
       ON PREBUILT TABLE WITH REDUCED PRECISION
       ENABLE QUERY REWRITE
       AS SELECT t.calendar_month_desc AS month, 
                 c.cust_state_province AS state,
                 SUM(s.amount_sold) AS sales
          FROM times t, customers c, sales s
          WHERE s.time_id = t.time_id AND s.cust_id = c.cust_id
          GROUP BY t.calendar_month_desc, c.cust_state_province;
    

In the preceding example, the materialized view has the same name and also has
the same number of columns with the same data types as the prebuilt table. The
`WITH` `REDUCED` `PRECISION` clause allows for differences between the
precision of the materialized view columns and the precision of the values
returned by the subquery.

Creating Primary Key Materialized Views: Example

The following statement creates the primary key materialized view `catalog` on
the sample table `oe.product_information`:

    
    
    CREATE MATERIALIZED VIEW catalog   
       REFRESH FAST START WITH SYSDATE NEXT SYSDATE + 1/4096 
       WITH PRIMARY KEY 
       AS SELECT * FROM product_information;  

Creating Rowid Materialized Views: Example

The following statement creates a rowid materialized view on the sample table
`oe.orders`:

    
    
    CREATE MATERIALIZED VIEW order_data REFRESH WITH ROWID 
       AS SELECT * FROM orders; 

Periodic Refresh of Materialized Views: Example

The following statement creates the primary key materialized view `emp_data`
and populates it with data from the sample table `hr.employees`:

    
    
    CREATE MATERIALIZED VIEW LOG ON employees
       WITH PRIMARY KEY
       INCLUDING NEW VALUES;
    
    CREATE MATERIALIZED VIEW emp_data 
       PCTFREE 5 PCTUSED 60 
       TABLESPACE example 
       STORAGE (INITIAL 50K)
       REFRESH FAST NEXT sysdate + 7 
       AS SELECT * FROM employees; 
    

The preceding statement does not include a `START` `WITH` parameter, so Oracle
Database determines the first automatic refresh time by evaluating the `NEXT`
value using the current `SYSDATE`. A materialized view log was created for the
employee table, so Oracle Database performs a fast refresh of the materialized
view every 7 days, beginning 7 days after the materialized view is created.

Because the materialized view conforms to the conditions for fast refresh, the
database will perform a fast refresh. The preceding statement also establishes
storage characteristics that the database uses to maintain the materialized
view.

Automatic Refresh Times for Materialized Views: Example

The following statement creates the complex materialized view `all_customers`
that queries the employee tables on the `remote` and `local` databases:

    
    
    CREATE MATERIALIZED VIEW all_customers
       PCTFREE 5 PCTUSED 60 
       TABLESPACE example 
       STORAGE (INITIAL 50K) 
       USING INDEX STORAGE (INITIAL 25K)
       REFRESH START WITH ROUND(SYSDATE + 1) + 11/24 
       NEXT NEXT_DAY(TRUNC(SYSDATE), 'MONDAY') + 15/24 
       AS SELECT * FROM sh.customers@remote 
             UNION
          SELECT * FROM sh.customers@local; 
    

Oracle Database automatically refreshes this materialized view tomorrow at
11:00 a.m. and subsequently every Monday at 3:00 p.m. The default refresh
method is `FORCE`. The defining query contains a `UNION` operator, which is
not supported for fast refresh, so the database will automatically perform a
complete refresh.

The preceding statement also establishes storage characteristics for both the
materialized view and the index that the database uses to maintain it:

  * The first `STORAGE` clause establishes the sizes of the first and second extents of the materialized view as 50 kilobytes each. 

  * The second `STORAGE` clause, appearing with the `USING` `INDEX` clause, establishes the sizes of the first and second extents of the index as 25 kilobytes each. 

Creating a Fast Refreshable Materialized View: Example

The following statement creates a fast-refreshable materialized view that
selects columns from the `order_items` table in the sample `oe` schema, using
the `UNION` set operator to restrict the rows returned from the
`product_information` and `inventories` tables using `WHERE` conditions. The
materialized view logs for `order_items` and `product_information` were
created in the "[Examples](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2064930)" section of
`CREATE` `MATERIALIZED` `VIEW` `LOG`. This example also requires a
materialized view log on `oe.inventories`.

    
    
    CREATE MATERIALIZED VIEW LOG ON inventories
       WITH (quantity_on_hand);
    
    CREATE MATERIALIZED VIEW warranty_orders REFRESH FAST AS
      SELECT order_id, line_item_id, product_id FROM order_items o
        WHERE EXISTS
        (SELECT * FROM inventories i WHERE o.product_id = i.product_id
          AND i.quantity_on_hand IS NOT NULL)
      UNION
        SELECT order_id, line_item_id, product_id FROM order_items
        WHERE quantity > 5; 
    

The materialized view `warranty_orders` requires that materialized view logs
be defined on `order_items` (with `product_id` as a join column) and on
inventories (with `quantity_on_hand` as a filter column). See "[Specifying
Filter Columns for Materialized View Logs: Example](CREATE-MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2098358)" and
"[Specifying Join Columns for Materialized View Logs: Example](CREATE-
MATERIALIZED-VIEW-
LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B__I2098379)".

Creating a Nested Materialized View: Example

The following example uses the materialized view from the preceding example as
a master table to create a materialized view tailored for a particular sales
representative in the sample `oe` schema:

    
    
    CREATE MATERIALIZED VIEW my_warranty_orders
       AS SELECT w.order_id, w.line_item_id, o.order_date
       FROM warranty_orders w, orders o
       WHERE o.order_id = o.order_id
       AND o.sales_rep_id = 165; 

Specify Annotations at the View Level

The following example adds annotations `Title` value `Tab1 MV1` and `Snapshot`
without a value to the materialized view `MView1`:

    
    
    CREATE MATERIALIZED VIEW MView1 ANNOTATIONS (Title 'Tab1 MV1', ADD Snapshot) AS SELECT * from Table1;
    

Specify Annotations at the View and Column Level

The following example adds `Hidden` to column `T`, `Title` with value `Tab1
MV1`, and `Snapshot` without a value to the materialized view `MView1` :

    
    
    CREATE MATERIALIZED VIEW MView1(T ANNOTATIONS (Hidden)) ANNOTATIONS (Title 'Tab1 MV1', ADD Snapshot) 
       AS SELECT * from Table1;
    


[← Previous](create-logical-partition-tracking.md)

[Next →](CREATE-MATERIALIZED-VIEW-LOG.md)
