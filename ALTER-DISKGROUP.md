[Previous](ALTER-DIMENSION.md) [Next](alter-domain.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: ADMINISTER KEY MANAGEMENT to ALTER JAVA](SQL-Statements-ADMINISTER-KEY-MANAGEMENT-to-ALTER-JAVA.md)
  3. ALTER DISKGROUP 

## ALTER DISKGROUP

Note:

This SQL statement is valid only if you are using Oracle ASM and you have
started an Oracle ASM instance. You must issue this statement from within the
Oracle ASM instance, not from a normal database instance. For information on
starting an Oracle ASM instance, refer to [Oracle Automatic Storage Management
Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG036).

Purpose

The `ALTER` `DISKGROUP` statement lets you perform a number of operations on a
disk group or on the disks in a disk group.

See Also:

  * [CREATE DISKGROUP](CREATE-DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880) for information on creating disk groups 

  * [Oracle Automatic Storage Management Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=OSTMG036) for information on Oracle ASM and using disk groups to simplify database administration 

Prerequisites

You must have an Oracle ASM instance started from which you issue this
statement. The disk group to be modified must be mounted.

You can issue all `ALTER` `DISKGROUP` clauses if you have the `SYSASM` system
privilege. You can issue specific clauses as follows:

  * The `SYSOPER` privilege permits the following subset of the `ALTER` `DISKGROUP` operations: `diskgroup_availability`, `rebalance_diskgroup_clause`, `check_diskgroup_clause` (without the `REPAIR` option). 

  * If you are connected as `SYSDBA`, you have limited privileges to use this statement. The following operations are always granted to users connected as `SYSDBA`: 

    * `ALTER` `DISKGROUP` ... `ADD` `DIRECTORY`

    * `ALTER` `DISKGROUP` ... `ADD`/`ALTER`/`DROP` `TEMPLATE` (nonsystem templates only) 

    * `ALTER` `DISKGROUP` ... `ADD` `USERGROUP`

    * `SELECT`

    * `SHOW` `PARAMETER`

[Table 10-1](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBFECBF "Column 1
lists the ALTER DISK operations with specific prerequisites. Column 2 contains
the prerequisites.") shows additional privileges granted to users connected as
`SYSDBA` under the conditions shown:

Table 10-1 Conditional Diskgroup Privileges for SYSDBA

ALTER DISKGROUP Operation | Condition  
---|---  
`DROP` `FILE` |  User must have read-write permission on the file.  
`ADD` `ALIAS` |  User must have read-write permission on the related file.  
`RENAME` `ALIAS` |  User must have read-write permission on the related file.  
`DROP` `ALIAS` |  User must have read-write permission on the related file.  
`RENAME` `DIRECTORY` |  Directory must contain only aliases and no files. User must have `DROP` `ALIAS` permissions on all aliases under the directory.   
`DROP` `DIRECTORY` |  Directory must contain only aliases and no files. User must have `DROP` `ALIAS` permissions on all aliases under the directory.   
`DROP` `USERGROUP` |  User must be the owner of the user group.  
`MODIFY` `USERGROUP` `ADD` `MEMBER` |  User must be the owner of the user group.  
`MODIFY` `USERGROUP` `DROP` `MEMBER` |  User must be the owner of the user group.  
`SET` `PERMISSION` |  User must be the owner of the file.  
`SET` `OWNER` `GROUP` |  User must be the owner of the file and a member of the user group.  
  
Syntax

alter_diskgroup::=

![Description of alter_diskgroup.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/alter_diskgroup.gif)  
[Description of the illustration
alter_diskgroup.eps](img_text/alter_diskgroup.md)

([add_disk_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168772),
[drop_disk_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168665),
[resize_disk_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168828),
[replace_disk_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEGBBHC),
[rename_disk_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEJJABJ),
[disk_online_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABEFCHE),
[disk_offline_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABEJJID),
[rebalance_diskgroup_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168857),
[check_diskgroup_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEBGCFB),
[diskgroup_template_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEEDEDC),
[diskgroup_directory_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGECIJCC),
[diskgroup_alias_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEEJAFI),
[diskgroup_volume_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBBDJBA),
[diskgroup_attributes::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABGCDFE),
[modify_diskgroup_file::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEGFJD),
[drop_diskgroup_file_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEBADJI),
[convert_redundancy_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__CONVERT_REDUNDANCY_CLAUSE-57BF8F00),
[usergroup_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBJACJH),
[user_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBBGAHG),
[file_permissions_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEAHIA),
[file_owner_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBFGDIJ),
[scrub_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEEHAAE),
[quotagroup_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__QUOTAGROUP_CLAUSES-4FAA7646),
[filegroup_clauses::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__FILEGROUP_CLAUSES-4FAAB7F0),
[undrop_disk_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168846),
[diskgroup_availability::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEGEFBJ),
[enable_disable_volume::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBHCFBD))

add_disk_clause::=

![Description of add_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_disk_clause.gif)  
[Description of the illustration
add_disk_clause.eps](img_text/add_disk_clause.md)

([qualified_disk_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2208507))

qualified_disk_clause::=

![Description of qualified_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/qualified_disk_clause.gif)  
[Description of the illustration
qualified_disk_clause.eps](img_text/qualified_disk_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

drop_disk_clause::=

![Description of drop_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_disk_clause.gif)  
[Description of the illustration
drop_disk_clause.eps](img_text/drop_disk_clause.md)

resize_disk_clause::=

![Description of resize_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/resize_disk_clause.gif)  
[Description of the illustration
resize_disk_clause.eps](img_text/resize_disk_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

replace_disk_clause::=

![Description of replace_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/replace_disk_clause.gif)  
[Description of the illustration
replace_disk_clause.eps](img_text/replace_disk_clause.md)

rename_disk_clause::=

![Description of rename_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rename_disk_clause.gif)  
[Description of the illustration
rename_disk_clause.eps](img_text/rename_disk_clause.md)

disk_online_clause::=

![Description of disk_online_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/disk_online_clause.gif)  
[Description of the illustration
disk_online_clause.eps](img_text/disk_online_clause.md)

disk_offline_clause::=

![Description of disk_offline_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/disk_offline_clause.gif)  
[Description of the illustration
disk_offline_clause.eps](img_text/disk_offline_clause.md)

timeout_clause::=

![Description of timeout_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/timeout_clause.gif)  
[Description of the illustration
timeout_clause.eps](img_text/timeout_clause.md)

rebalance_diskgroup_clause::=

![Description of rebalance_diskgroup_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/rebalance_diskgroup_clause.gif)  
[Description of the illustration
rebalance_diskgroup_clause.eps](img_text/rebalance_diskgroup_clause.md)

check_diskgroup_clause::=

![Description of check_diskgroup_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/check_diskgroup_clause.gif)  
[Description of the illustration
check_diskgroup_clause.eps](img_text/check_diskgroup_clause.md)

diskgroup_template_clauses::=

![Description of diskgroup_template_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/diskgroup_template_clauses.gif)  
[Description of the illustration
diskgroup_template_clauses.eps](img_text/diskgroup_template_clauses.md)

([qualified_template_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2208551))

qualified_template_clause::=

![Description of qualified_template_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/qualified_template_clause.gif)  
[Description of the illustration
qualified_template_clause.eps](img_text/qualified_template_clause.md)

redundancy_clause::=

![Description of redundancy_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/redundancy_clause.gif)  
[Description of the illustration
redundancy_clause.eps](img_text/redundancy_clause.md)

striping_clause::=

![Description of striping_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/striping_clause.gif)  
[Description of the illustration
striping_clause.eps](img_text/striping_clause.md)

diskgroup_directory_clauses::=

![Description of diskgroup_directory_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/diskgroup_directory_clauses.gif)  
[Description of the illustration
diskgroup_directory_clauses.eps](img_text/diskgroup_directory_clauses.md)

diskgroup_alias_clauses::=

![Description of diskgroup_alias_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/diskgroup_alias_clauses.gif)  
[Description of the illustration
diskgroup_alias_clauses.eps](img_text/diskgroup_alias_clauses.md)

diskgroup_volume_clauses::=

![Description of diskgroup_volume_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/diskgroup_volume_clauses.gif)  
[Description of the illustration
diskgroup_volume_clauses.eps](img_text/diskgroup_volume_clauses.md)

([add_volume_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABGCCEJ),
[modify_volume_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABCIDJB)

add_volume_clause::=

![Description of add_volume_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_volume_clause.gif)  
[Description of the illustration
add_volume_clause.eps](img_text/add_volume_clause.md)

([size_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABEDJHI),
[redundancy_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABDDHBB), )

size_clause::=

![Description of size_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/size_clause.gif)  
[Description of the illustration size_clause.eps](img_text/size_clause.md)

modify_volume_clause::=

![Description of modify_volume_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/modify_volume_clause.gif)  
[Description of the illustration
modify_volume_clause.eps](img_text/modify_volume_clause.md)

diskgroup_attributes::=

![Description of diskgroup_attributes.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/diskgroup_attributes.gif)  
[Description of the illustration
diskgroup_attributes.eps](img_text/diskgroup_attributes.md)

modify_diskgroup_file::=

![Description of modify_diskgroup_file.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/modify_diskgroup_file.gif)  
[Description of the illustration
modify_diskgroup_file.eps](img_text/modify_diskgroup_file.md)

drop_diskgroup_file_clause::=

![Description of drop_diskgroup_file_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_diskgroup_file_clause.gif)  
[Description of the illustration
drop_diskgroup_file_clause.eps](img_text/drop_diskgroup_file_clause.md)

convert_redundancy_clause::=

![Description of convert_redundancy_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/convert_redundancy_clause.gif)  
[Description of the illustration
convert_redundancy_clause.eps](img_text/convert_redundancy_clause.md)

usergroup_clauses::=

![Description of usergroup_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/usergroup_clauses.gif)  
[Description of the illustration
usergroup_clauses.eps](img_text/usergroup_clauses.md)

user_clauses::=

![Description of user_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/user_clauses.gif)  
[Description of the illustration user_clauses.eps](img_text/user_clauses.md)

file_permissions_clause::=

![Description of file_permissions_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/file_permissions_clause.gif)  
[Description of the illustration
file_permissions_clause.eps](img_text/file_permissions_clause.md)

file_owner_clause::=

![Description of file_owner_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/file_owner_clause.gif)  
[Description of the illustration
file_owner_clause.eps](img_text/file_owner_clause.md)

scrub_clause::=

![Description of scrub_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/scrub_clause.gif)  
[Description of the illustration scrub_clause.eps](img_text/scrub_clause.md)

quotagroup_clauses::=

![Description of quotagroup_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/quotagroup_clauses.gif)  
[Description of the illustration
quotagroup_clauses.eps](img_text/quotagroup_clauses.md)

filegroup_clauses::=

![Description of filegroup_clauses.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/filegroup_clauses.gif)  
[Description of the illustration
filegroup_clauses.eps](img_text/filegroup_clauses.md)

([add_filegroup_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__ADD_FILEGROUP_CLAUSE-5AD3A8CA),
[modify_filegroup_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__MODIFY_FILEGROUP_CLAUSE-5AD3AC4F),
[move_to_filegroup_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__MOVE_TO_FILEGROUP_CLAUSE-5AD3B18B),
[drop_filegroup_clause::=](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__DROP_FILEGROUP_CLAUSE-5AD3B51F))

add_filegroup_clause::=

![Description of add_filegroup_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/add_filegroup_clause.gif)  
[Description of the illustration
add_filegroup_clause.eps](img_text/add_filegroup_clause.md)

modify_filegroup_clause::=

![Description of modify_filegroup_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/modify_filegroup_clause.gif)  
[Description of the illustration
modify_filegroup_clause.eps](img_text/modify_filegroup_clause.md)

move_to_filegroup_clause::=

![Description of move_to_filegroup_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/move_to_filegroup_clause.gif)  
[Description of the illustration
move_to_filegroup_clause.eps](img_text/move_to_filegroup_clause.md)

drop_filegroup_clause::=

![Description of drop_filegroup_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_filegroup_clause.gif)  
[Description of the illustration
drop_filegroup_clause.eps](img_text/drop_filegroup_clause.md)

undrop_disk_clause::=

![Description of undrop_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/undrop_disk_clause.gif)  
[Description of the illustration
undrop_disk_clause.eps](img_text/undrop_disk_clause.md)

diskgroup_availability::=

![Description of diskgroup_availability.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/diskgroup_availability.gif)  
[Description of the illustration
diskgroup_availability.eps](img_text/diskgroup_availability.md)

enable_disable_volume::=

![Description of enable_disable_volume.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/enable_disable_volume.gif)  
[Description of the illustration
enable_disable_volume.eps](img_text/enable_disable_volume.md)

Semantics

diskgroup_name

Specify the name of the disk group you want to modify. To determine the names
of existing disk groups, query the
[`V$ASM_DISKGROUP`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30171) dynamic performance view.

add_disk_clause

Use this clause to add one or more disks to the disk group and specify
attributes for the newly added disk. Oracle ASM automatically rebalances the
disk group as part of this operation.

You cannot use this clause to change the failure group of a disk. Instead you
must drop the disk from the disk group and then add the disk back into the
disk group as part of the new failure group.

To determine the names of the disks already in this disk group, query the
[`V$ASM_DISK`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30170) dynamic performance view.

QUORUM | REGULAR

The semantics of these keyword are the same as the semantics in a `CREATE` `DISKGROUP` statement. See [QUORUM | REGULAR](CREATE-DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__CACJHFHD) for more information on these keywords. 

You cannot change this qualifier for an existing disk or disk group.
Therefore, you cannot specify in this clause a keyword different from the
keyword that was specified when the disk group was created.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG13790) for more information about the use of these
keywords

FAILGROUP Clause

Use this clause to assign the newly added disk to a failure group. If you omit
this clause and you are adding the disk to a normal or high redundancy disk
group, then Oracle Database automatically adds the newly added disk to its own
failure group. The implicit name of the failure group is the same as the
operating system independent disk name (see "[NAME Clause](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__I2177129)").

You cannot specify this clause if you are creating an external redundancy disk
group.

qualified_disk_clause

This clause has the same semantics in `CREATE` `DISKGROUP` and `ALTER`
`DISKGROUP` statements. For complete information on this clause, refer to
[qualified_disk_clause](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__I2177293) in the
documentation on `CREATE` `DISKGROUP`.

drop_disk_clause

Use this clause to drop one or more disks from the disk group.

DROP DISK

The `DROP` `DISK` clause lets you drop one or more disks from the disk group
and automatically rebalance the disk group. When you drop a disk, Oracle ASM
relocates all the data from the disk and clears the disk header so that it no
longer is part of the disk group. The disk header is not cleared if you
specify the `FORCE` keyword.

Specify `disk_name` as shown in the `NAME` column of the `V$ASM_DISK` dynamic
performance view.

If a disk to be dropped is a quorum disk or belongs to a quorum failure group, then you must specify `QUORUM` in order to drop the disk. See [QUORUM | REGULAR](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEHDFI). 

DROP DISKS IN FAILGROUP

The `DROP` `DISKS` `IN` `FAILGROUP` clause lets you drop all the disks in the
specified failure group. The behavior is otherwise the same as that for the
`DROP` `DISK` clause.

If the specified failure group is a quorum failure group, then you must specify the `QUORUM` keyword in order to drop the disks. See [QUORUM | REGULAR](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEHDFI). 

FORCE | NOFORCE

These keywords let you specify when the disk is considered to be no longer
part of the disk group. The default and recommended setting is `NOFORCE`.

  * When you specify `NOFORCE`, Oracle ASM reallocates all of the extents of the disk to other disks and then expels the disk from the disk group and rebalances the disk group. 

Note:

`DROP` `DISK` ... `NOFORCE` returns control to the user before the disk can be
safely reused or removed from the system. To ensure that the drop disk
operation has completed, query the `V$ASM_DISK` view to verify that
`HEADER_STATUS` has the value `FORMER`. Do not attempt to remove or reuse a
disk if `STATE` has the value `DROPPING`. Query the `V$ASM_OPERATION` view for
approximate information on how long it will take to complete the rebalance
resulting from dropping the disk.If you also specify `REBALANCE` ... `WAIT`
(see [rebalance_diskgroup_clause](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168800)), then the
statement will not return until the rebalance operation is complete and the
disk has been cleared. However, you should always verify that the
`HEADER_STATUS` column of `V$ASM_DISK` is `FORMER`, because of the unlikely
event the rebalance operations fails.

  * When you specify `FORCE`, Oracle Database expels the disk from the disk group immediately. It then reconstructs the data from the redundant copies on other disks, reallocates the data to other disks, and rebalances the disk group. 

The `FORCE` clause can be useful, for example, if Oracle ASM can no longer
read the disk to be dropped. However, it is more time consuming than a
`NOFORCE` drop, and it can leave portions of a file with reduced protection.
You cannot specify `FORCE` for an external redundancy disk group at all,
because in the absence of redundant data on the disk, Oracle ASM must read the
data from the disk before it can be dropped.

The rebalance operation invoked when a disk is dropped is time consuming,
whether or not you specify `FORCE` or `NOFORCE`. You can monitor the progress
by querying the
[`V$ASM_OPERATION`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30173) dynamic performance view. Refer to
[rebalance_diskgroup_clause](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168800) for more
information on rebalance operations.

resize_disk_clause

Use this clause to specify a new size for every disk in a disk group. This
clause lets you override the size returned by the operating system or the size
you specified previously for the disks.

SIZE

Specify the new size in kilobytes, megabytes, gigabytes, or terabytes. You
cannot specify a size greater than the capacity of the disk. If you specify a
size smaller than the disk capacity, then you limit the amount of disk space
Oracle ASM will use. If you omit this clause, then Oracle ASM attempts
programatically to determine the size of the disks.

replace_disk_clause

Use this clause to replace one or more disks in the disk group. This clause
allows you to replace disks with a single operation, which is more efficient
than dropping and adding each disk.

For `disk_name`, specify the name of the disk you want to replace. This name
is assigned to the replacement disk. You can view disk names by querying the
`NAME` column of the `V$ASM_DISK` dynamic performance view.

For `path_name`, specify the full path name for the replacement disk.

FORCE

Specify `FORCE` if you want Oracle ASM to add the replacement disk to the disk
group even if the replacement disk is already a member of a disk group.

Note:

Using `FORCE` in this way may destroy existing disk groups.

NOFORCE

Specify `NOFORCE` if you want Oracle ASM to return an error if the replacement
disk is already a member of a disk group. `NOFORCE` is the default.

POWER

The `POWER` clause has the same semantics here as for a manual rebalancing of
a disk group, except that the power value cannot be set to 0. See
[POWER](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABCGEIH).

WAIT | NOWAIT

The `WAIT` and `NOWAIT` keywords have the same semantics here as for a manual rebalancing of a disk group. See [WAIT | NOWAIT](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABHEIIB). 

rename_disk_clause

Use this clause to rename one or more disks in the disk group. The disk group
must be in the `MOUNT` `RESTRICTED` state and all disks in the disk group must
be online.

RENAME DISK

Specify this clause to rename one or more disks. For each disk, specify the
`old_disk_name` and `new_disk_name`. If `new_disk_name` already exists, then
this operation fails.

RENAME DISKS ALL

Specify this clause to rename all disks in the disk group to a name of the
form `diskgroupname_####`, where `####` is the disk number. Disk names that
are already in the `diskgroupname_####` format are not changed.

disk_online_clause

Use this clause to bring one or more disks online and rebalance the disk
group.

ONLINE DISK

The `ONLINE` `DISK` clause lets you bring one or more specified disks online
and rebalance the disk group.

Specify `disk_name` as shown in the `NAME` column of the `V$ASM_DISK` dynamic
performance view.

The `QUORUM` and `REGULAR` keywords have the same semantics here as they have when adding a disk to a disk group. See [QUORUM | REGULAR](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEHDFI). 

ONLINE DISKS IN FAILGROUP

The `ONLINE` `DISKS` `IN` `FAILGROUP` clause lets you bring all disks in the
specified failure group online and rebalance the disk group.

If the specified failure group is a quorum failure group, then you must specify the `QUORUM` keyword in order to bring the disks online. See [QUORUM | REGULAR](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEHDFI). 

ALL

The `ALL` clause lets you bring all disks in the disk group online and
rebalance the disk group.

POWER

The `POWER` clause has the same semantics here as for a manual rebalancing of
a disk group. See [POWER](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABCGEIH)

WAIT | NOWAIT

The `WAIT` and `NOWAIT` keywords have the same semantics here as for a manual rebalancing of a disk group. See [WAIT | NOWAIT](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABHEIIB). 

disk_offline_clause

Use the `disk_offline_clause` to take one or more disks offline. This clause
fails if the redundancy level of the disk group would be violated by taking
the specified disks offline.

OFFLINE DISK

The `OFFLINE` `DISK` clause lets you take one or more specified disks offline.

Specify `disk_name` as shown in the `NAME` column of the `V$ASM_DISK` dynamic
performance view.

The `QUORUM` and `REGULAR` keywords have the same semantics here as they have when adding a disk to a disk group. See [QUORUM | REGULAR](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEHDFI). 

OFFLINE DISKS IN FAILGROUP

The `OFFLINE` `DISKS` `IN` `FAILGROUP` clause lets you take all disks in the
specified failure group offline.

If the specified failure group is a quorum failure group, then you must specify the `QUORUM` keyword in order to take the disks offline. See [QUORUM | REGULAR](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBEHDFI). 

timeout_clause

By default, Oracle ASM drops a disk shortly after it is taken offline. You can
delay this operation by specifying the `timeout_clause`, which gives you the
opportunity to repair the disk and bring it back online. You can specify the
timeout value in units of minute or hour. If you omit the unit, then the
default is hour.

You can change the timeout period by specifying this clause multiple times.
Each time you specify it, Oracle ASM measures the time from the most recent
previous `disk_offline_clause` while the disk group is mounted. To learn how
much time remains before Oracle ASM will drop an offline disk, query the
`REPAIR_TIMER` column of `V$ASM_DISK`.

This clause overrides any previous setting of the `disk_repair_time`
attribute. Refer to [Table 13-2](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__BGEDFCIB "Column 1
lists diskgroup attribute names; column 2 lists valid values for each
attribute; column 3 describes the attributes.") for more information about
disk group attributes.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG10044) for more information about taking Oracle ASM
disks online and offline

WAIT | NOWAIT

Specify `WAIT` for all disk handles to close all instances before offline
returns. The default wait timeout is 300 seconds (5 minutes).

rebalance_diskgroup_clause

Use this clause to manually rebalance the disk group. During a rebalance
operation, Oracle ASM redistributes data files evenly across all drives. This
clause is rarely necessary, because Oracle ASM allocates files evenly and
automatically rebalances disk groups when the storage configuration changes.
However, it is useful if you want to perform a controlled rebalance operation.
It allows you to include or exclude certain phases of a rebalance operation,
pause and restart a rebalance operation, and adjust the power of a rebalance
operation.

WITH | WITHOUT

A rebalance operation consists of the following phases: `RESTORE` (includes
the `RESYNC`, `RESILVER`, or `REBUILD` phases), `BALANCE`, `PREPARE`, and
`COMPACT`.

You can use the `WITH` or `WITHOUT` clause to instruct Oracle ASM to include
or exclude specific phases of a rebalance operation. For example, if you have
time constraints, you can include only the `RESTORE` phase. Or, if you are
using flash storage disk groups or disk groups with flash cache, you can
exclude the `COMPACT` phase, which is not beneficial for such disk groups.

  * Use the `WITH` clause to include only the specified phases of a rebalance operation. You can specify any of phases `RESTORE`, `BALANCE`, `PREPARE`, and `COMPACT`. It is acceptable, but not necessary, to specify `RESTORE`, because the `RESTORE` phase always occurs. 

  * Use the `WITHOUT` clause to exclude the specified phases of a rebalance operation. You can specify any of the phases `BALANCE`, `PREPARE`, and `COMPACT`. You cannot specify `RESTORE`, because the `RESTORE` phase must always occur. 

The order in which you specify multiple phases in the `WITH` or `WITHOUT`
clause does not matter. Oracle ASM will perform the phases of the rebalance
operation in the proper order. You cannot specify the `RESYNC`, `RESILVER`, or
`REBUILD` phases; they are part of the `RESTORE` phase.

If you omit the `WITH` and `WITHOUT` clauses, then Oracle ASM performs all
phases of the rebalance operation.

You can monitor the progress of the rebalance operation by querying the
`V$ASM_OPERATION` dynamic performance view.

See [Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG-GUID-020ABD10-8370-444C-9B44-71F2FF688861) for more
information on the phases of a rebalance operation.

POWER

This clause lets you specify the power, or speed, of the rebalance operation.
It also lets you stop the rebalance operation.

For `integer`, specify a value from `0` to `1024`:

  * A value of `1` through `1024` specifies the power at which Oracle ASM is to perform the rebalance operation, with `1` representing the lowest possible power and `1024` representing the highest possible power. 

  * A value of `0` stops an active rebalance operation. No further rebalancing will occur until the start of another manual or automatic rebalance operation on the disk group, and at that time the rebalance operation will start from the beginning. If you would like to have the option of later resuming the rebalance operation from where it left off, then instead stop the rebalance operation by specifying `MODIFY` `POWER` `0`. See the clause [MODIFY POWER](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__MODIFYPOWER-6173CE80) for more information. 

If you omit the `POWER` clause, then the default power is determined as
follows:

  * For flex disk groups, Oracle ASM rebalances each file group according the value of its `POWER_LIMIT` property. If the `POWER_LIMIT` property is not set for a file group, then Oracle ASM uses the value of the `ASM_POWER_LIMIT` initialization parameter for the file group. 

  * For all other types of disk groups, if you omit the `POWER` clause, then Oracle ASM rebalances the disk group according to the value of the `ASM_POWER_LIMIT` initialization parameter. 

WAIT | NOWAIT

Use this clause to specify when, in the course of the rebalance operation,
control should be returned to the user.

  * Specify `WAIT` if you want control returned to the user after the rebalance operation has finished. You can explicitly terminate a rebalance operation running in `WAIT` mode, although doing so does not undo any completed disk add, drop, or resize operations in the same statement. 

  * Specify `NOWAIT` if you want control returned to the user immediately after the statement is issued. This is the default. 

MODIFY POWER

Use this clause to pause, resume, or change the power of an active rebalance
operation.

You can specify `integer` as follows:

  * Specify `0` to pause the rebalance operation. When you pause a rebalance operation in this manner, you can subsequently resume the operation from the phase where it left off by issuing an `ALTER` `DISKGROUP` ... `MODIFY` `POWER` ... statement. If you subsequently start a manual rebalance operation on the disk group using the clause [POWER](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABCGEIH), or an automatic rebalance operation for the disk group occurs, then the rebalance operation will start at the beginning. 

  * Specify `1` through `1024` to specify the power of the rebalance operation, with `1` representing the lowest possible power and `1024` representing the highest possible power. If a rebalance operation is running, then Oracle ASM changes the power without interrupting the operation. If a rebalance operation was previously paused with the `MODIFY` `POWER` `0` clause, then the rebalance operation resumes at the specified power. 

  * Omit `integer` to specify the default power. If a rebalance operation is running, then Oracle ASM changes the power to the default power without interrupting the operation. If a rebalance operation was previously paused with the `MODIFY` `POWER` `0` clause, then the rebalance operation resumes at the default power. Refer to the clause [POWER](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABCGEIH) for information on how the default power is determined. 

See Also:

  * Oracle Database Reference for more information on the [`ASM_POWER_LIMIT`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN10246) initialization parameter and the [`V$ASM_OPERATION`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN30173) dynamic performance view 

  * [Rebalancing a Disk Group: Example](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEJBJJJ)

check_diskgroup_clause

The `check_diskgroup_clause` lets you verify the internal consistency of
Oracle ASM disk group metadata. The disk group must be mounted. Oracle ASM
displays summary errors and writes the details of the detected errors in the
alert log.

The `CHECK` keyword performs the following operations:

  * Checks the consistency of the disk.

  * Cross checks all the file extent maps and allocation tables for consistency.

  * Checks that the alias metadata directory and file directory are linked correctly.

  * Checks that the alias directory tree is linked correctly.

  * Checks that Oracle ASM metadata directories do not have unreachable allocated blocks.

REPAIR | NOREPAIR

This clause lets you instruct Oracle ASM whether or not to attempt to repair
any errors found during the consistency check. The default is `NOREPAIR`. The
`NOREPAIR` setting is useful if you want to be alerted to any inconsistencies
but do not want Oracle ASM to take any automatic action to resolve them.

Deprecated Clauses

In earlier releases, you could specify `CHECK` for `ALL`, `DISK`, `DISKS` `IN`
`FAILGROUP`, or `FILE`. Those clauses have been deprecated as they are no
longer needed. If you specify them, then their behavior is the same as in
earlier releases and a message is added to the alert log. However, Oracle
recommends that you do not introduce these clauses into your new code, as they
are scheduled for desupport. The deprecated clauses are these:

  * `ALL` checks all disks and files in the disk group. 

  * `DISK` checks one or more specified disks in the disk group. 

  * `DISKS` `IN` `FAILGROUP` checks all disks in a specified failure group. 

  * `FILE` checks one or more specified files in the disk group. You must use one of the reference forms of the filename. Refer to [ASM_filename](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1026664) for information on the reference forms of Oracle ASM filenames. 

diskgroup_template_clauses

A template is a named collection of attributes. When you create a disk group,
Oracle ASM associates a set of initial system default templates with that disk
group. The attributes defined by the template are applied to all files in the
disk group. [Table 10-2](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBCHIIF "The ASM
templates are listed along with their file type, various redundancy levels,
and striping level.") lists the system default templates and the attributes
they apply to the various file types. The `diskgroup_template_clauses`
described following the table let you change the template attributes and
create new templates.

You cannot use this clause to change the attributes of a disk group file after
it has been created. Instead, you must use Recovery Manager (RMAN) to copy the
file into a new file with the new attributes.

Table 10-2 Oracle Automatic Storage Management System Default File Group
Templates

Template Name | File Type | Mirroring Level in External Redundancy Disk Groups | Mirroring Level in Normal Redundancy Disk Groups | Mirroring Level in High Redundancy Disk Groups | Striped  
---|---|---|---|---|---  
`CONTROLFILE` |  Control files |  Unprotected |  3-way mirror |  3-way mirror |  `FINE`  
`DATAFILE` |  Data Files and copies |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`ONLINELOG` |  Online logs |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`ARCHIVELOG` |  Archive logs |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`TEMPFILE` |  Temp files |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`BACKUPSET` |  Data File backup pieces, data file incremental backup pieces, and archive log backup pieces |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`PARAMETERFILE` |  SPFILE |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`DATAGUARDCONFIG` |  Disaster recovery configurations (used in standby databases) |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`FLASHBACK` |  Flashback logs |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`CHANGETRACKING` |  Block change tracking data (used during incremental backups) |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`DUMPSET` |  Data Pump dumpset |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`XTRANSPORT` |  Cross-platform converted data file |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`AUTOBACKUP` |  Automatic backup files |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`ASMPARAMETERFILE` |  SPFILE |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
`OCRFILE` |  Oracle Cluster Registry file |  Unprotected |  2-way mirror |  3-way mirror |  `COARSE`  
  
ADD TEMPLATE

Use this clause to add one or more named templates to a disk group. To
determine the names of existing templates, query the
[`V$ASM_TEMPLATE`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30174) dynamic performance view.

MODIFY TEMPLATE

Use this clause to modify the attributes of a system default or user-defined
disk group template. Only the specified attributes are altered. Unspecified
properties retain their current values.

Note:

In earlier releases, the keywords `ALTER` `TEMPLATE` were used instead of
`MODIFY` `TEMPLATE`. The `ALTER` keyword is still supported for backward
compatibility, but is replaced with `MODIFY` for consistency with other Oracle
SQL.

template_name

Specify the name of the template to be added or modified. The maximum length
of a template name is 30 characters. The name must satisfy the requirements
listed in "[Database Object Naming Rules](Database-Object-Names-and-
Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

redundancy_clause

Specify `PARITY` for single parity protection for write-once file types like
archive logs and backup sets. If parity protection is not specified, the
default redundancy for write-once file types will continue to be derived from
system templates.

Specify `DOUBLE` for double parity for write-once file types like archive logs
and backup sets. If parity protection is not specified, the default redundancy
for write-once file types will continue to be derived from system templates.

Example:

    
    
    ALTER DISKGROUP <diskgroup_name> MODIFY TEMPLATE <archivelog> ATTRIBUTE (DOUBLE) 

The redundancy of write-once file types may be changed to support parity
protection later as needed.

Specify the redundancy level of the newly added or modified template:

  * `MIRROR`: Files to which this template are applied are protected by mirroring their data blocks. In normal redundancy disk groups, each primary extent has one mirror extent (2-way mirroring). For high redundancy disk groups, each primary extent has two mirror extents (3-way mirroring). You cannot specify `MIRROR` for templates in external redundancy disk groups. 

  * `HIGH`: Files to which this template are applied are protected by mirroring their data blocks. Each primary extent has two mirror extents (3-way mirroring) for both normal redundancy and high redundancy disk groups. You cannot specify `HIGH` for templates in external redundancy disk groups. 

  * `UNPROTECTED`: Files to which this template are applied are not protected by Automated Storage Management from media failures. Disks taken offline, either through system action or by user command, can cause loss of unprotected files. `UNPROTECTED` is the only valid setting for external redundancy disk groups. `UNPROTECTED` may not be specified for templates in high redundancy disk groups. Oracle discourages the use of unprotected files in high and normal redundancy disk groups. 

  * `PARITY`: Specify the property `PARITY` for single parity for write-once file types only. 

If you omit the redundancy clause, then the value defaults to `MIRROR` for a
normal redundancy disk group, `HIGH` for a high redundancy disk group, and
`UNPROTECTED` for an external redundancy disk group.

striping_clause

Specify how the files to which this template are applied will be striped:

  * `FINE`: Files to which this template are applied are striped every 128KB. This striping mode is not valid for an Oracle ASM spfile. 

  * `COARSE`: Files to which this template are applied are striped every 1MB. This is the default value. 

DROP TEMPLATE

Use this clause to drop one or more templates from the disk group. You can use
this clause to drop only user-defined templates, not system default templates.

diskgroup_directory_clauses

Before you can create alias names for Oracle ASM filenames (see
[diskgroup_alias_clauses](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168812)), you must
specify the full directory structure in which the alias name will reside. The
`diskgroup_directory_clauses` let you create and manipulate such a directory
structure.

ADD DIRECTORY

Use this clause to create a new directory path for hierarchically named
aliases. Use a slash (/) to separate components of the directory. Each
directory component can be up to 48 bytes in length and must not contain the
slash character. You cannot use a space for the first or last character of any
component. The total length of the directory path cannot exceed 256 bytes
minus the length of any alias name you intend to create in this directory (see
[diskgroup_alias_clauses](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168812)).

DROP DIRECTORY

Use this clause to drop a directory for hierarchically named aliases. Oracle
ASM will not drop the directory if it contains any alias definitions unless
you also specify `FORCE`. This clause is not valid for dropping directories
created as part of a system alias. Such directories are labeled with the value
`Y` in the `SYSTEM_CREATED` column of the
[`V$ASM_ALIAS`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30168) dynamic performance view.

RENAME DIRECTORY

Use this clause to change the name of a directory for hierarchically named
aliases. This clause is not valid for renaming directories created as part of
a system alias. Such directories are labeled with the value `Y` in the
`SYSTEM_CREATED` column of the
[`V$ASM_ALIAS`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30168) dynamic performance view.

diskgroup_alias_clauses

When an Oracle ASM file is created, either implicitly or by user
specification, Oracle ASM assigns to the file a fully qualified name ending in
a dotted pair of numbers (see
[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)).
The `diskgroup_alias_clauses` let you create more user-friendly alias names
for the Oracle ASM filenames. You cannot specify an alias name that ends in a
dotted pair of numbers, as this format is indistinguishable from an Oracle ASM
filename.

Before specifying this clause, you must first create the directory structure
appropriate for your naming conventions (see
[diskgroup_directory_clauses](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2175401)). The
total length of the alias name, including the directory prefix, is limited to
256 bytes. Alias names are case insensitive but case retentive.

ADD ALIAS

Use this clause to create an alias name for an Oracle ASM filename. The
`alias_name` consists of the full directory path and the alias itself. To
determine the names of existing Oracle ASM aliases, query the
[`V$ASM_ALIAS`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30168) dynamic performance view. Refer to
[ASM_filename](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1026664)
for information on Oracle ASM filenames.

DROP ALIAS

Use this clause to remove an alias name from the disk group directory. Each
alias name consists of the full directory path and the alias itself. The
underlying file to which the alias refers remains unchanged.

RENAME ALIAS

Use this clause to change the name of an existing alias. The `alias_name`
consists of the full directory path and the alias itself.

Restriction on Dropping and Renaming Aliases

You cannot drop or rename a system-generated alias. To determine whether an
alias was system generated, query the `SYSTEM_CREATED` column of the
[`V$ASM_ALIAS`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30168) dynamic performance view.

diskgroup_volume_clauses

Use these clauses to manipulate logical Oracle ASM Dynamic Volume Manager
(Oracle ADVM) volumes corresponding to physical volume devices. To use these
clauses, Oracle ASM must be started and the disk group being modified must be
mounted.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG32000) for more information about disk group
volumes, including examples

add_volume_clause

Use this clause to add a volume to the disk group.

For `asm_volume`, specify the name of the volume. The name can contain only
alphanumeric characters and the first character must be alphabetic. The
maximum length of the name is platform dependent. Refer to [Oracle Automatic
Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG94739) for more information.

For `size_clause`, specify the size of the Oracle ADVM volume. The Oracle ASM
instance determines whether sufficient space exists to create the volume. If
sufficient space does not exist, then the Oracle ASM instance returns an
error. If sufficient space does exist, then all nodes in the cluster with an
Oracle ASM instance running and the disk group mounted are notified of the
addition. Oracle ASM creates and enables on those nodes a volume device that
can be used to create and mount file systems.

The following optional settings are also available:

  * In the `redundancy_clause`, specify the redundancy level of the Oracle ADVM volume. You can specify this clause only when creating a volume in a normal redundancy disk group. You can specify the following volume redundancy levels: 

    * `MIRROR`: 2-way mirroring of the volume. This is the default. 

    * `HIGH`: 3-way mirroring of the volume. 

    * `UNPROTECTED`: No mirroring of the volume. 

You cannot specify the `redundancy_clause` when creating a volume in a high
redundancy disk group or an external redundancy disk group. If you do so, then
an error will result. In high redundancy disk groups, Oracle Database
automatically sets the volume redundancy to `HIGH` (3-way mirroring). In
external redundancy disk groups, Oracle Database automatically sets the volume
redundancy to `UNPROTECTED` (no mirroring).

  * In the `STRIPE_WIDTH` clause, specify a stripe width for the Oracle ADVM volume. The valid range is from 4KB to 1MB, at intervals of the power of 2. The default value is 128K. 

  * In the `STRIPE_COLUMNS` clause, specify the number of stripes in a stripe set of the Oracle ADVM volume. The valid range is 1 to 8. The default is 4. If `STRIPE_COLUMNS` is set to 1, then striping becomes disabled. In this case, the stripe width is the extent size of the volume. This volume extent size is 64 times the allocation unit (AU) size of the disk group. 

modify_volume_clause

Use this clause to modify the characteristics of an existing Oracle ADVM
volume. You must specify at least one of the following clauses:

  * In the `MOUNTPATH` clause, specify the mountpath name associated with the volume. The `mountpath_name` can be up to 1024 characters. 

  * In the `USAGE` clause, specify the usage name associated with the volume. The `usage_name` can be up to 30 characters. 

RESIZE VOLUME Clause

Use this clause to change the size of an existing Oracle ADVM volume. In an
Oracle ASM cluster, the new size is propagated to all nodes. If an Oracle
Advanced Cluster File System (ACFS) exists on the volume, then you must use
the `acfsutil` `size` command instead of the `ALTER` `DISKGROUP` statement.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG94000) for more information about the `acfsutil`
`size` command

DROP VOLUME Clause

Use this clause to remove the Oracle ASM file that is the storage container
for an existing Oracle ADVM volume. In an Oracle ASM cluster, all nodes with
an Oracle ASM instance running and with this disk group open are notified of
the drop operation, which results in removal of the volume device. If the
volume file is open, then this clause returns an error.

diskgroup_attributes

Use this clause to specify attributes for the disk group. [Table 13-2](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__BGEDFCIB "Column 1
lists diskgroup attribute names; column 2 lists valid values for each
attribute; column 3 describes the attributes.") lists the attributes you can
set with this clause. Refer to the `CREATE` `DISKGROUP` "[ATTRIBUTE
Clause](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__BABECECH)" for
information on the behavior of this clause.

drop_diskgroup_file_clause

Use this clause to drop a file from the disk group. Oracle ASM also drops all
aliases associated with the file being dropped. You must use one of the
reference forms of the filename. Most Oracle ASM files do not need to be
manually deleted because, as Oracle Managed Files, they are removed
automatically when they are no longer needed. Refer to
[ASM_filename](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1026664)
for information on the reference forms of Oracle ASM filenames.

You cannot drop a disk group file it if is the spfile that was used to start
up the current instance or any instance in the Oracle ASM cluster.

convert_redundancy_clause

You can use this clause to convert a `NORMAL` `REDUNDANCY` or `HIGH`
`REDUNDANCY` disk group to a `FLEX` `REDUNDANCY` disk group. The disk group
must have at least three failure groups before you start the conversion.

usergroup_clauses

Use these clauses to add a user group to the disk group, remove a user group
from the disk group, or to add a member to or drop a member from an existing
user group.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG02660) for detailed information about user groups
and members, including examples

ADD USERGROUP

Use this clause to add a user group to the disk group. You must have `SYSASM`
or `SYSDBA` privilege to create a user group. The maximum length of a user
group name is 63 bytes. If you specify the user name, then it must be in the
OS password file and its length cannot exceed 32 characters.

MODIFY USERGROUP

Use these clauses to add a member to or drop a member from an existing user
group. You must be an Oracle ASM administrator (with SYSASM privilege) or the
creator (with SYSDBA privilege) of the user group to use these clauses. The
user name must be an existing user in the OS password file.

DROP USERGROUP

Use this clause to drop an existing user group from the disk group. You must
be an Oracle ASM administrator (with SYSASM privilege) or the creator (with
SYSDBA privilege) of the user group to use this clause. Dropping a user group
may leave a disk group file without a valid user group. In this case, you can
update the disk group file manually to add a new, valid group using the
[file_permissions_clause](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGBJGAFA).

user_clauses

Use these clauses to add a user to, drop a user from, or replace a user in a
disk group.

Note:

When administering users with SQL*Plus, the users must be existing operating
system users and their user names must have corresponding operating system
user IDs. However, only users in the same cluster as the Oracle ASM instance
can be validated.

ADD USER

Use this clause to add one or more operating system (OS) users to an Oracle
ASM disk group and give those users access privileges on the disk group. A
user name must be an existing user in the OS password file and its length
cannot exceed 32 characters. If a specified user already exists in the disk
group, as shown by `V$ASM_USER`, then the command records an error and
continues to add other users, if any have been specified. This command is
seldom needed, because the OS user running the database instance is added to a
disk group automatically when the instance accesses the disk group. However,
this clause is useful when adding users that are not associated with a
particular database instance.

DROP USER

Use this clause to drop one or more users from the disk group. If a specified
user is not in the disk group, then this clause records an error and continues
to drop other users, if any are specified. If the user owns any files, then
you must specify the `CASCADE` keyword, which drops the user and all the
user's files. If any files owned by the user are open, then `DROP` `USER`
`CASCADE` fails with an error.

To delete a user without deleting the files owned by that user, change the
owner of each of these files to another user and then issue an `ALTER`
`DISKGROUP` ... `DROP` `USER` statement on the user. Alternatively, you can
issue an `ALTER` `DISKGROUP` ... `REPLACE` `USER` statement to replace the
user you want to drop with a user that currently does not exist in the disk
group. This operation has the side effect of making the new user the owner of
files that were previously owned by the dropped user.

REPLACE USER

Use this clause to replace `old_user` with `new_user` in the disk group. All
files that are currently owned by `old_user` will become owned by `new_user`,
and `old_user` will be dropped from the disk group. `old_user` must exist in
the disk group and `new_user` must not exist in the disk group.

file_permissions_clause

Use this clause to change the permission settings of a disk group file. The
three classes of permissions are owner, user group, and other. You must be the
file owner or the Oracle ASM administrator to use this clause.

If you change the permission settings of an open file, then the operation
currently running on the file will complete using the old permission settings.
The new permission settings will take effect when re-authentication is
required.

file_owner_clause

Use this clause to set the owner or user group for a specified file. You must
be the Oracle ASM administrator to change the owner of the file. You must be
the owner of the file or the Oracle ASM administrator to change the user group
of a file. In addition, to change the associated user group of a file, the
specified user group must already exist in the disk group, and the owner of
the file must be a member of that user group.

If you use this clause on an open file, then the following conditions apply:

  * If you change the owner or user group of an open file, then the operation currently running on the file will complete using the old owner or user group. The new owner or user group will take effect when re-authentication is required.

  * If you change the owner of an open file, then the new owner of the file cannot be dropped from the disk group until the instance has been restarted. In an Oracle ASM cluster, the new owner of the file cannot be dropped until all instances in the cluster have been restarted.

  * If you change the owner of an open file, then the old owner cannot be dropped while the file is still open, even after the ownership of the file has changed.

scrub_clause

Use this clause to scrub a disk group. The scrub operation checks for logical
data corruptions and repairs the corruptions automatically in normal and high
redundancy disks groups.

  * Use the `FILE` clause to scrub the specified Oracle ASM file in the disk group. You must use one of the reference forms of the `ASM_filename`. Refer to [ASM_filename](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__I1026664) for information on the reference forms of Oracle ASM filenames. 

  * Use the `DISK` clause to scrub the specified disk in the disk group. 

  * If you do not specify `FILE` or `DISK`, then all files and disks in the disk group are scrubbed. 

REPAIR | NOREPAIR

Specify `REPAIR` to attempt to repair any errors found during the logical data
corruption check. Specify `NOREPAIR` to be alerted of any corruptions; Oracle
ASM will not take any action to resolve them. The default is `NOREPAIR`.

POWER

Use the `POWER` clause to specify the power level of the scrub operation.
Valid values are `AUTO`, `LOW`, `HIGH`, and `MAX`. If you omit this clause,
then the power level defaults to `AUTO` and the power adjusts to the optimum
level for the system.

WAIT | NOWAIT

Specify `WAIT` to allow the scrub operation to complete before returning
control to the user. Specify `NOWAIT` to add the operation to the scrubbing
queue and return control to the user immediately. The default is `NOWAIT`.

FORCE | NOFORCE

Specify `FORCE` to process the command even if the system I/O load is high or
scrubbing has been disabled at the system level. Specify `NOFORCE` to process
the command normally. The default is `NOFORCE`.

STOP

Specify `STOP` if you want to stop an ongoing scrub operation.

You can monitor the progress of the scrub operation by querying the `V$ASM_
OPERATION` dynamic performance view.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG95351) for more information on scrubbing disk groups
and "[Scrubbing a Disk Group: Example](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BGEFHBEA)"

quotagroup_clauses

Use these clauses to add a quota group to the disk group, modify a quota
group, move a file group into a quota group, or drop a quota group.

A quota group is a collection of file groups. A file group is a container for
all files of a database within one disk group. A quota group has a specified
quota limit, which is the maximum amount of storage space that its file groups
can collectively use. Therefore, a quota group enables you to define the quota
limit for a group of databases within a disk group. The sum of the quota
limits for all quota groups in a disk group can exceed the storage capacity of
the disk group.

Each disk group contains a default quota group named `GENERIC`. If you create
a file group and do not specify its quota group, then the file group belongs
to the `GENERIC` quota group. Oracle ASM automatically creates the `GENERIC`
quota group when you create a disk group with the `compatible`.`asm` attribute
set to `12`.`2` or higher, or when you set `compatible`.`asm` to `12`.`2` or
higher for an existing disk group. Initially, the quota limit for `GENERIC` is
`UNLIMITED`. You can subsequently modify this quota limit with the `MODIFY`
`QUOTAGROUP` clause.

ADD QUOTAGROUP

Use this clause to create a quota group and add it to the disk group. For
`quotagroup_name`, specify the name of the new quota group.

The `SET` clause allows you to set the quota limit for the quota group.

  * For `property_name`, specify `QUOTA`. 

  * For `property_value`, specify one of the following clauses: 

    * Specify `size_clause` to set a number of bytes for the quota limit. The minimum value you can specify is 1 byte. You can specify a value that is greater than the storage size of the disk group. In this case, storage use is limited by the current size of the disk group. However, if you subsequently increase the storage space for the disk group to a size that exceeds the quota limit, then the quota limit will be enforced. Refer to [size_clause](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517) for the syntax and semantics of this clause. Note that specifying 0 bytes is equivalent to specifying `UNLIMITED`. 

    * Specify `UNLIMITED` if you do not want to set a quota limit. In this case, storage use is limited by the storage size of the disk group. 

If you omit the `SET` clause, then the default is `SET QUOTA=UNLIMITED`.

MODIFY QUOTAGROUP

Use this clause to modify the quota limit for a quota group. For
`quotagroup_name`, specify the name of the quota group you want to modify. You
can modify the quota limit for any quota group, including the `GENERIC` quota
group. The `SET` clause has the same semantics here as for the `ADD`
`QUOTAGROUP` clause. The quota limit can be set below the amount of space
currently used by the quota group. This action prevents any additional space
from being allocated for files described by file groups associated with this
quota group.

MOVE FILEGROUP

Use this clause to move a file group from one quota group to another. For
`filegroup_name`, specify the file group you want to move. For
`quotagroup_name`, specify the name of the destination quota group. If the
move operation causes the amount of used storage space in the destination
quota group to exceed the quota limit, then the operation succeeds, but no new
storage allocations can take place in the file groups within the quota group.
This capability enables you to stop any files described by a specific file
group from allocating additional space.

DROP QUOTAGROUP

Use this clause to drop a quota group from the disk group. For
`quotagroup_name`, specify the quota group you want to drop. The quota group
must not contain any file groups. You cannot drop the quota group `GENERIC`.

See Also:

[Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG-GUID-A4AA7D67-082F-402D-8164-53193B405211) for more
information on quota groups

filegroup_clauses

The `filegroup_clauses` are valid only for flex disk groups. Use these clauses
to create a file group, modify a file group, move a file into a file group, or
drop a file group. A file group is a container for all files of a database
within one disk group. A file group must belong to a quota group.

Each disk group has a default file group with `FILEGROUP_NUMBER` `=` `0`.

add_filegroup_clause

Use this clause to create a file group.

For `filegroup_name`, specify the name of the new file group. The maximum
length of a file group name is 127 characters. The name must satisfy the
requirements listed in "[Database Object Naming Rules](Database-Object-Names-
and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)", with the
following addition: File group names are not case sensitive, even if you
specify them with quotation marks. They are always stored internally as
uppercase. File group names must be unique within a disk group.

  * Use the `DATABASE` clause to specify the database (non-CDB, CDB, or PDB) with which the file group is associated. 

  * Use the `CLUSTER` clause to specify the cluster with which the file group is associated. 

  * Use the `VOLUME` clause to specify the volume with which the file group is associated. 

  * Use the `TEMPLATE` clause to create a file group template with which the file group is associated. You can use the template to customize a set of file group properties, that can then be inherited by one or more databases. 

You cannot associate more than one file group in the same disk group with the
same database, cluster, volume, or template. If the database, cluster, volume,
or template does not exist at the time of file group creation, then the file
group will be automatically associated with it when it is subsequently
created. Database, cluster, volume, and template names must satisfy the
requirements listed in "[Database Object Naming Rules](Database-Object-Names-
and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)".

The `SET` clause allows you to set properties for the file group. If you do
not specify the `SET` clause for a property, then the default value is
assigned. You can specify the `file_type` for any property for which a file
type applies. If you do not specify `file_type` for such a property, then the
property applies to all file types. For complete information on file group
properties and their default values, see [Oracle Automatic Storage Management
Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG-GUID-BE9083C8-A5DF-48CD-BB32-C8A6FCDA3E7B).

Example 1: Create a file group from a file group template to inherit
properties from the template

    
    
    ALTER DISKGROUP hmdg ADD FILEGROUP fgtem TEMPLATE SET 'datafile.redundancy'='unprotected'
        ALTER DISKGROUP hmdg ADD FILEGROUP fgdb DATABASE NONE FROM TEMPLATE fgtem

Example 2: Create a file group or a tablespace from a file group template to
inherit properties from the template

    
    
    ALTER DISKGROUP hmdg ADD FILEGROUP fgtem2 TEMPLATE 
        CREATE TABLESPACE tbs1 datafile '+hmdg(fg$fgtem2)/dbs/tbs1.f' size 1M

modify_filegroup_clause

Use this clause to modify file group properties. For `filegroup_name`, specify
the name of the file group you want to modify. You can modify properties for
any file group, including the default file group. Any that you do not specify
with this clause remain unchanged. The `SET` clause has the same semantics
here as for the `add_filegroup_clause`.

move_to_filegroup_clause

Use this clause to move a file to a file group. If the file is currently
associated with a different file group, then it is disassociated from that
file group. The target file group must have enough space available to contain
the file. You must be the owner of the file and the target file group.

drop_filegroup_clause

Use this clause to drop an empty file group. For `filegroup_name`, specify the
name of the file group you want to drop.

CASCADE

Use the keyword `CASCADE` to drop a file group that is not empty. When a file
group is dropped with the keyword `CASCADE`, every file associated with the
file group is automatically dropped.

FOR DATABASE Clause

  * If the file group being dropped is associated with a pluggable database, then the `FOR PLUGGABLE DATABASE` clause names the pluggable database in `pdb_name`. You must then specify the `FOR DATABASE` clause with `db_unique_name`, the name of the container database that contains the pluggable database. 

  * If the file group being dropped is associated with a non-CDB database, then the `FOR DATABASE` clause names the non-CDB database in `db_unique_name`. 

  * You can specify the `CASCADE` clause with `FOR PLUGGABLE DATABASE` and `FOR DATABASE`. 

Use the `CASCADE` option to delete every file associated with the file group
as part of the file group drop.

When a file group of type `DATABASE` is dropped using the `CASCADE` option,
ASM checks the OMF (Oracle Managed File) file name of the files being deleted
to verify that they belong to the database or pluggable database that is
associated with the file group being dropped.

See Also:

[Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG-GUID-B2AC119F-BFFE-4288-A721-E8B97D574632) for more
information on file groups

undrop_disk_clause

Use this clause to cancel the drop of disks from the disk group. You can
cancel the pending drop of all the disks in one or more disk groups (by
specifying `diskgroup_name`) or of all the disks in all disk groups (by
specifying `ALL`).

This clause is not relevant for disks that have already been completely
dropped from the disk group or for disk groups that have been completely
dropped. This clause results in a long-running operation. You can see the
status of the operation by querying the `V$ASM_OPERATION` dynamic performance
view.

See Also:

[`V$ASM_OPERATION`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN30173) for more information on the details of long-
running Oracle ASM operations

diskgroup_availability

Use this clause to make one or more disk groups available or unavailable to
the database instances running on the same node as the Oracle ASM instance.
This clause does not affect the status of the disk group on other nodes in a
cluster.

MOUNT

Specify `MOUNT` to mount the disk groups in the local Oracle ASM instance.
Specify `ALL` `MOUNT` to mount all disk groups specified in the
`ASM_DISKGROUPS` initialization parameter. File operations can only be
performed when a disk group is mounted. If Oracle ASM is running in a cluster
or a standalone server managed by Oracle Grid Infrastructure for a standalone
server, then the `MOUNT` clause automatically brings the corresponding
resource online.

RESTRICTED | NORMAL

Use these clauses to determine the manner in which the disk groups are
mounted.

  * In the `RESTRICTED` mode, the disk group is mounted in single-instance exclusive mode. No other Oracle ASM instance in the same cluster can mount that disk group. In this mode the disk group is not usable by any Oracle ASM client. 

  * In the `NORMAL` mode, the disk group is mounted in shared mode, so that other Oracle ASM instances and clients can access the disk group. This is the default. 

FORCE | NOFORCE

Use these clauses to determine the circumstances under which the disk groups
are mounted.

  * In the `FORCE` mode, Oracle ASM attempts to mount the disk group even if it cannot discover all of the devices that belong to the disk group. This setting is useful if some of the disks in a normal or high redundancy disk group became unavailable while the disk group was dismounted. When `MOUNT` `FORCE` succeeds, Oracle ASM takes the missing disks offline. 

If Oracle ASM discovers all of the disks in the disk group, then `MOUNT`
`FORCE` fails. Therefore, use the `MOUNT` `FORCE` setting only if some disks
are unavailable. Otherwise, use `NOFORCE`.

In normal- and high-redundancy disk groups, disks from one failure group can
be unavailable and `MOUNT` `FORCE` will succeed. Also in high-redundancy disk
groups, two disks in two different failure groups can be unavailable and
`MOUNT` `FORCE` will succeed. Any other combination of unavailable disks
causes the operation to fail, because Oracle ASM cannot guarantee that a valid
copy of all user data or metadata exists on the available disks.

  * In the `NOFORCE` mode, Oracle ASM does not attempt to mount the disk group unless it can discover all the member disks. This is the default. 

See Also:

[`ASM_DISKGROUPS`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN10247) for more information about adding disk group
names to the initialization parameter file

DISMOUNT

Specify `DISMOUNT` to dismount the specified disk groups. Oracle ASM returns
an error if any file in the disk group is open unless you also specify
`FORCE`. Specify `ALL` `DISMOUNT` to dismount all currently mounted disk
groups. File operations can only be performed when a disk group is mounted. If
Oracle ASM is running in a cluster or a standalone server managed by Oracle
Grid Infrastructure for a standalone server, then the `DISMOUNT` clause
automatically takes the corresponding resource offline.

FORCE

Specify `FORCE` if you want Oracle ASM to dismount the disk groups even if
some files in the disk group are open.

enable_disable_volume

Use this clause to enable or disable one or more volumes in the disk group.

  * For each volume you enable, Oracle ASM creates a volume device file on the local node that can be used to create or mount the file system.

  * For each volume you disable, Oracle ASM deletes the device file on the local node. If the volume file is open on the local node, then the `DISABLE` clause returns an error. 

Use the `ALL` keyword to enable or disable all volumes in the disk group. If
you specify `ALTER` `DISKGROUP` `ALL` `...`, then you must use the `ALL`
keyword in this clause as well.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG32000) for more information about disk group volumes

Examples

The following examples require a disk group called `dgroup_01`. They assume
that `ASM_DISKSTRING` is set to `/devices/disks/*`. In addition, they assume
the Oracle user has read/write permission to `/devices/disks/d100`. Refer to
"[Creating a Diskgroup: Example](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__CACIHAAD)" to create
`dgroup_01`.

Adding a Disk to a Disk Group: Example

To add a disk, `d100`, to a disk group, `dgroup_01`, issue the following
statement:

    
    
    ALTER DISKGROUP dgroup_01
      ADD DISK '/devices/disks/d100';

Dropping a Disk from a Disk Group: Example

To drop a disk, `dgroup_01_0000`, from a disk group, `dgroup_01`, issue the
following statement:

    
    
    ALTER DISKGROUP dgroup_01
      DROP DISK dgroup_01_0000;

Undropping a Disk from a Disk Group: Example

To cancel the drop of disks from a disk group, `dgroup_01`, issue the
following statement:

    
    
    ALTER DISKGROUP dgroup_01
      UNDROP DISKS;

Resizing a Disk Group: Example

To resize every disk in a disk group, `dgroup_01`, issue the following
statement:

    
    
    ALTER DISKGROUP dgroup_01
      RESIZE ALL
      SIZE 36G;

Rebalancing a Disk Group: Example

To manually rebalance a disk group, `dgroup_01`, and permit Oracle ASM to
execute the rebalance as fast as possible, issue the following statement:

    
    
    ALTER DISKGROUP dgroup_01
      REBALANCE POWER 11 WAIT;
    

The `WAIT` keyword causes the database to wait for the disk group to be
rebalanced before returning control to the user.

Verifying the Internal Consistency of Disk Group Metadata: Example

To verify the internal consistency of Oracle ASM disk group metadata and
instruct Oracle ASM to repair any errors found, issue the following statement:

    
    
    ALTER DISKGROUP dgroup_01
      CHECK ALL
      REPAIR;

Adding a Named Template to a Disk Group: Example

To add a named template, `template_01` to a disk group, `dgroup_01`, issue the
following statement:

    
    
    ALTER DISKGROUP dgroup_01
      ADD TEMPLATE template_01
        ATTRIBUTES (UNPROTECTED COARSE);

Changing the Attributes of a Disk Group Template: Example

To modify the attributes of a system default or user-defined disk group
template, `template_01`, issue the following statement:

    
    
    ALTER DISKGROUP dgroup_01
      MODIFY TEMPLATE template_01
        ATTRIBUTES (FINE);

Dropping a User-Defined Template from a Disk Group: Example

To drop a user-defined template, `template_01`, from a disk group,
`dgroup_01`, issue the following statement:

    
    
    ALTER DISKGROUP dgroup_01
      DROP TEMPLATE template_01;

Creating a Directory Path for Hierarchically Named Aliases: Example

To specify the directory structure in which alias names will reside, issue the
following statement:

    
    
    ALTER DISKGROUP dgroup_01
      ADD DIRECTORY '+dgroup_01/alias_dir';

Creating an Alias Name for an Oracle ASM Filename: Example

To create a user alias by specifying the numeric Oracle ASM filename, issue
the following statement:

    
    
    ALTER DISKGROUP dgroup_01
      ADD ALIAS '+dgroup_01/alias_dir/datafile.dbf'
        FOR '+dgroup_01.261.1';

Scrubbing a Disk Group: Example

To scrub a disk group, `dgroup_01`, issue the following statement. This
statement attempts to repair any errors found during the logical data
corruption check and allows the scrub operation to complete before returning
control to the user.

    
    
    ALTER DISKGROUP dgroup_01
      SCRUB REPAIR WAIT;

Dismounting a Disk Group: Example

To dismount a disk group, `dgroup_01`, issue the following statement. This
statement dismounts the disk group even if one or more files are active:

    
    
    ALTER DISKGROUP dgroup_01
      DISMOUNT FORCE;

Mounting a Disk Group: Example

To mount a disk group, `dgroup_01`, issue the following statement:

    
    
    ALTER DISKGROUP dgroup_01
      MOUNT;


[← Previous](ALTER-DIMENSION.md)

[Next →](alter-domain.md)
