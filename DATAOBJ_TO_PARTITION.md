##  DATAOBJ_TO_PARTITION {#GUID-B6F62AFF-0AE1-469B-98B1-589A2D07F3A3} 

Syntax 

![Description of dataobj_to_partition.eps follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/dataobj_to_partition.gif)[ Description of the illustration dataobj_to_partition.eps ](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img_text/dataobj_to_partition.md)

Purpose 

` DATAOBJ_TO_PARTITION ` is useful only to Data Cartridge developers who are performing data maintenance or query operations on system-partitioned tables that are used to store domain index data. The DML or query operations are triggered by corresponding operations on the base table of the domain index. 

This function takes as arguments the name of the base table and the partition ID of the base table partition, both of which are passed to the function by the appropriate ODCIIndex method. The function returns the absolute partition number of the corresponding system-partitioned table, which can be used to perform the operation (DML or query) on that partition of the system-partitioned table. 

> **note:** 

If the base table is interval partitioned, then Oracle recommends that you instead use the ` DATAOBJ_TO_MAT_PARTITION ` function. Refer to [ DATAOBJ_TO_MAT_PARTITION ](DATAOBJ_TO_MAT_PARTITION.md#GUID-195AC748-0C9E-4A68-B2BC-2411DE435375) for more information. 

> **note:** See Also: 

[ *Oracle Database Data Cartridge Developer's Guide*  ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADDCI290) for information on the use of the ` DATAOBJ_TO_PARTITION ` function, including examples 
