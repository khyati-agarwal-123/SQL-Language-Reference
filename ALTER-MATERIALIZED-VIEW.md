[Previous](ALTER-LOCKDOWN-PROFILE.md) [Next](ALTER-MATERIALIZED-VIEW-
LOG.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ALTER LIBRARY to ALTER SESSION](SQL-Statements-ALTER-LIBRARY-to-ALTER-SESSION.md)
  3. ALTER MATERIALIZED VIEW 

## ALTER MATERIALIZED VIEW

Purpose

A materialized view is a database object that contains the results of a query.
The `FROM` clause of the query can name tables, views, and other materialized
views. Collectively these source objects are called master tables (a
replication term) or detail tables (a data warehousing term). This reference
uses the term master tables for consistency. The databases containing the
master tables are called the master databases.

Use the `ALTER` `MATERIALIZED` `VIEW` statement to modify an existing
materialized view in one or more of the following ways:

  * To change its storage characteristics

  * To change its refresh method, mode, or time

  * To alter its structure so that it is a different type of materialized view

  * To enable or disable query rewrite

Note:

The keyword `SNAPSHOT` is supported in place of `MATERIALIZED` `VIEW` for
backward compatibility.

See Also:

  * [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B) for more information on creating materialized views 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-A422B474-4BED-4A60-AEDB-E93630746083) for information on materialized views in a replication environment 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG008) for information on materialized views in a data warehousing environment 

Prerequisites

The materialized view must be in your own schema, or you must have the `ALTER`
`ANY` `MATERIALIZED` `VIEW` system privilege.

To enable a materialized view for query rewrite:

  * If all of the master tables in the materialized view are in your schema, then you must have the `QUERY` `REWRITE` privilege. 

  * If any of the master tables are in another schema, then you must have the `GLOBAL` `QUERY` `REWRITE` privilege. 

  * If the materialized view is in another user's schema, then both you and the owner of that schema must have the appropriate `QUERY` `REWRITE` privilege, as described in the preceding two items. In addition, the owner of the materialized view must have `SELECT` access to any master tables that the materialized view owner does not own. 

To specify an edition in the `evaluation_edition_clause` or the
`unusable_editions_clause`, you must have the `USE` privilege on the edition.

Syntax

alter_materialized_view::=

![Description of alter_materialized_view.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_materialized_view.gif)  
[Description of the illustration
alter_materialized_view.eps](img_text/alter_materialized_view.md)

([physical_attributes_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226135),
[modify_mv_column_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBHEFGD),
[table_compression::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226151),
[inmemory_table_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBGHBAD),
[LOB_storage_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226161),
[modify_LOB_storage_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226189),
[alter_table_partitioning::=](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2087440) (part of
`ALTER` `TABLE`), [parallel_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2295551),
[logging_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226238),
[allocate_extent_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226245),
[deallocate_unused_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226254),
[shrink_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBBHABC),
[alter_iot_clauses::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2233183),
[scoped_table_ref_constraint::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__CCHJJHEC),
[alter_mv_refresh::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2233205),
[evaluation_edition_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__CCHCFCEH),
[alter_query_rewrite_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__CCHCAFJB),
[annotations_clause](annotations_clause.md#GUID-1AC16117-BBB6-4435-8794-2B99F8F68052))

physical_attributes_clause::=

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB))

modify_mv_column_clause::=

![Description of modify_mv_column_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/modify_mv_column_clause.gif)  
[Description of the illustration
modify_mv_column_clause.eps](img_text/modify_mv_column_clause.md)

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

([inmemory_attributes::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBFJIIJ),
[inmemory_column_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBGJGGE))

inmemory_attributes::=

![Description of inmemory_attributes.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/inmemory_attributes.gif)  
[Description of the illustration
inmemory_attributes.eps](img_text/inmemory_attributes.md)

([inmemory_memcompress::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBJFGIE),
[inmemory_priority::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBDEIHD),
[inmemory_distribute::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBFJEID),
[inmemory_duplicate::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBHHAHA))

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

([inmemory_memcompress::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBJFGIE))

LOB_storage_clause::=

![Description of lob_storage_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lob_storage_clause.gif)  
[Description of the illustration
lob_storage_clause.eps](img_text/lob_storage_clause.md)

([LOB_storage_parameters::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BABEIHJF))

LOB_storage_parameters::=

![Description of lob_storage_parameters.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lob_storage_parameters.gif)  
[Description of the illustration
lob_storage_parameters.eps](img_text/lob_storage_parameters.md)

(`TABLESPACE` `SET`: not supported with `ALTER` `MATERIALIZED` `VIEW`,
[LOB_parameters::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BABFCFDI),
[storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB))

LOB_parameters::=

![Description of lob_parameters.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/lob_parameters.gif)  
[Description of the illustration
lob_parameters.eps](img_text/lob_parameters.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB),
[logging_clause::=](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E__CJAHABGF))

modify_LOB_storage_clause::=

![Description of modify_lob_storage_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/modify_lob_storage_clause.gif)  
[Description of the illustration
modify_lob_storage_clause.eps](img_text/modify_lob_storage_clause.md)

([modify_LOB_parameters::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2295516))

modify_LOB_parameters::=

![Description of modify_lob_parameters.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/modify_lob_parameters.gif)  
[Description of the illustration
modify_lob_parameters.eps](img_text/modify_lob_parameters.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB),
[LOB_retention_clause::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__BABEBCJJ),
[LOB_compression_clause::=](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__BABFHIFJ),
[logging_clause::=](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E__CJAHABGF),
[allocate_extent_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226245),
[shrink_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBBHABC),
[deallocate_unused_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226254))

parallel_clause::=

![Description of parallel_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_clause.gif)  
[Description of the illustration
parallel_clause.eps](img_text/parallel_clause.md)

logging_clause::=

![Description of logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logging_clause.gif)  
[Description of the illustration
logging_clause.eps](img_text/logging_clause.md)

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

shrink_clause::=

![Description of shrink_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/shrink_clause.gif)  
[Description of the illustration
shrink_clause.eps](img_text/shrink_clause.md)

annotations_clause::=

  

![Description of annotations_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/annotations_clause.gif)  
[Description of the illustration
annotations_clause.eps](img_text/annotations_clause.md)

  

annotations_list::=

  

![Description of annotations_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/annotations_list.gif)  
[Description of the illustration
annotations_list.eps](img_text/annotations_list.md)

  

annotation::=

  

![Description of annotation.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/annotation.gif)  
[Description of the illustration annotation.eps](img_text/annotation.md)

  

annotation_name::=

  

![Description of annotation_name.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/annotation_name.gif)  
[Description of the illustration
annotation_name.eps](img_text/annotation_name.md)

  

annotation_value::=

  

![Description of annotation_value.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/annotation_value.gif)  
[Description of the illustration
annotation_value.eps](img_text/annotation_value.md)

  

alter_iot_clauses::=

![Description of alter_iot_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_iot_clauses.gif)  
[Description of the illustration
alter_iot_clauses.eps](img_text/alter_iot_clauses.md)

([index_org_table_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226281),
[alter_overflow_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226300),
`alter_mapping_table_clauses`: not supported with materialized views)

index_org_table_clause::=

![Description of index_org_table_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/index_org_table_clause.gif)  
[Description of the illustration
index_org_table_clause.eps](img_text/index_org_table_clause.md)

(`mapping_table_clause`: not supported with materialized views,
`prefix_compression`: not supported for altering materialized views,
[index_org_overflow_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226294))

index_org_overflow_clause::=

![Description of index_org_overflow_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/index_org_overflow_clause.gif)  
[Description of the illustration
index_org_overflow_clause.eps](img_text/index_org_overflow_clause.md)

([segment_attributes_clause::=](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2085649)âpart of
`ALTER` `TABLE`)

alter_overflow_clause::=

![Description of alter_overflow_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_overflow_clause.gif)  
[Description of the illustration
alter_overflow_clause.eps](img_text/alter_overflow_clause.md)

([allocate_extent_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226245),
[shrink_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__BGBBHABC),
[deallocate_unused_clause::=](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226254))

add_overflow_clause::=

![Description of add_overflow_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_overflow_clause.gif)  
[Description of the illustration
add_overflow_clause.eps](img_text/add_overflow_clause.md)

([segment_attributes_clause::=](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2085649)\--part of
`ALTER` `TABLE`)

scoped_table_ref_constraint::=

![Description of scoped_table_ref_constraint.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/scoped_table_ref_constraint.gif)  
[Description of the illustration
scoped_table_ref_constraint.eps](img_text/scoped_table_ref_constraint.md)

alter_mv_refresh::=

![Description of alter_mv_refresh.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_mv_refresh.gif)  
[Description of the illustration
alter_mv_refresh.eps](img_text/alter_mv_refresh.md)

evaluation_edition_clause::=

![Description of evaluation_edition_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/evaluation_edition_clause.gif)  
[Description of the illustration
evaluation_edition_clause.eps](img_text/evaluation_edition_clause.md)

alter_query_rewrite_clause::=

![Description of alter_query_rewrite_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_query_rewrite_clause.gif)  
[Description of the illustration
alter_query_rewrite_clause.eps](img_text/alter_query_rewrite_clause.md)

Note:

You cannot specify only `QUERY` `REWRITE`. You must specify at least one of
the following: `ENABLE`, `DISABLE`, or a subclause of the
`unusable_editions_clause`.

unusable_editions_clause::=

![Description of unusable_editions_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/unusable_editions_clause.gif)  
[Description of the illustration
unusable_editions_clause.eps](img_text/unusable_editions_clause.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to alter an existing materialized view.

Specifying `IF NOT EXISTS` with `ALTER VIEW` results in `ORA-11544: Incorrect
IF EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the materialized view. If you omit `schema`,
then Oracle Database assumes the materialized view is in your own schema.

materialized_view

Specify the name of the materialized view to be altered.

physical_attributes_clause

Specify new values for the `PCTFREE`, `PCTUSED`, and `INITRANS` parameters
(or, when used in the `USING` `INDEX` clause, for the `INITRANS` parameter
only) and the storage characteristics for the materialized view. Refer to
[ALTER TABLE](ALTER-TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877) for
information on the `PCTFREE`, `PCTUSED`, and `INITRANS` parameters and to
[storage_clause](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393__I1026834)
for information about storage characteristics.

modify_mv_column_clause

Use this clause to encrypt or decrypt this column of the materialized view.
Refer to the `CREATE` `TABLE` clause [encryption_spec](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__CEGDFHBD) for
information on this clause.

table_compression

Use the `table_compression` clause to instruct Oracle Database whether to
compress data segments to reduce disk and memory use. Refer to the
[table_compression](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2128733) clause of
`CREATE` `TABLE` for the full semantics of this clause.

inmemory_table_clause

Use the `inmemory_table_clause` to enable or disable the materialized view or
its columns for the In-Memory Column Store (IM column store), or to change the
In-Memory attributes for the materialized view or its columns. This clause has
the same semantics here as it has for the `ALTER` `TABLE` statement. Refer to
the [inmemory_table_clause](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__CIHJBAJD) of `ALTER`
`TABLE` for the full semantics of this clause.

LOB_storage_clause

The `LOB_storage_clause` lets you specify the storage characteristics of a new
LOB. LOB storage behaves for materialized views exactly as it does for tables.
Refer to the [LOB_storage_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2128940) (in `CREATE`
`TABLE`) for information on the LOB storage parameters.

modify_LOB_storage_clause

The `modify_LOB_storage_clause` lets you modify the physical attributes of the
LOB attribute `LOB_item` or the LOB object attribute. Modification of LOB
storage behaves for materialized views exactly as it does for tables.

See Also:

The [modify_LOB_storage_clause](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2103804) of `ALTER`
`TABLE` for information on the LOB storage parameters that can be modified

alter_table_partitioning

The syntax and general functioning of the partitioning clauses for
materialized views is the same as for partitioned tables. Refer to
[alter_table_partitioning](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2085640) in the
documentation on `ALTER` `TABLE`.

Restriction on Altering Materialized View Partitions

You cannot specify the `LOB_storage_clause` or `modify_LOB_storage_clause`
within any of the `partitioning_clauses`.

Note:

If you want to keep the contents of the materialized view synchronized with
those of the master table, then Oracle recommends that you manually perform a
complete refresh of all materialized views dependent on the table after
dropping or truncating a table partition.

MODIFY PARTITION UNUSABLE LOCAL INDEXES

Use this clause to mark `UNUSABLE` all the local index partitions associated
with `partition`.

MODIFY PARTITION REBUILD UNUSABLE LOCAL INDEXES

Use this clause to rebuild the unusable local index partitions associated with
`partition`.

parallel_clause

The `parallel_clause` lets you change the default degree of parallelism for
the materialized view.

For complete information on this clause, refer to [parallel_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2159323) in the
documentation on `CREATE` `TABLE`.

logging_clause

Specify or change the logging characteristics of the materialized view. Refer
to the
[logging_clause](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E)
for a full description of this clause.

allocate_extent_clause

The `allocate_extent_clause` lets you explicitly allocate a new extent for the
materialized view. Refer to the
[allocate_extent_clause](allocate_extent_clause.md#GUID-
DA6B3DC2-84B5-4404-AD96-5ABF7341580F) for a full description of this clause.

deallocate_unused_clause

Use the `deallocate_unused_clause` to explicitly deallocate unused space at
the end of the materialized view and make the freed space available for other
segments. Refer to the
[deallocate_unused_clause](deallocate_unused_clause.md#GUID-016A106B-47D4-4FFF-8A3B-2DF19A5FE9FF)
for a full description of this clause.

shrink_clause

Use this clause to compact the materialized view segments. For complete
information on this clause, refer to [shrink_clause](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2192484) in the
documentation on `CREATE` `TABLE`.

CACHE | NOCACHE

For data that will be accessed frequently, `CACHE` specifies that the blocks retrieved for this table are placed at the most recently used end of the LRU list in the buffer cache when a full table scan is performed. This attribute is useful for small lookup tables. `NOCACHE` specifies that the blocks are placed at the least recently used end of the LRU list. Refer to "[CACHE | NOCACHE | CACHE READS](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__I2215507)" in the documentation on `CREATE` `TABLE` for more information about this clause. 

annotations_clause

The `annotation_name` is an identifier that can have up to 4000 characters. If
the annotation name is a reserved word it must be provided in double quotes.
When a double quoted identifier is used, the identifier can also contain
whitespace characters. However, identifiers that contain only whitespace
characters are not accepted.

You can only change annotations at the view level with the `ALTER` statement.
To drop column-level annotations, you must drop and recreate the view.

For the full semantics of the annotations clause see
[annotations_clause](CREATE-
TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6__SECTION_YPF_1B5_NVB) of
`CREATE TABLE`.

alter_iot_clauses

Use the `alter_iot_clauses` to change the characteristics of an index-
organized materialized view. The keywords and parameters of the components of
the `alter_iot_clauses` have the same semantics as in `ALTER` `TABLE`, with
the restrictions that follow.

Restrictions on Altering Index-Organized Materialized Views

You cannot specify the `mapping_table_clause` or the `prefix_compression`
clause of the `index_org_table_clause`.

See Also:

[index_org_table_clause](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2105365) of `CREATE` `MATERIALIZED`
`VIEW` for information on creating an index-organized materialized view

USING INDEX Clause

Use this clause to change the value of `INITRANS` and `STORAGE` parameters for
the index Oracle Database uses to maintain the materialized view data.

Restriction on the USING INDEX clause

You cannot specify the `PCTUSED` or `PCTFREE` parameters in this clause.

MODIFY scoped_table_ref_constraint

Use the `MODIFY` `scoped_table_ref_constraint` clause to rescope a `REF`
column or attribute to a new table or to an alias for a new column.

Restrictions on Rescoping REF Columns

You can rescope only one `REF` column or attribute in each `ALTER`
`MATERIALIZED` `VIEW` statement, and this must be the only clause in this
statement.

alter_mv_refresh

Use the `alter_mv_refresh` clause to change the default method and mode and
the default times for automatic refreshes. If the contents of the master
tables of a materialized view are modified, then the data in the materialized
view must be updated to make the materialized view accurately reflect the data
currently in its master table(s). This clause lets you schedule the times and
specify the method and mode for Oracle Database to refresh the materialized
view.

See Also:

  * This clause only sets the default refresh options. For instructions on actually implementing the refresh, refer to [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-31E1E90D-C565-40EF-BD22-4DB2D13462AA) and [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG015). 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG-GUID-6AD8879A-0BE5-466E-8D19-1D076C5DDFFB) to learn how to use refresh statistics to monitor the performance of materialized view refresh operations 

FAST Clause

Specify `FAST` for the fast refresh method, which performs the refresh
according to the changes that have occurred to the master tables. The changes
are stored either in the materialized view log associated with the master
table (for conventional DML changes) or in the direct loader log (for direct-
path `INSERT` operations).

For both conventional DML changes and for direct-path `INSERT` operations,
other conditions may restrict the eligibility of a materialized view for fast
refresh.

When you change the refresh method to `FAST` in an `ALTER` `MATERIALIZED`
`VIEW` statement, Oracle Database does not perform this verification. If the
materialized view is not eligible for fast refresh, then Oracle Database
returns an error when you attempt to refresh this view.

See Also:

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-7B26829E-1389-46CF-81AD-28EA6C2F13A1) for restrictions on fast refresh in replication environments 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG015) for restrictions on fast refresh in data warehouse environments 

  * "[Automatic Refresh: Examples](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226830)"

COMPLETE Clause

Specify `COMPLETE` for the complete refresh method, which is implemented by
executing the defining query of the materialized view. If you specify a
complete refresh, then Oracle Database performs a complete refresh even if a
fast refresh is possible.

See Also:

"[Complete Refresh: Example](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226866)"

FORCE Clause

Specify `FORCE` if, when a refresh occurs, you want Oracle Database to perform
a fast refresh if one is possible or a complete refresh otherwise.

ON COMMIT Clause

Specify `ON` `COMMIT` if you want a refresh to occur whenever Oracle Database
commits a transaction that operates on a master table of the materialized
view.

You cannot specify both `ON` `COMMIT` and `ON` `DEMAND`. If you specify `ON`
`COMMIT`, then you cannot also specify `START` `WITH` or `NEXT`.

Restriction on ON COMMIT

This clause is supported only for materialized join views and single-table
materialized aggregate views.

ON DEMAND Clause

Specify `ON` `DEMAND` if you want the materialized view to be refreshed on
demand by calling one of the three `DBMS_MVIEW` refresh procedures. If you
omit both `ON` `COMMIT` and `ON` `DEMAND`, then `ON` `DEMAND` is the default.

You cannot specify both `ON` `COMMIT` and `ON` `DEMAND`. `START` `WITH` and
`NEXT` take precedence over `ON` `DEMAND`. Therefore, in most circumstances it
is not meaningful to specify `ON` `DEMAND` when you have specified `START`
`WITH` or `NEXT`.

See Also:

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS027) for information on these procedures 

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG015) on the types of materialized views you can create by specifying `REFRESH` `ON` `DEMAND`

START WITH Clause

Specify `START` `WITH` `date` to indicate a date for the first automatic
refresh time.

NEXT Clause

Specify `NEXT` to indicate a date expression for calculating the interval
between automatic refreshes.

Both the `START` `WITH` and `NEXT` values must evaluate to a time in the
future. If you omit the `START` `WITH` value, then Oracle Database determines
the first automatic refresh time by evaluating the `NEXT` expression with
respect to the creation time of the materialized view. If you specify a
`START` `WITH` value but omit the `NEXT` value, then Oracle Database refreshes
the materialized view only once. If you omit both the `START` `WITH` and
`NEXT` values, or if you omit the `alter_mv_refresh` entirely, then Oracle
Database does not automatically refresh the materialized view.

WITH PRIMARY KEY Clause

Specify `WITH` `PRIMARY` `KEY` to change a rowid materialized view to a
primary key materialized view. Primary key materialized views allow
materialized view master tables to be reorganized without affecting the
ability of the materialized view to continue to fast refresh.

For you to specify this clause, the master table must contain an enabled
primary key constraint and must have defined on it a materialized view log
that logs primary key information.

See Also:

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-31D07B2A-4B42-4B26-BB6F-0BA90FC0FB0D) for detailed information about primary key materialized views 

  * "[Primary Key Materialized View: Example](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226895)"

USING ROLLBACK SEGMENT Clause

This clause is not valid if your database is in automatic undo mode, because
in that mode Oracle Database uses undo tablespaces instead of rollback
segments. Oracle strongly recommends that you use automatic undo mode. This
clause is supported for backward compatibility with replication environments
containing older versions of Oracle Database that still use rollback segments.

For complete information on this clause, refer to `CREATE` `MATERIALIZED`
`VIEW` ... "[USING ROLLBACK SEGMENT Clause](CREATE-MATERIALIZED-
VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__CCHHBCEB)".

USING ... CONSTRAINTS Clause

This clause has the same semantics in `CREATE` `MATERIALIZED` `VIEW` and
`ALTER` `MATERIALIZED` `VIEW` statements. For complete information, refer to
"[USING ... CONSTRAINTS Clause](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2152121)" in the documentation on
`CREATE` `MATERIALIZED` `VIEW`.

evaluation_edition_clause

Use this clause to change the evaluation edition for the materialized view.
This clause has the same semantics in `CREATE` `MATERIALIZED` `VIEW` and
`ALTER` `MATERIALIZED` `VIEW` statements. For complete information on this
clause, refer to [evaluation_edition_clause](CREATE-MATERIALIZED-
VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__CCHCFGHG) in the
documentation on `CREATE` `MATERIALIZED` `VIEW`.

Notes on Changing the Evaluation Edition of a Materialized View

The following notes apply when changing the evaluation edition of a
materialized view:

  * If you change the evaluation edition of a refresh-on-commit materialized view, then Oracle Database performs a complete refresh of the materialized view unless you specify `CONSIDER` `FRESH`. 

  * If you change the evaluation edition of a refresh-on-demand materialized view, then Oracle Database sets the staleness state of the materialized view to `STALE` unless you specify `CONSIDER` `FRESH`. 

  * For both refresh-on-commit and refresh-on-demand materialized views: If you change the evaluation edition and specify `CONSIDER` `FRESH`, then Oracle Database does not update the staleness state of the materialized view and does not rebuild the materialized view. Therefore, you can specify `CONSIDER` `FRESH` to indicate that, although the evaluation edition has changed, there is no difference in the results that `subquery` will produce. If the materialized view is stale and in need of either a fast refresh or a complete refresh before this statement is issued, then the state will not be changed and the materialized view may contain bad data. 

{ ENABLE | DISABLE } ON QUERY COMPUTATION

This clause lets you control whether the materialized view is a real-time
materialized view or a regular materialized view.

  * Specify `ENABLE` `ON` `QUERY` `COMPUTATION` to convert a regular materialized view into a real-time materialized view by enabling on-query computation. 

  * Specify `DISABLE` `ON` `QUERY` `COMPUTATION` to convert a real-time materialized view into a regular materialized view by disabling on-query computation. 

This clause has the same semantics in `CREATE` `MATERIALIZED` `VIEW` and `ALTER` `MATERIALIZED` `VIEW` statements. For complete information on this clause, refer to [{ ENABLE | DISABLE } ON QUERY COMPUTATION](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__ENABLEDISABLEONQUERYCOMPUTATION-2C8E4857) in the documentation on `CREATE` `MATERIALIZED` `VIEW`. 

alter_query_rewrite_clause

Use this clause to specify whether the materialized view is eligible to be
used for query rewrite.

ENABLE Clause

Specify `ENABLE` to enable the materialized view for query rewrite. If you
currently specify, or previously specified, the `unusable_editions_clause` for
the materialized view, then it is not enabled for query rewrite in the
unusable editions.

See Also:

  * "[Enabling Query Rewrite: Example](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226881)"

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG-GUID-6AD8879A-0BE5-466E-8D19-1D076C5DDFFB) to learn how to use refresh statistics to monitor the performance of materialized view refresh operations 

Restrictions on Enabling Materialized Views

Enabling materialized views is subject to the following restrictions:

  * If the materialized view is in an invalid or unusable state, then it is not eligible for query rewrite in spite of the `ENABLE` mode. 

  * You cannot enable query rewrite if the materialized view was created totally or in part from a view.

  * You can enable query rewrite only if all user-defined functions in the materialized view are `DETERMINISTIC`. 

See Also:

[CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-
ADD0-4E46-AA56-6D1F7CA63306)

  * You can enable query rewrite only if expressions in the statement are repeatable. For example, you cannot include `CURRENT_TIME` or `USER`. 

See Also:

[Oracle Database Data Warehousing Guide
](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG080)for more information on query rewrite

DISABLE Clause

Specify `DISABLE` if you do not want the materialized view to be eligible for
use by query rewrite. If a materialized view is in the invalid state, then it
is not eligible for use by query rewrite, whether or not it is disabled.
However, a disabled materialized view can be refreshed.

unusable_editions_clause

Use this clause to specify the editions in which the materialized view is not
eligible for query rewrite. This clause has the same semantics in `CREATE`
`MATERIALIZED` `VIEW` and `ALTER` `MATERIALIZED` `VIEW` statements. For
complete information on this clause, refer to
[unusable_editions_clause](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__CCHICCEH) in the documentation on
`CREATE` `MATERIALIZED` `VIEW`.

Cursors that use the materialized view for query rewrite and were compiled in
an edition that is made unusable will be invalidated.

ENABLE | DISABLE CONCURRENT REFRESH

Enable concurrent refresh to refresh the same on-commit atomic materialized
view across mulitple sessions. Multiple sessions which have DML on a base
table can refresh the MV concurrently. There are no limitations on how many
materialized views can be refreshed.

Concurrent refresh is disabled by default. You must explictly enable it on the
materialized view. Note that you can enable it only on on-commit materialized
views.

See Also:

[Refreshing Materialized
Views](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DWHSG-GUID-64068234-BDB0-4C12-AE70-75571046A586) of the
Oracle Database Data Warehousing Guide.

COMPILE

Specify `COMPILE` to explicitly revalidate a materialized view. If an object
upon which the materialized view depends is dropped or altered, then the
materialized view remains accessible, but it is invalid for query rewrite. You
can use this clause to explicitly revalidate the materialized view to make it
eligible for query rewrite.

If the materialized view fails to revalidate, then it cannot be refreshed or
used for query rewrite.

See Also:

"[Compiling a Materialized View: Example](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226906)"

CONSIDER FRESH

This clause lets you manage the staleness state of a materialized view after
changes have been made to its master tables. `CONSIDER` `FRESH` directs Oracle
Database to consider the materialized view fresh and therefore eligible for
query rewrite in the `TRUSTED` or `STALE_TOLERATED` modes.

Caution:

The `CONSIDER` `FRESH` clause also directs Oracle Database to no longer apply
any rows in a materialized view log or Partition Change Tracking changes to
the materialized view prior to the issuance of the `CONSIDER` `FRESH` clause.
In other words, the pending changes will be ignored and deleted, not applied
to the materialized view. This may result in the materialized view containing
more or less data than the base table.

Because Oracle Database cannot guarantee the freshness of the materialized
view, query rewrite in `ENFORCED` mode is not supported. This clause also sets
the staleness state of the materialized view to `UNKNOWN`. The staleness state
is displayed in the `STALENESS` column of the `ALL_MVIEWS`, `DBA_MVIEWS`, and
`USER_MVIEWS` data dictionary views.

A materialized view is stale if changes have been made to the contents of any
of its master tables. This clause directs Oracle Database to assume that the
materialized view is fresh and that no such changes have been made. Therefore,
actual updates to those tables pending refresh are purged with respect to the
materialized view.

See Also:

  * [Oracle Database Data Warehousing Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=DWHSG080) for more information on query rewrite and the implications of performing partition maintenance operations on master tables 

  * "[CONSIDER FRESH: Example](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__I2226850)"

Examples

Automatic Refresh: Examples

The following statement changes the default refresh method for the
`sales_by_month_by_state` materialized view (created in "[Creating
Materialized Aggregate Views: Example](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2092102)") to `FAST`:

    
    
    ALTER MATERIALIZED VIEW sales_by_month_by_state
       REFRESH FAST; 
    

The next automatic refresh of the materialized view will be a fast refresh
provided it is a simple materialized view and its master table has a
materialized view log that was created before the materialized view was
created or last refreshed.

Because the `REFRESH` clause does not specify `START` `WITH` or `NEXT` values,
Oracle Database will use the refresh intervals established by the `REFRESH`
clause when the `sales_by_month_by_state` materialized view was created or
last altered.

The following statement establishes a new interval between automatic refreshes
for the `sales_by_month_by_state` materialized view:

    
    
    ALTER MATERIALIZED VIEW sales_by_month_by_state
       REFRESH NEXT SYSDATE+7;
    

Because the `REFRESH` clause does not specify a `START` `WITH` value, the next
automatic refresh occurs at the time established by the `START` `WITH` and
`NEXT` values specified when the `sales_by_month_by_state` materialized view
was created or last altered.

At the time of the next automatic refresh, Oracle Database refreshes the
materialized view, evaluates the `NEXT` expression `SYSDATE`+7 to determine
the next automatic refresh time, and continues to refresh the materialized
view automatically once a week. Because the `REFRESH` clause does not
explicitly specify a refresh method, Oracle Database continues to use the
refresh method specified by the `REFRESH` clause of the `CREATE`
`MATERIALIZED` `VIEW` or most recent `ALTER` `MATERIALIZED` `VIEW` statement.

CONSIDER FRESH: Example

The following statement instructs Oracle Database that materialized view
`sales_by_month_by_state` should be considered fresh. This statement allows
`sales_by_month_by_state` to be eligible for query rewrite in `TRUSTED` mode
even after you have performed partition maintenance operations on the master
tables of `sales_by_month_by_state`:

    
    
    ALTER MATERIALIZED VIEW sales_by_month_by_state CONSIDER FRESH;
    

As a result of the preceding statement, any partition maintenance operations
that were done to the base table since the last refresh of the materialized
view will not be applied to the materialized view. For example, the add, drop,
or change of data in a partition in the base table will not be reflected in
the materialized view if `CONSIDER` `FRESH` is used before the next refresh of
the materialized view. Refer to [CONSIDER FRESH](ALTER-MATERIALIZED-
VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233__CCHIGAJA) for more
information.

See Also:

"[Splitting Table Partitions: Examples](ALTER-
TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877__I2110367)" for a
partitioning maintenance example that would require this `ALTER`
`MATERIALIZED` `VIEW` example

Complete Refresh: Example

The following statement specifies a new refresh method, a new `NEXT` refresh
time, and a new interval between automatic refreshes of the `emp_data`
materialized view (created in "[Periodic Refresh of Materialized Views:
Example](CREATE-MATERIALIZED-VIEW.md#GUID-
EE262CA4-01E5-4618-B659-6165D993CA1B__I2098290)"):

    
    
    ALTER MATERIALIZED VIEW emp_data
       REFRESH COMPLETE   
       START WITH TRUNC(SYSDATE+1) + 9/24  
       NEXT SYSDATE+7;
    

The `START` `WITH` value establishes the next automatic refresh for the
materialized view to be 9:00 a.m. tomorrow. At that point, Oracle Database
performs a complete refresh of the materialized view, evaluates the `NEXT`
expression, and subsequently refreshes the materialized view every week.

Enabling Query Rewrite: Example

The following statement enables query rewrite on the materialized view
`emp_data` and implicitly revalidates it:

    
    
    ALTER MATERIALIZED VIEW emp_data
       ENABLE QUERY REWRITE;

Primary Key Materialized View: Example

The following statement changes the rowid materialized view `order_data`
(created in "[Creating Rowid Materialized Views: Example](CREATE-MATERIALIZED-
VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B__I2098291)") to a primary
key materialized view. This example requires that you have already defined a
materialized view log with a primary key on `order_data`.

    
    
    ALTER MATERIALIZED VIEW order_data 
       REFRESH WITH PRIMARY KEY; 

Compiling a Materialized View: Example

The following statement revalidates the materialized view `store_mv`:

    
    
    ALTER MATERIALIZED VIEW order_data COMPILE;

Drop Annotation from View: Example

The following example drops annotation `Snapshot` from view `MView1`:

    
    
    ALTER MATERIALIZED VIEW MView1 ANNOTATIONS(DROP Snapshot);


[← Previous](ALTER-LOCKDOWN-PROFILE.md)

[Next →](ALTER-MATERIALIZED-VIEW-LOG.md)
