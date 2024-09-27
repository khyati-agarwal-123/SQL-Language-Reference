[Previous](CREATE-DIRECTORY.md) [Next](create-domain.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: COMMIT to CREATE JAVA](SQL-Statements-COMMIT-to-CREATE-JAVA.md)
  3. CREATE DISKGROUP 

## CREATE DISKGROUP

The script content on this page is for navigation purposes only and does not
alter the content in any way.

Note:

This SQL statement is valid only if you are using Oracle ASM and you have
started an Oracle ASM instance. You must issue this statement from within the
Oracle ASM instance, not from a normal database instance. For information on
starting an Oracle ASM instance, refer to [Oracle Automatic Storage Management
Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG036).

Purpose

Use the `CREATE` `DISKGROUP` clause to name a group of disks and specify that
Oracle Database should manage the group for you. Oracle Database manages a
disk group as a logical unit and evenly spreads each file across the disks to
balance I/O. Oracle Database also automatically distributes database files
across all available disks in disk groups and rebalances storage automatically
whenever the storage configuration changes.

This statement creates a disk group, assigns one or more disks to the disk
group, and mounts the disk group for the first time. Note that `CREATE`
`DISKGROUP` only mounts a disk group on the local node. If you want Oracle ASM
to mount the disk group automatically in subsequent instances, then you must
add the disk group name to the value of the `ASM_DISKGROUPS` initialization
parameter in the initialization parameter file. If you use an `SPFILE`, then
the disk group is added to the initialization parameter automatically.

See Also:

  * [ALTER DISKGROUP](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557) for information on modifying disk groups 

  * [Oracle Automatic Storage Management Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=OSTMG036) for information on Oracle ASM and using disk groups to simplify database administration 

  * [`ASM_DISKGROUPS`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN10247) for more information about adding disk group names to the initialization parameter file 

  * [`V$ASM_OPERATION`](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=REFRN30173) for information on monitoring Oracle ASM operations 

  * [DROP DISKGROUP](DROP-DISKGROUP.md#GUID-6F77FABB-3365-448F-8E2B-9B776904182C) for information on dropping a disk group 

Prerequisites

You must have the `SYSASM` system privilege to issue this statement.

Before issuing this statement, you must format the disks using an operating
system format utility. Also ensure that the Oracle Database user has
read/write permission and the disks can be discovered using the
`ASM_DISKSTRING`.

When you store your database files in Oracle ASM disk groups, rather than in a
file system, before the database instance can access your files in the disk
groups, you must configure and start up an Oracle ASM instance to manage the
disk groups.

Each database instance communicates with a single Oracle ASM instance on the
same node as the database. Multiple database instances on the same node can
communicate with a single Oracle ASM instance.

Syntax

create_diskgroup::=

![Description of create_diskgroup.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_diskgroup.gif)  
[Description of the illustration
create_diskgroup.eps](img_text/create_diskgroup.md)

qualified_disk_clause::=

![Description of qualified_disk_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/qualified_disk_clause.gif)  
[Description of the illustration
qualified_disk_clause.eps](img_text/qualified_disk_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

diskgroup_name

Specify the name of the disk group. The name must satisfy the requirements
listed in "[Database Object Naming Rules](Database-Object-Names-and-
Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)". However, disk
groups are not schema objects.

Note:

Oracle does not recommend using quoted identifiers for disk group names. These
quoted identifiers are accepted when issuing the `CREATE` `DISKGROUP`
statement in SQL*Plus, but they may not be valid when using other tools that
manage disk groups.

REDUNDANCY Clause

The `REDUNDANCY` clause lets you specify the redundancy level of the disk
group.

  * `NORMAL` `REDUNDANCY` requires the existence of at least two failure groups (see the `FAILGROUP` clause that follows). Oracle ASM provides redundancy for all files in the disk group according to the attributes specified in the disk group templates. `NORMAL` `REDUNDANCY` disk groups can tolerate the loss of one group. Refer to `ALTER` `DISKGROUP` ... [diskgroup_template_clauses](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__I2168808) for more information on disk group templates. 

`NORMAL` `REDUNDANCY` is the default if you omit the `REDUNDANCY` clause.
Therefore, if you omit this clause, you must create at least two failure
groups, or the create operation will fail.

  * `HIGH` `REDUNDANCY` requires the existence of at least three failure groups. Oracle ASM fixes mirroring at 3-way mirroring, with each extent getting two mirrored copies. `HIGH` `REDUNDANCY` disk groups can tolerate the loss of two failure groups. 

  * `FLEX` `REDUNDANCY` is a type of disk group that allows a database to specify its own redundancy after the disk group is created. A file's redundancy can also be changed after its creation. This type of disk group supports Oracle ASM file groups and quota groups. A flex disk group requires the existence of at least three failure groups. If a flex disk group has fewer than five failure groups, then it can tolerate the loss of one; otherwise, it can tolerate the loss of two failure groups. To create a flex disk group, the `COMPATIBLE`.`ASM` and `COMPATIBLE`.`RDBMS` disk group attributes must be set to `12`.`2` or greater. 

  * `EXTENDED` `REDUNDANCY` is a disk group that has all the features of a flex disk group in addition to being highly available in an extended cluster environment. The cluster contains nodes that span multiple physically separated sites. For more see [About Oracle ASM Extended Disk Groups](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=OSMTG-GUID-5A0CD2C9-3BE4-45FB-B5B6-5CD58D7F89EA)

You can use the `SITE` keyword to specify the redundancy of files and file
groups in an extended disk group for each site, rather than for each disk
group.

  * `EXTERNAL` `REDUNDANCY` indicates that Oracle ASM does not provide any redundancy for the disk group. The disks within the disk group must provide redundancy (for example, using a storage array), or you must be willing to tolerate loss of the disk group if a disk fails (for example, in a test environment). You cannot specify the `FAILGROUP` clause if you specify `EXTERNAL` `REDUNDANCY`. 

You cannot change the redundancy level after the disk group has been created,
with the following exception: You can convert a normal or high redundancy disk
group to a flex disk group. For more information, see the
[convert_redundancy_clause](ALTER-
DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__CONVERT_REDUNDANCY_CLAUSE-57C1BAB2)
of `ALTER` `DISKGROUP`.

QUORUM | REGULAR

Use these keywords to qualify either failure group or disk specifications.

  * `REGULAR` disks, or disks in non-quorum failure groups, can contain any files. 

  * `QUORUM` disks, or disks in quorum failure groups, cannot contain any database files, the Oracle Cluster Registry (OCR), or dynamic volumes. However, `QUORUM` disks can contain the voting file for Cluster Synchronization Services (CSS). Oracle ASM uses quorum disks or disks in quorum failure groups for voting files whenever possible. 

A quorum failure group is not considered when determining redundancy
requirements with respect to storing user data.

If you specify neither keyword, then `REGULAR` is the default.

Specify either `QUORUM` or `REGULAR` before the keyword `FAILGROUP` if you are
explicitly specifying the failure group. If you are creating a disk group with
implicitly created failure groups, then specify these keywords before the
keyword `DISK`.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG137) for more information about quorum and regular
disks and failure groups

FAILGROUP Clause

Use this clause to specify a name for one or more failure groups. If you omit
this clause, and you have specified `NORMAL` or `HIGH` `REDUNDANCY`, then
Oracle Database automatically adds each disk in the disk group to its own
failure group. The implicit name of the failure group is the same as the
operating system independent disk name (see "[NAME Clause](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__I2177129)").

You cannot specify this clause if you are creating an `EXTERNAL` `REDUNDANCY`
disk group.

qualified_disk_clause

Specify `DISK` `qualified_disk_clause` to add a disk to a disk group.

search_string

For each disk you are adding to the disk group, specify the operating system
dependent search string that Oracle ASM will use to find the disk. The
`search_string` must point to a subset of the disks returned by discovery
using the strings in the `ASM_DISKSTRING` initialization parameter. If
`search_string` does not point to any disks the Oracle Database user has
read/write access to, then Oracle ASM returns an error. If it points to one or
more disks that have already been assigned to a different disk group, then
Oracle Database returns an error unless you also specify `FORCE`.

For each valid candidate disk, Oracle ASM formats the disk header to indicate
that it is a member of the new disk group.

See Also:

``The [`ASM_DISKSTRING`](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=REFRN10248) initialization parameter for more information
on specifying the search string

NAME Clause

The `NAME` clause is valid only if the `search_string` points to a single
disk. This clause lets you specify an operating system independent name for
the disk. The name can be up to 30 characters long and can contain only
alphanumeric characters. The first character must be alphabetic. If you omit
this clause and you assigned a label to a disk through ASMLIB, then that label
is used as the disk name. If you omit this clause and you did not assign a
label through ASMLIB, then Oracle ASM creates a default name of the form
`diskgroupname_####`, where `####` is the disk number. You use this name to
refer to the disk in subsequent Oracle ASM operations.

SIZE Clause

Use this clause to specify in bytes the size of the disk. If you specify a
size greater than the capacity of the disk, then Oracle ASM returns an error.
If you specify a size less than the capacity of the disk, then you limit the
disk space Oracle ASM will use. The size value must be identical for all disks
in a disk group. If you omit this clause, then Oracle ASM attempts
programmatically to determine the size of the disk.

FORCE

Specify `FORCE` if you want Oracle ASM to add the disk to the disk group even
if the disk is already a member of a different disk group.

Note:

Using `FORCE` in this way may destroy existing disk groups.

For this clause to be valid, the disk must already be a member of a disk group
and the disk cannot be part of a mounted disk group.

NOFORCE

Specify `NOFORCE` if you want Oracle ASM to return an error if the disk is
already a member of a different disk group. `NOFORCE` is the default.

ATTRIBUTE Clause

Use this clause to set attribute values for the disk group. You can view the
current attribute values by querying the `V$ASM_ATTRIBUTE` view. [Table
13-2](CREATE-
DISKGROUP.md#GUID-039A1373-1F3F-4A53-A152-8EBC348FB880__BGEDFCIB "Column 1
lists diskgroup attribute names; column 2 lists valid values for each
attribute; column 3 describes the attributes.") lists the attributes you can
set with this clause. All attribute values are strings.

Table 13-2 Disk Group Attributes

Attribute | Valid Values | Description  
---|---|---  
`ACCESS_CONTROL.ENABLED` |  `true` or `false` |  Specifies whether Oracle ASM File Access Control is enabled for a disk group. If set to `true`, accessing Oracle ASM files is subject to access control. If `false`, any user can access every file in the disk group. All other operations behave independently of this attribute. The default value is `false`.  If both the `compatible.rdbms` and `compatible.asm` attributes are set to at least 11.2, you can set this attribute in an `ALTER` `DISKGROUP` ... `SET` `ATTRIBUTE` statement. You cannot set this attribute when creating a disk group.  When you set up file access control on an existing disk group, the files previously created remain accessible by everyone, unless you run the `ALTER` `DISKGROUP` `SET` `PERMISSION` statement to restrict the permissions.  Note: This attribute is used in conjunction with `ACCESS_CONTROL`.`UMASK` to manage Oracle ASM File Access Control. After setting the `ACCESS_CONTROL`.`ENABLED` disk attribute, you must set permissions with the `ACCESS_CONTROL`.`UMASK` attribute.   
`ACCESS_CONTROL.UMASK` |  A three-digit number where each digit is 0, 2, or 6. |  Determines which permissions are masked out on the creation of an Oracle ASM file for the user that owns the file (first digit), users in the same user group (second digit), and others not in the user group (third digit). This attribute applies to all files on a disk group. Setting to 0 masks out nothing. Setting to 2 masks out write permission. Setting to 6 masks out both read and write permissions. The default value is `066`.  If both the `compatible.rdbms` and `compatible.asm` attributes are set to at least 11.2, you can set this attribute in an `ALTER` `DISKGROUP` ... `SET` `ATTRIBUTE` statement. You cannot set this attribute when creating a disk group.  When you set up file access control on an existing disk group, the files previously created remain accessible by everyone, unless you run the `ALTER` `DISKGROUP` `SET` `PERMISSION` statement to restrict the permissions.  Note: This attribute is used in conjunction with `ACCESS_CONTROL`.`ENABLED` to manage Oracle ASM File Access Control. Before setting `ACCESS_CONTROL`.`UMASK`, you must set `ACCESS_CONTROL`.`ENABLED` to `true`.   
`AU_SIZE` |  Size in bytes. Valid values are powers of 2 from 1M to 64M. Examples '4M', '4194304'. |  Specifies the allocation unit size. This attribute can be set only during disk group creation; it cannot be modified with an `ALTER` `DISKGROUP` statement.   
`COMPATIBLE.ADVM` |  Valid Oracle Database version numberFoot 1 |  Determines whether the disk group can contain Oracle ADVM volumes. The value must be set to `11`.`2` or higher. Before setting this attribute, the `COMPATIBLE`.`ASM` value must be `11`.`2` or higher. Also, the Oracle ADVM volume drivers must be loaded.  By default, the value of the `COMPATIBLE`.`ADVM` attribute is empty until set.   
`COMPATIBLE.ASM` |  Valid Oracle Database version numberFoot 1 |  Determines the minimum software version for an Oracle ASM instance that can use the disk group. This setting also affects the format of the data structures for the Oracle ASM metadata on the disk. For Oracle ASM in Oracle Database 11g, `10`.`1` is the default setting for the `COMPATIBLE`.`ASM` attribute when using the SQL `CREATE` `DISKGROUP` statement, the ASMCMD mkdg command, and Oracle Enterprise Manager Create Disk Group page. When creating a disk group with ASMCA, the default setting is `11`.`2`.   
`COMPATIBLE.RDBMS` |  Valid Oracle Database version numberFoot 1 |  Determines the minimum `COMPATIBLE` database initialization parameter setting for any database instance that is allowed to use the disk group.  Before advancing the `COMPATIBLE`.`RDBMS` attribute, ensure that the values for the `COMPATIBLE` initialization parameter for all of the databases that access the disk group are set to at least the value of the new setting for `COMPATIBLE`.`RDBMS`. For example, if the `COMPATIBLE` initialization parameters of the databases are set to either `11`.`1` or `11`.`2`, then `COMPATIBLE`.`RDBMS` can be set to any value between `10`.`1` and `11`.`1` inclusively.  For Oracle ASM in Oracle Database 11g, `10`.`1` is the default setting for the `COMPATIBLE`.`RDBMS` attribute when using the SQL `CREATE` `DISKGROUP` statement, the ASMCMD mkdg command, ASMCA Create Disk Group page, and Oracle Enterprise Manager Create Disk Group page.   
`CONTENT`.`CHECK` |  `true` or `false` |  Enables (`true`) or disables (`false`) content checking when performing data copy operations for rebalancing a disk group. You cannot set this attribute when creating a disk group.  The default value is dependent on the `COMPATIBLE.ASM` attribute and follows this rule: 

  * If `COMPATIBLE.ASM` > = 19.0.0.0.0, then `CONTENT.CHECK` defaults to `true`. 
  * If `COMPATIBLE.ASM` < 19.0.0.0.0, then `CONTENT.CHECK` defaults to `false`. 

Note: This rule is ONLY true for the creation of new diskgroups. If the
`COMPATIBLE.ASM` attribute of an existing diskgroup is updated to 19.0.0.0.0
or above, the `CONTENT.CHECK` attribute remains at its current value.  
`DISK_REPAIR_TIME` |  0 to 136 years  |  When disks are taken offline, Oracle ASM drops them after a default period of time. If both the `compatible.rdbms` and `compatible.asm` attributes are set to at least 11.1, you can set the `disk_repair_time` attribute in an `ALTER` `DISKGROUP` ... `SET` `ATTRIBUTE` statement to change that default period of time so that the disk can be repaired and brought back online. You cannot set this attribute when creating a disk group.  The time can be specified in units of minute (M) or hour (H). The specified time elapses only when the disk group is mounted. If you omit the unit, then the default is H. If you omit this attribute, and both `compatible.rdbms` and `compatible.asm` are set to at least 11.1, then the default is 12 H. Otherwise the disk is dropped immediately. You can override this attribute with an `ALTER` `DISKGROUP` ... `OFFLINE` `DISK` statement and the `DROP` `AFTER` clause.  Note: If a disk is taken offline using the current value of `disk_repair_time`, and the value of this attribute is subsequently changed, then the changed value is used by Oracle ASM in the disk offline logic.  See Also: The `ALTER` `DISKGROUP` ... [disk_offline_clause](ALTER-DISKGROUP.md#GUID-22D73AB6-7063-4627-A2ED-18D521ED2557__BABFJHFG) and [Oracle Automatic Storage Management Administrator's Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=OSTMG10044) for more information   
`FAILGROUP_REPAIR_TIME` |  <`number`>`m` (number of minutes) or <`number`>`h` (number of hours)  |  Specifies a default repair time for the failure groups in the disk group. The failure group repair time is used if Oracle ASM determines that an entire failure group has failed. The default value is 24 hours (`24h`).  If there is a repair time specified for a disk, such as with the `DROP` `AFTER` clause of the `ALTER` `DISKGROUP` `OFFLINE` `DISK` statement, then that disk repair time overrides the failure group repair time.  This attribute can only be set when altering a disk group and is only applicable to normal and high redundancy disk groups.  
`LOGICAL_SECTOR_SIZE` |  512, 4096, or 4`K` |  Sets the logical sector size of a disk group. This value specifies the smallest possible I/O that the disk group can accept. The default value is estimated from the disks that join the disk group. To set this disk group attribute during the creation of a disk group or to alter it after a disk group has been created, the `COMPATIBLE`.`ASM` disk group attribute must be set to `12`.`2` or higher.   
`PHYS_META_REPLICATED` |  `true` or `false` |  Tracks the replication status of a disk group. When the Oracle ASM compatibility of a disk group is advanced to 12.0 or higher, the physical metadata of each disk, including its disk header, free space table blocks and allocation table blocks, is replicated. The replication is performed online asynchronously. `PHYS_META_REPLICATED` is set to `true` by Oracle ASM if the physical metadata of every disk in the disk group has been replicated.  This disk group attribute is only defined in a disk group with the Oracle ASM disk group compatibility (`COMPATIBLE`.`ASM`) set to `12.0` and higher. This attribute is read-only and is intended for information only. You cannot set or change its value.   
`PREFERRED_READ.ENABLED` |  `true` or `false` |  In an Oracle extended cluster, which contains nodes that span multiple physically separated sites, the `PREFERRED_READ.ENABLED` disk group attribute controls whether preferred read functionality is enabled for a disk group. If preferred read functionality is enabled, then this functionality enables an instance to determine and read from disks at the same site as itself, which can improve performance. For extended clusters, the default value is `true`. For clusters that are not extended (only one physical site), preferred read is disabled (`false`). Preferred read status applies to extended, normal, high, and flex redundancy disk groups.  This disk group attribute is only defined in a disk group with the Oracle ASM disk group compatibility (`COMPATIBLE`.`ASM`) set to `12.2` and higher.   
`SECTOR_SIZE` |  512, 4096, or 4`K` |  Sets the physical sector size of a disk group. All disks in the disk group must have this physical sector size. The default value is obtained from the disks that join the disk group. To set this disk group attribute during the creation of a disk group, the `COMPATIBLE`.`ASM` and `COMPATIBLE`.`RDBMS` disk group attributes must be set to `11`.`2` or higher. To alter this disk group attribute after a disk group has been created, the `COMPATIBLE`.`ASM` disk group attribute must be set to `12`.`2` or higher.   
`THIN_PROVISIONED` |  `true` or `false` |  Enables (`true`) or disables (`false`) the functionality to discard unused storage space after a disk group rebalance is completed. The default value is `false`.   
`CONTENT_HARDCHECK` | `true` or `false` | `CONTENT_HARDCHECK` enables or disables Hardware Assisted Resilient Data (HARD) checking when performing data copy operations for rebalancing a disk group. This attribute can only be set when altering a disk group.   
  
Footnote 1

Specify at least the first two digits of a valid Oracle Database release
number. Refer to [Oracle Database Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN001) for information on specifying valid version
numbers. For example, you can specify `compatibility` as '11.2' or '12.1'.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG10045) for more information on managing these
attribute settings

Examples

The following example assumes that the `ASM_DISKSTRING` parameter is a
superset of `/devices/disks/c*`, `/devices/disks/c*` points to at least one
device to be used as an Oracle ASM disk, and the Oracle Database user has
read/write permission to the disks.

See Also:

[Oracle Automatic Storage Management Administrator's
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=OSTMG036) for information on Oracle ASM and using disk
groups to simplify database administration

Creating a Diskgroup: Example

The following statement creates an Oracle ASM disk group `dgroup_01` where no
redundancy for the disk group is provided by Oracle ASM and includes all disks
that match the `search_string`:

    
    
    CREATE DISKGROUP dgroup_01
      EXTERNAL REDUNDANCY
      DISK '/devices/disks/c*';


[← Previous](CREATE-DIRECTORY.md)

[Next →](create-domain.md)
