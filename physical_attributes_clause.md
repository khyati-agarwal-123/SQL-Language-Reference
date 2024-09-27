[Previous](parallel_clause.md) [Next](size_clause.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Common SQL DDL Clauses ](Common-SQL-DDL-Clauses.md)
  3. physical_attributes_clause 

## physical_attributes_clause

Purpose

The `physical_attributes_clause` lets you specify the value of the `PCTFREE`,
`PCTUSED`, and `INITRANS` parameters and the storage characteristics of a
table, cluster, index, or materialized view.

You can specify the `physical_attributes_clause` in the following statements:

  * `CREATE` `CLUSTER` and `ALTER` `CLUSTER`: to set or change the physical attributes of the cluster and all tables in the cluster (see [CREATE CLUSTER](CREATE-CLUSTER.md#GUID-4DBC701F-AFC3-486D-AA32-B5CB1D6946F7) and [ALTER CLUSTER](ALTER-CLUSTER.md#GUID-A4E03C13-7690-4567-9B0A-DA6A21173B4D)). 

  * `CREATE` `TABLE`: to set the physical attributes of the table, a table partition, the `OIDINDEX` of an object table, or the overflow segment of an index-organized table (see [CREATE TABLE](CREATE-TABLE.md#GUID-F9CE0CC3-13AE-4744-A43C-EAC7A71AAAB6)). 

  * `ALTER` `TABLE`: to change the physical attributes of the table, the default physical attributes of future table partitions, or the physical attributes of existing table partitions (see [ALTER TABLE](ALTER-TABLE.md#GUID-552E7373-BF93-477D-9DA3-B2C9386F2877)). The following restrictions apply: 

    * You cannot specify physical attributes for a temporary table.

    * You cannot specify physical attributes for a clustered table. Tables in a cluster inherit the physical attributes of the cluster.

  * `CREATE` `INDEX`: to set the physical attributes of an index or index partition (see [CREATE INDEX](CREATE-INDEX.md#GUID-1F89BBC0-825F-4215-AF71-7588E31D8BFE)). 

  * `ALTER` `INDEX`: to change the physical attributes of the index, the default physical attributes of future index partitions, or the physical attributes of existing index partitions (see [ALTER INDEX](ALTER-INDEX.md#GUID-D8F648E7-8C07-4C89-BB71-862512536558)). 

  * `CREATE` `MATERIALIZED` `VIEW`: to set the physical attributes of the materialized view, one of its partitions, or the index Oracle Database generates to maintain the materialized view (see [CREATE MATERIALIZED VIEW](CREATE-MATERIALIZED-VIEW.md#GUID-EE262CA4-01E5-4618-B659-6165D993CA1B)). 

  * `ALTER` `MATERIALIZED` `VIEW`: to change the physical attributes of the materialized view, the default physical attributes of future partitions, the physical attributes of an existing partition, or the index Oracle creates to maintain the materialized view (see [ALTER MATERIALIZED VIEW](ALTER-MATERIALIZED-VIEW.md#GUID-29EE5682-AE42-4879-ABAD-E34E66ADD233)). 

  * `CREATE` `MATERIALIZED` `VIEW` `LOG` and `ALTER` `MATERIALIZED` `VIEW` `LOG`: to set or change the physical attributes of the materialized view log (see [CREATE MATERIALIZED VIEW LOG](CREATE-MATERIALIZED-VIEW-LOG.md#GUID-13902019-D044-4B79-9EB4-1F60652D037B) and [ALTER MATERIALIZED VIEW LOG](ALTER-MATERIALIZED-VIEW-LOG.md#GUID-4DAD5E6F-E30A-43D0-B023-634752E0E627)). 

Syntax

physical_attributes_clause::=

![Description of physical_attributes_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/physical_attributes_clause.gif)  
[Description of the illustration
physical_attributes_clause.eps](img_text/physical_attributes_clause.md)

([storage_clause::=](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__CJACEJGB))

Semantics

This section describes the parameters of the `physical_attributes_clause`. For
additional information, refer to the SQL statement in which you set or reset
these parameters for a particular database object.

PCTFREE integer

Specify a whole number representing the percentage of space in each data block
of the database object reserved for future updates to rows of the object. The
value of `PCTFREE` must be a value from 0 to 99. A value of 0 means that the
entire block can be filled by inserts of new rows. The default value is 10.
This value reserves 10% of each block for updates to existing rows and allows
inserts of new rows to fill a maximum of 90% of each block.

`PCTFREE` has the same function in the statements that create and alter
tables, partitions, clusters, indexes, materialized views, materialized view
logs, and zone maps. The combination of `PCTFREE` and `PCTUSED` determines
whether new rows will be inserted into existing data blocks or into new
blocks. See "[How PCTFREE and PCTUSED Work
Together](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393__BABCJFCF)".

Restriction on the PCTFREE Clause

When altering an index, you can specify this parameter only in the
`modify_index_default_attrs` clause and the `split_index_partition` clause.

PCTUSED integer

Specify a whole number representing the minimum percentage of used space that
Oracle maintains for each data block of the database object. `PCTUSED` is
specified as a positive integer from 0 to 99 and defaults to 40.

`PCTUSED` has the same function in the statements that create and alter
tables, partitions, clusters, materialized views, materialized view logs, and
zone maps.

`PCTUSED` is not a valid table storage characteristic for an index-organized
table.

The sum of `PCTFREE` and `PCTUSED` must be equal to or less than 100. You can
use `PCTFREE` and `PCTUSED` together to utilize space within a database object
more efficiently. See "[How PCTFREE and PCTUSED Work
Together](physical_attributes_clause.md#GUID-A15063A9-3237-43D3-B0AE-D01F6E80B393__BABCJFCF)".

Restrictions on the PCTUSED Clause

The `PCTUSED` parameter is subject to the following restrictions:

  * You cannot specify this parameter for an index or for the index segment of an index-organized table. 

  * This parameter is not useful and is ignored for objects with automatic segment-space management. 

See Also:

[Oracle Database Performance Tuning
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=TGDBA94472) for information on the performance effects of
different values of `PCTUSED` and `PCTFREE` and `CREATE` `TABLESPACE`
[segment_management_clause](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2096553) for
information on automatic segment-space management

How PCTFREE and PCTUSED Work Together

In a newly allocated data block, the space available for inserts is the block
size minus the sum of the block overhead and free space (`PCTFREE`). Updates
to existing data can use any available space in the block. Therefore, updates
can reduce the available space of a block to less than `PCTFREE`.

After a data block is filled to the limit determined by `PCTFREE`, Oracle
Database considers the block unavailable for the insertion of new rows until
the percentage of that block falls beneath the parameter `PCTUSED`. Until this
value is achieved, Oracle Database uses the free space of the data block only
for updates to rows already contained in the data block. A block becomes a
candidate for row insertion when its used space falls below `PCTUSED`.

See Also:

[FREELISTS](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15__BABECDAG)
for information on how `PCTUSED` and `PCTFREE` work with freelist segment
space management

INITRANS integer

Specify the initial number of concurrent transaction entries allocated within
each data block allocated to the database object. This value can range from 1
to 255 and defaults to 1, with the following exceptions:

  * The default `INITRANS` value for a cluster is 2 or the default `INITRANS` value of the tablespace in which the cluster resides, whichever is greater. 

  * The default value for an index is 2.

In general, you should not change the `INITRANS` value from its default.

Each transaction that updates a block requires a transaction entry in the
block. This parameter ensures that a minimum number of concurrent transactions
can update the block and helps avoid the overhead of dynamically allocating a
transaction entry.

The `INITRANS` parameter serves the same purpose in the statements that create
and alter tables, partitions, clusters, indexes, materialized views, and
materialized view logs.

MAXTRANS Parameter

In earlier releases, the `MAXTRANS` parameter determined the maximum number of
concurrent update transactions allowed for each data block in the segment.
This parameter has been deprecated. Oracle now automatically allows up to 255
concurrent update transactions for any data block, depending on the available
space in the block. Note that the maximum number of concurrent update
transactions is based on the size of the block

Existing objects for which a value of `MAXTRANS` has already been set retain
that setting. However, if you attempt to change the value for `MAXTRANS`,
Oracle ignores the new specification and substitutes the value 255 without
returning an error.

storage_clause

The `storage_clause` lets you specify storage characteristics for the table,
object table `OIDINDEX`, partition, LOB data segment, or index-organized table
overflow data segment. This clause has performance ramifications for large
tables. Storage should be allocated to minimize dynamic allocation of
additional space. Refer to the
[storage_clause](storage_clause.md#GUID-C5A67610-3160-41E9-8D48-03206BD5ED15)
for more information.


[← Previous](parallel_clause.md)

[Next →](size_clause.md)
