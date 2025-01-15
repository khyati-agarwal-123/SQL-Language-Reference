##  OBJECT_ID Pseudocolumn {#GUID-EA125CCC-B4EE-4065-996E-12A1ADCC5F7F} 

The ` OBJECT_ID ` pseudocolumn returns the object identifier of a column of an object table or view. Oracle uses this pseudocolumn as the primary key of an object table. ` OBJECT_ID ` is useful in ` INSTEAD ` ` OF ` triggers on views and for identifying the ID of a substitutable row in an object table. 

> **note:** 

In earlier releases, this pseudocolumn was called ` SYS_NC_OID$ ` . That name is still supported for backward compatibility. However, Oracle recommends that you use the more intuitive name ` OBJECT_ID ` . 

> **note:** See Also: 

[ *Oracle Database Object-Relational Developer's Guide*  ](https://docs.oracle.com/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADOBJ7129) for examples of the use of this pseudocolumn 
