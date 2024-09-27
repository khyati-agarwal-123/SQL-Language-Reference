[Previous](Backus-Naur-Form-Syntax.md) [Next](Automatic-Locks-in-DML-
Operations.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. Automatic and Manual Locking Mechanisms During SQL Operations

## B Automatic and Manual Locking Mechanisms During SQL Operations

This appendix describes mechanisms that lock data either automatically or as
specified by the user during SQL statements. For a general discussion of
locking mechanisms in the context of data concurrency and consistency, see
[Oracle Database Concepts](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=CNCPT1313).

This appendix contains the following sections:

  * [Automatic Locks in DML Operations](Automatic-Locks-in-DML-Operations.md#GUID-3D57596F-8B73-4C80-8F4D-79A12F781EFD)

  * [Automatic Locks in DDL Operations](Automatic-Locks-in-DDL-Operations.md#GUID-84D392A3-94EC-444D-950F-7829DBCD43EE)

  * [Manual Data Locking](Manual-Data-Locking.md#GUID-B1DE7D59-7FD1-4971-B98D-B69529DF7688)

  * [List of Nonblocking DDLs](Automatic-and-Manual-Locking-Mechanisms-During-SQL-Operations.md#GUID-1B08DE66-5ED8-4BEF-893B-B887E3A82D50)

### List of Nonblocking DDLs

Release 23

The following nonblocking DDLs are added in Release 23.3:

  * alter table add column

  * alter table set column unused

  * alter table add constraint enable novalidate

  * alter table drop constraint

Release 21

The following nonblocking DDLs are added in Release 21c:

  * alter table modify default attributes tablespace

  * alter table modify default attributes lob tablespace

  * alter index modify default attributes tablespace

  * alter table modify default attributes for partition tablespace

  * alter table modify default attributes for partition lob tablespace

  * alter index modify default attributes for partition tablespace

Release 12.2.0.2

List of Nonblocking DDLs Added in 12.2.0.2

  * Alter table merge partition online

  * alter table modify partition by .. online (to change the partitioning schema of a table)

Release 12.2.0.1

List of Nonblocking DDLs Added in 12.2.0.1

  * alter table split partition [subpartition] online

  * alter table move online (move of a non-partitioned table)

  * alter table modify partition by .. online (to convert a non-partitioned table to partitioned state)

Release 12.1

The following nonblocking DDLs are added as of Release 12.1. Some nonblocking
DDLs are downgraded to blocking in the presence of supplemental logging.

List of Nonblocking DDLs Added in 12.1

  * drop index online

  * alter index unusable online

  * alter table move partition online

  * alter table move subpartition online

List of Nonblocking DDLs Added in 12.1 that Downgrade to Blocking During
Supplemental Logging

  * alter table set unused column online

  * alter table drop constraint online

  * alter table modify column visible / invisible

  * alter table add nullable column with default value

Release 11.2

The following nonblocking DDLs are added as of Release 11.2. Some nonblocking
DDLs are downgraded to blocking in the presence of supplemental logging.

List of Nonblocking DDLs Added in 11.2

  * create index online

  * alter index rebuild online

  * alter index rebuild partition online

  * alter index rebuild subpartition online

  * alter index visible / novisible

List of Nonblocking DDLs Added in 11.2 that Downgrade to Blocking During
Supplemental Logging

  * alter table add column not null with default value

  * alter table add constraint enable novalidate

  * alter table modify constraint validate 

  * alter table add column (without any default)


[← Previous](Manual-Data-Locking.md)

[Next →](Oracle-and-Standard-SQL.md)
