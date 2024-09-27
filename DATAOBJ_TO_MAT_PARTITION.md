[Previous](CV.md) [Next](DATAOBJ_TO_PARTITION.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. DATAOBJ_TO_MAT_PARTITION 

## DATAOBJ_TO_MAT_PARTITION

Syntax

![Description of dataobj_to_mat_partition.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dataobj_to_mat_partition.gif)  
[Description of the illustration
dataobj_to_mat_partition.eps](img_text/dataobj_to_mat_partition.md)

Purpose

`DATAOBJ_TO_MAT_PARTITION` is useful only to Data Cartridge developers who are
performing data maintenance or query operations on system-partitioned tables
that are used to store domain index data. The DML or query operations are
triggered by corresponding operations on the base table of the domain index.

This function takes as arguments the name of the base table and the partition
ID of the base table partition, both of which are passed to the function by
the appropriate ODCIIndex method. The function returns the materialized
partition number of the corresponding system-partitioned table, which can be
used to perform the operation (DML or query) on that partition of the system-
partitioned table.

If the base table is interval partitioned, then Oracle recommends that you use
this function instead of the `DATAOBJ_TO_PARTITION` function. The
`DATAOBJ_TO_PARTITION` function determines the absolute partition number,
given the physical partition identifier. However, if the base table is
interval partitioned, then there might be holes in the partition numbers
corresponding to unmaterialized partitions. Because the system partitioned
table only has materialized partitions, `DATAOBJ_TO_PARTITION` numbers can
cause a mis-match between the partitions of the base table and the partitions
of the underlying system partitioned index storage tables. The
`DATAOBJ_TO_MAT_PARTITION` function returns the materialized partition number
(as opposed to the absolute partition number) and helps keep the two tables in
sync. Indextypes planning to support local domain indexes on interval
partitioned tables should migrate to the use of this function.

See Also:

  * [DATAOBJ_TO_PARTITION](DATAOBJ_TO_PARTITION.md#GUID-B6F62AFF-0AE1-469B-98B1-589A2D07F3A3)

  * [Oracle Database Data Cartridge Developer's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADDCI290) for information on the use of the `DATAOBJ_TO_MAT_PARTITION` function, including examples 


[← Previous](CV.md)

[Next →](DATAOBJ_TO_PARTITION.md)
