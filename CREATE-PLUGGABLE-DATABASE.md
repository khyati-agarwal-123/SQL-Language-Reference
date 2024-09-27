[Previous](CREATE-PFILE.md) [Next](create-pmem-filestore.md) JavaScript
must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE PLUGGABLE DATABASE

## CREATE PLUGGABLE DATABASE

Purpose

Use the `CREATE` `PLUGGABLE` `DATABASE` statement to create a pluggable
database (PDB).

This statement enables you to perform the following tasks:

  * Create a PDB by using the seed as a template

Use the `create_pdb_from_seed` clause to create a PDB by using the seed in the
multitenant container database (CDB) as a template. The files associated with
the seed are copied to a new location and the copied files are then associated
with the new PDB.

  * Create a PDB by cloning an existing PDB 

Use the `create_pdb_clone` clause to create a PDB by copying an existing PDB
and then plugging the copy into the CDB. The files associated with the
existing PDB are copied to a new location and the copied files are associated
with the new PDB.

  * Create a PDB by plugging an unplugged PDB into a CDB

Use the `create_pdb_from_xml` clause to plug an unplugged PDB into a CDB,
using an XML metadata file.

  * Create a proxy PDB by referencing another PDB. A proxy PDB provides fully functional access to the referenced PDB.

Use the `create_pdb_clone` clause and specify `AS` `PROXY` `FROM` to create a
proxy PDB.

  * Create an application container, application seed, or application PDB

Use the `create_pdb_from_seed`, `create_pdb_clone`, or `create_pdb_from_xml
clause`. To create an application container, you must specify the `AS`
`APPLICATION` `CONTAINER` clause. To create an application seed, you must
specify the `AS` `SEED` clause.

Note:

A multitenant container database is the only supported architecture in Oracle
Database 21c and later releases. While the documentation is being revised,
legacy terminology may persist. In most cases, "database" and "non-CDB" refer
to a CDB or PDB, depending on context. In some contexts, such as upgrades,
"non-CDB" refers to a non-CDB from a previous release.

Note:

When a new PDB is established in a CDB, it is possible that the name of a
service offered by the new PDB will collide with an existing service name. The
namespace in which a collision can occur is that of the listener that gives
access to the CDB. Within that namespace, collisions are possible among the
names of CDB's default services, PDB's default services, and user-defined
services. For example, if two or more CDBs on the same computer system use the
same listener, and the newly established PDB has the same service name as
another PDB in these CDBs, then a collision occurs.

When you create a PDB, you can specify new names for any potential colliding
service names. See the clause [service_name_convert](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__SERVICE_NAME_CONVERT-5754C12A). If you discover a
service name collision after a PDB is created, you must not attempt to operate
the PDB that causes a collision with an existing service name. If the
colliding name is that of the PDB's default service, then you must rename the
PDB. If the colliding name is that of a user-created service within the PDB,
then you must drop that service and create one in its place, with a non-
colliding name, that has the same purpose and properties.

See Also:

  * [Oracle Multitenant Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MULTI) for more information on multi-tenant architecture and concepts. 

  * [ALTER PLUGGABLE DATABASE](ALTER-PLUGGABLE-DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7) and [DROP PLUGGABLE DATABASE](DROP-PLUGGABLE-DATABASE.md#GUID-4A663783-E184-417A-8BE1-703E1CDBA30B) for information on modifying and dropping PDBs 

Prerequisites

You must be connected to a CDB. The CDB must be open and in `READ` `WRITE`
mode.

To create a PDB or an application container, the current container must be the
root and you must have the `CREATE` `PLUGGABLE` `DATABASE` system privilege,
granted commonly.

To create an application seed or an application PDB, the current container
must be an application root, the application container must be open and in
`READ` `WRITE` mode, and you must have the `CREATE` `PLUGGABLE` `DATABASE`
system privilege, either granted commonly or granted locally in that
application container.

To specify the `create_pdb_clone` clause:

  * If `src_pdb_name` refers to a PDB in the same CDB, then you must have the `CREATE` `PLUGGABLE` `DATABASE` system privilege in the root of the CDB in which the new PDB will be created and in the PDB being cloned. 

  * If `src_pdb_name` refers to a PDB in a remote database, then you must have the `CREATE` `PLUGGABLE` `DATABASE` system privilege in the root of the CDB in which the new PDB will be created. In addition, the remote user must have the `CREATE` `PLUGGABLE` `DATABASE` system privilege in the PDB to which `src_pdb_name` refers. 

See [Oracle Multitenant Administratorâs Guide
](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MULTI-
GUID-B26D56E1-B958-444F-864C-8AFDFF1566A6) for more information on the
prerequisites to PDB creation.

Syntax

create_pluggable_database::=

![Description of create_pluggable_database.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pluggable_database.gif)  
[Description of the illustration
create_pluggable_database.eps](img_text/create_pluggable_database.md)

([create_pdb_from_seed::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBFIDF), [create_pdb_clone::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CCHDFDDG),
[create_pdb_from_xml::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHEJDJD))

create_pdb_from_seed::=

![Description of create_pdb_from_seed.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pdb_from_seed.gif)  
[Description of the illustration
create_pdb_from_seed.eps](img_text/create_pdb_from_seed.md)

([pdb_dba_roles::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHJEJCB),
[parallel_pdb_creation_clause::=](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__PARALLEL_PDB_CREATION-53B657E9),
[default_tablespace::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBCAJI), [file_name_convert::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CCHIICFG),
[service_name_convert::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__SERVICE_NAME_CONVERT-575466E9),
[pdb_storage_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBHJEI), [path_prefix_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CCHGABFD),
[tempfile_reuse_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBAFHJ), [user_tablespaces_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACEADIC),
[standbys_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACBFHBB), [logging_clause::=](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACGFJGB),
[create_file_dest_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACGJDFB))

pdb_dba_roles::=

![Description of pdb_dba_roles.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_dba_roles.gif)  
[Description of the illustration
pdb_dba_roles.eps](img_text/pdb_dba_roles.md)

parallel_pdb_creation_clause::=

![Description of parallel_pdb_creation_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/parallel_pdb_creation_clause.gif)  
[Description of the illustration
parallel_pdb_creation_clause.eps](img_text/parallel_pdb_creation_clause.md)

default_tablespace::=

![Description of default_tablespace.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/default_tablespace.gif)  
[Description of the illustration
default_tablespace.eps](img_text/default_tablespace.md)

([datafile_tempfile_spec::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CHDHEGJH),
[extent_management_clause::=](CREATE-DATABASE.md#GUID-
ECE717DF-F116-4151-927C-2E51BB9DD39C__BGEIBGJH))

pdb_storage_clause::=

![Description of pdb_storage_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_storage_clause.gif)  
[Description of the illustration
pdb_storage_clause.eps](img_text/pdb_storage_clause.md)

([size_clause::=](size_clause.md#GUID-E97FADC2-A6E1-4D68-9F79-DCA271B86517__CHDEAIID))

file_name_convert::=

![Description of file_name_convert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/file_name_convert.gif)  
[Description of the illustration
file_name_convert.eps](img_text/file_name_convert.md)

service_name_convert::=

![Description of service_name_convert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/service_name_convert.gif)  
[Description of the illustration
service_name_convert.eps](img_text/service_name_convert.md)

path_prefix_clause::=

![Description of path_prefix_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/path_prefix_clause.gif)  
[Description of the illustration
path_prefix_clause.eps](img_text/path_prefix_clause.md)

tempfile_reuse_clause::=

![Description of tempfile_reuse_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/tempfile_reuse_clause.gif)  
[Description of the illustration
tempfile_reuse_clause.eps](img_text/tempfile_reuse_clause.md)

user_tablespaces_clause::=

![Description of user_tablespaces_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/user_tablespaces_clause.gif)  
[Description of the illustration
user_tablespaces_clause.eps](img_text/user_tablespaces_clause.md)

standbys_clause::=

![Description of standbys_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/standbys_clause.gif)  
[Description of the illustration
standbys_clause.eps](img_text/standbys_clause.md)

logging_clause::=

![Description of logging_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/logging_clause.gif)  
[Description of the illustration
logging_clause.eps](img_text/logging_clause.md)

create_file_dest_clause::=

![Description of create_file_dest_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_file_dest_clause.gif)  
[Description of the illustration
create_file_dest_clause.eps](img_text/create_file_dest_clause.md)

create_pdb_clone::=

![Description of create_pdb_clone.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pdb_clone.gif)  
[Description of the illustration
create_pdb_clone.eps](img_text/create_pdb_clone.md)

([parallel_pdb_creation_clause::=](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__PARALLEL_PDB_CREATION-53B657E9),
[default_tablespace::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBCAJI), [pdb_storage_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CCHBHJEI),
[file_name_convert::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHIICFG), [service_name_convert::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__SERVICE_NAME_CONVERT-575466E9),
[path_prefix_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHGABFD), [tempfile_reuse_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CCHBAFHJ),
[user_tablespaces_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACEADIC), [standbys_clause::=](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACBFHBB),
[logging_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACGFJGB), [create_file_dest_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACGJDFB),
[keystore_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__KEYSTORE_CLAUSE-5AD7BB55),
[pdb_refresh_mode_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__PDB_REFRESH_MODE_CLAUSE-532F10A5))

keystore_clause::=

![Description of keystore_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/keystore_clause.gif)  
[Description of the illustration
keystore_clause.eps](img_text/keystore_clause.md)

pdb_refresh_mode_clause::=

![Description of pdb_refresh_mode_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_refresh_mode_clause.gif)  
[Description of the illustration
pdb_refresh_mode_clause.eps](img_text/pdb_refresh_mode_clause.md)

create_pdb_from_xml::=

![Description of create_pdb_from_xml.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pdb_from_xml.gif)  
[Description of the illustration
create_pdb_from_xml.eps](img_text/create_pdb_from_xml.md)

([source_file_name_convert::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHEJFID), [source_file_directory::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACIAJHI),
[file_name_convert::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHIICFG), [service_name_convert::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__SERVICE_NAME_CONVERT-575466E9),
[default_tablespace::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBCAJI), [pdb_storage_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CCHBHJEI),
[path_prefix_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHGABFD), [tempfile_reuse_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CCHBAFHJ),
[user_tablespaces_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACEADIC), [standbys_clause::=](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACBFHBB),
[logging_clause::=](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACGFJGB), [create_file_dest_clause::=](CREATE-
PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACGJDFB))

create_pdb_from_mirror_copy::=

![Description of create_pdb_from_mirror_copy.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pdb_from_mirror_copy.gif)  
[Description of the illustration
create_pdb_from_mirror_copy.eps](img_text/create_pdb_from_mirror_copy.md)

using_snapshot_clause ::=

![Description of using_snapshot_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/using_snapshot_clause.gif)  
[Description of the illustration
using_snapshot_clause.eps](img_text/using_snapshot_clause.md)

container_map_clause ::=

![Description of container_map_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/container_map_clause.gif)  
[Description of the illustration
container_map_clause.eps](img_text/container_map_clause.md)

pdb_snapshot_clause ::=

![Description of pdb_snapshot_clause.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/pdb_snapshot_clause.gif)  
[Description of the illustration
pdb_snapshot_clause.eps](img_text/pdb_snapshot_clause.md)

source_file_name_convert::=

![Description of source_file_name_convert.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/source_file_name_convert.gif)  
[Description of the illustration
source_file_name_convert.eps](img_text/source_file_name_convert.md)

source_file_directory::=

![Description of source_file_directory.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/source_file_directory.gif)  
[Description of the illustration
source_file_directory.eps](img_text/source_file_directory.md)

create_pdb_decrypt_from_xml::=

![Description of create_pdb_decrypt_from_xml.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_pdb_decrypt_from_xml.gif)  
[Description of the illustration
create_pdb_decrypt_from_xml.eps](img_text/create_pdb_decrypt_from_xml.md)

Semantics

pdb_name

Specify the name of the PDB to be created. The name must satisfy the
requirements listed in "[Database Object Naming Rules](Database-Object-Names-
and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA)". The first
character of a PDB name must be an alphabet character. The remaining
characters can be alphanumeric or the underscore character (`_`).

The PDB name must be unique in the CDB, and it must be unique within the scope
of all the CDBs whose instances are reached through a specific listener.

AS APPLICATION CONTAINER

Specify this clause to create an application container.

See Also:

[Creating and Removing Application Containers and Seeds
](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MULTI-
GUID-E2B95068-D16D-438D-9A0B-974540988990)

using_snapshot_clause

Specify this clause to create a PDB from an existing PDB snapshot that can be
identified by its name, SCN, or timestamp.

If you additionally specify SNAPSHOT COPY, then the new PDB will depend on the
existence of the specified PDB snapshot. This will affect your ability to drop
or purge the new PDB.

AS SEED

Specify this clause to create an application seed. The database assigns the
seed a name of the form `application_container_name``$SEED`.

An application container can have at most one application seed. The
application seed is optional, but, if it exists, you can use it to create
application PDBs quickly that match the requirements of the application
container. An application seed enables instant provisioning of application
PDBs that are created from it.

See Also:

[Creating and Removing Application Containers and
Seeds](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=MULTI-GUID-E2B95068-D16D-438D-9A0B-974540988990)

create_pdb_from_seed

This clause enables you to create a PDB by using the seed in the CDB as a
template.

See Also:

[Creating a PDB from Scratch](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=MULTI-GUID-CCA938BD-52BE-422C-86AF-576D3E02B96B)

ADMIN USER

Use this clause to create an administrative user who can be granted the
privileges required to perform administrative tasks on the PDB. For
`admin_user_name`, specify name of the user to be created. Use the `IDENTIFIED
BY` clause to specify the password for `admin_user_name`. Oracle Database
creates a local user in the PDB and grants the `PDB_DBA` local role to that
user.

pdb_dba_roles

This clause lets you grant one or more roles to the `PDB_DBA` role. Use this
clause to grant roles that have the privileges required by the administrative
user of the PDB. For `role`, specify a predefined role. For a list of
predefined roles, refer to [Oracle Database Security
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=DBSEG4414).

You can also use the `GRANT` statement to grant roles to the `PDB_DBA` role
after the PDB has been created. Until you have granted the appropriate
privileges to the `PDB_DBA` role, the `SYS` and `SYSTEM` users can perform
administrative tasks on a PDB.

parallel_pdb_creation_clause

This clause instructs the CDB to use parallel execution servers to copy the
new PDB's data files to a new location. This may result in faster creation of
the PDB.

PARALLEL

If you specify `PARALLEL`, then the CDB automatically chooses the number of
parallel execution servers to use. This is the default if the `COMPATIBLE`
initialization parameter is set to `12`.`2` or higher.

PARALLEL integer

Use integer to specify the number of parallel execution servers to use. The
CDB can ignore this setting, depending on the current database load and the
number of available parallel execution servers. If you specify a value of 0 or
1, then the CDB does not parallelize the creation of the PDB. This can result
in a longer PDB creation time.

default_tablespace

If you specify this clause, then Oracle Database creates a smallfile
tablespace and sets it as the default permanent tablespace for the PDB. Oracle
Database will assign the default tablespace to any non-`SYSTEM` user for whom
a different permanent tablespace is not specified. The `default_tablespace`
clause has the same semantics that it has for the `CREATE` `DATABASE`
statement. For full information, refer to [default_tablespace](CREATE-
DATABASE.md#GUID-ECE717DF-F116-4151-927C-2E51BB9DD39C__I2186890) in the
documentation on `CREATE` `DATABASE`.

pdb_storage_clause

Use this clause to specify storage limits for the PDB.

  * Use `MAXSIZE` to limit the amount of storage that can be used by all tablespaces in the PDB to the value specified with `size_clause`. This limit includes the size of data files and temporary files for tablespaces belonging to the PDB. Specify `MAXSIZE` `UNLIMITED` to enforce no limit. 

  * Use `MAX_AUDIT_SIZE` to limit the amount of storage that can be used by unified audit OS spillover (`.bin` format) files in the PDB to the value specified with `size_clause`. Specify `MAX_AUDIT_SIZE` `UNLIMITED` to enforce no limit. 

  * Use `MAX_DIAG_SIZE` to limit the amount of storage for diagnostics (trace files and incident dumps) in the Automatic Diagnostic Repository (ADR) that can be used by the PDB to the value specified with `size_clause`. Specify `MAX_DIAG_SIZE` `UNLIMITED` to enforce no limit. 

If you omit this clause, or specify `STORAGE` `UNLIMITED`, then there are no
storage limits for the PDB. This is equivalent to specifying `STORAGE`
`(MAXSIZE` `UNLIMITED` `MAX_AUDIT_SIZE` `UNLIMITED` `MAX_DIAG_SIZE`
`UNLIMITED`).

file_name_convert

Use this clause to determine how the database generates the names of files
(such as data files and wallet files) for the PDB.

  * For `filename_pattern`, specify a string found in names of files associated with the seed (when creating a PDB by using the seed), associated with the source PDB (when cloning a PDB), or listed in the XML file (when plugging a PDB into a CDB). 

  * For `replacement_filename_pattern`, specify a replacement string. 

Oracle Database will replace `filename_pattern` with
`replacement_filename_pattern` when generating the names of files associated
with the new PDB.

File name patterns cannot match files or directories managed by Oracle Managed
Files.

You can specify `FILE_NAME_CONVERT` `=` `NONE`, which is the same as omitting
this clause. If you omit this clause, then the database first attempts to use
Oracle Managed Files to generate file names. If you are not using Oracle
Managed Files, then the database uses the `PDB_FILE_NAME_CONVERT`
initialization parameter to generate file names. If this parameter is not set,
then an error occurs.

service_name_convert

Use this clause to rename the user-defined services of the new PDB based on
the service names of the source PDB. When the service name of a new PDB
conflicts with an existing service name in the CDB, plug-in violations can
result. This clause enables you to avoid these violations.

  * For `service_name`, specify the name of a service found in the PDB seed (when creating a PDB in an application container by using the application seed) or in the source PDB (when cloning a PDB or plugging a PDB into a CDB). 

  * For `replacement_service_name`, specify the replacement name for the service. 

Oracle Database will use the replacement service name for the service in the
PDB being created.

You can specify `SERVICE_NAME_CONVERT` `=` `NONE`, which is the same as
omitting this clause.

Restrictions on service_name_convert

The `service_name_convert` clause is subject to the following restrictions:

  * You cannot change the name of the default service for a PDB. The default service has the same name as the PDB.

  * You cannot specify this clause when you use the `create_pdb_from_seed` clause to create a PDB from the CDB seed, because the CDB seed does not have user-defined services. You can, however, specify this clause when you use the `create_pdb_from_seed` clause to create an application PDB from the application seed. 

path_prefix_clause

Use this clause to ensure that file paths for directory objects associated
with the PDB are restricted to the specified directory or its subdirectories.
This clause also ensures that the following files associated with the PDB are
restricted to the specified directory: the Oracle XML repository for the PDB,
files created with a `CREATE` `PFILE` statement, and the export directory for
Oracle wallets. You cannot modify the setting of this clause after you create
the PDB. This clause does not affect files created by Oracle Managed Files.

  * For `path_name`, specify the absolute path name of an operating system directory. The single quotation marks are required, with the result that the path name is case sensitive. Oracle Database uses `path_name` as a prefix for all file paths associated with the PDB. 

Be sure to specify `path_name` so that the resulting path name will be
properly formed when relative paths are appended to it. For example, on UNIX
systems, be sure to end `path_name` with a forward slash (`/`), such as:

    
        PATH_PREFIX = '/disk1/oracle/dba/salespdb/'
    

  * For `directory_object_name`, specify the name of a directory object that exists in the CDB root (`CDB$ROOT`). The directory object points to the absolute path to be used for `PATH_PREFIX`. 

  * If you specify `PATH_PREFIX` `=` `NONE`, then the relative paths for directory objects associated with the PDB are treated as absolute paths and are not restricted to a particular directory. 

Omitting the `path_prefix_clause` is equivalent to specifying `PATH_PREFIX`
`=` `NONE`.

After the `path_prefix_clause` is specified for a PDB, existing directory
objects might not work as expected, since the `PATH_PREFIX` string is always
added as a prefix to all local directory objects in the PDB. The
`path_prefix_clause` only applies to user-created directory objects. It does
not apply to Oracle-supplied directory objects.

tempfile_reuse_clause

When you create a PDB, Oracle Database associates temp files with the new PDB.
Depending on how you create the PDB, the temp files may already exist and may
have been previously used.

Specify `TEMPFILE` `REUSE` to instruct the database to format and reuse a temp
file associated with the new PDB if it already exists. If you specify this
clause and a temp file does not exist, then the database creates the temp
file.

If you do not specify `TEMPFILE` `REUSE` and a temp file to be associated with
the new PDB already exists, then the database returns an error and does not
create the PDB.

user_tablespaces_clause

This clause lets you specify the tablespaces to be made available in the new
PDB. The `SYSTEM`, `SYSAUX`, and `TEMP` tablespaces are available in all PDBs
and cannot be specified in this clause.

You can use this clause to separate the data for multiple schemas into
different PDBs.

  * Specify `tablespace` to make the tablespace available in the new PDB. You can specify more than one tablespace in a comma-separated list. 

  * Specify `ALL` to make all tablespaces available in the new PDB. This is the default. 

  * Specify `ALL` `EXCEPT` to make all tablespaces available in the new PDB, except the specified tablespaces. 

  * Specify `NONE` to make only the `SYSTEM`, `SYSAUX`, and `TEMP` tablespaces available in the new PDB. 

When the compatibility level of the CDB is `12.2` or higher, the tablespaces
that are excluded by this clause are created offline in the new PDB, and they
have no data files associated with them. When the compatibility level of the
CDB is lower than `12.2`, the tablespaces that are excluded by this clause are
offline in the new PDB, and all data files that belong to these tablespaces
are unnamed and offline.

{ SNAPSHOT COPY | NO DATA }

These clauses apply only when cloning a PDB with the `create_pdb_clone`
clause. By default, the database creates each tablespace to be made available
in the new PDB according to the settings specified for cloning the PDB. These
clauses allow you to override those settings as follows:

  * `SNAPSHOT` `COPY` \- Clone the tablespace using storage snapshots. 

  * `NO` `DATA` \- Clone the data model definition of the tablespace, but not the tablespace's data. 

{ COPY | MOVE | NOCOPY }

These clauses apply when you plug in a PDB with the `create_pdb_from_xml`
clause. By default, the database creates each tablespace to be made available
in the new PDB according to the settings specified for plugging in the PDB.
These clauses allow you to override those settings as follows:

  * `COPY` \- Copy the tablespace files to the new location. 

  * `MOVE` \- Move the tablespace files to the new location. 

  * `NOCOPY` \- Do not copy or move the tablespace files to the new location. 

standbys_clause

Use this clause to specify whether the new PDB is included in one or more
standby CDBs. If you include a PDB in a standby CDB, then during standby
recovery the standby CDB will search for the data files for the PDB. If the
data files are not found, then standby recovery will stop and you must copy
the data files to the correct location before you can restart recovery.

  * Specify `cdb_name` to include the new PDB in the specified standby CDB. You can specify more than one standby CDB name in a comma-separated list. 

  * Specify `ALL` to include the new PDB in all standby CDBs. This is the default. 

  * Specify `ALL` `EXCEPT` to include the new PDB in all standby CDBs, except the specified standby CDBs. 

  * Specify `NONE` to exclude the new PDB from all standby CDBs. When a PDB is excluded from all standby CDBs, the PDB's data files are unnamed and marked offline on all of the standby CDBs. Standby recovery will not stop if the data files for the PDB are not found on the standby. If you instantiate a new standby CDB after the PDB is created, then you must explicitly disable the PDB for recovery on the new standby CDB. 

You can enable a PDB on a standby CDB after it was excluded on that standby
CDB by copying the data files to the correct location, bringing the PDB
online, and marking it as enabled for recovery.

logging_clause

Use this clause to specify the default logging attribute for tablespaces
created within the PDB. The logging attribute controls whether certain DML
operations are logged in the redo log file (`LOGGING`) or not
(`NOLOGGING`).The default is `LOGGING`.

When creating a tablespace, you can override the default logging attribute by
specifying the [logging_clause](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__CJAICHIG) of the
`CREATE` `TABLESPACE` statement.

Refer to
[logging_clause](logging_clause.md#GUID-C4212274-5595-4045-A599-F033772C496E)
for a full description of this clause.

create_file_dest_clause

By default, a newly created PDB inherits its Oracle Managed Files settings
from the root. If the root uses Oracle Managed Files, then the PDB also uses
Oracle Managed Files. The PDB shares the same base file system directory for
Oracle Managed Files with the root and has its own subdirectory named with the
GUID of the PDB. If the root does not use Oracle Managed Files, then the PDB
also does not use Oracle Managed Files.

This clause lets you override the default behavior. You can enable or disable
Oracle Managed Files for the PDB and you specify a different base file system
directory or Oracle ASM disk group for the PDB's files.

  * Specify `NONE` to disable Oracle Managed Files for the PDB. 

  * Specify either `directory_path_name` or `diskgroup_name` to enable Oracle Managed Files for the PDB. 

Specify `directory_path_name` to designate the base file system directory for
the PDB's files. Specify the full path name of the operating system directory.
The directory must exist and Oracle processes must have appropriate
permissions on the directory. The single quotation marks are required, with
the result that the path name is case sensitive.

Specify `diskgroup_name` to designate the default Oracle ASM disk group for
the PDB's files.

If you specify a value other than `NONE`, then the database implicitly sets
the `DB_CREATE_FILE_DEST` initialization parameter with `SCOPE=SPFILE` in the
PDB.

HOST and PORT

These clauses are useful only if you are creating a PDB that you plan to
reference from a proxy PDB. This type of PDB is called a referenced PDB.

When creating a referenced PDB:

  * If the name of the listener is different from the host name of the PDB, then you must specify the `HOST` clause. For `hostname`, specify the fully qualified domain name of the listener. Enclose `hostname` in single quotation marks. For example: `'myhost.example.com'`. 

In an Oracle Real Application Clusters (Oracle RAC) environment, you can
specify for `hostname` any of the hosts for the PDB.

  * If the port number of the listener is not 1521, then you must specify the `PORT` clause. For `number`, specify the port number for the listener. 

A proxy PDB uses a database link to establish communication with its
referenced PDB. After communication is established, the proxy PDB communicates
directly with the referenced PDB without using a database link. The host name
and port number of the listener for the referenced PDB must be correct for the
proxy PDB to function properly.

See Also:

The clause [AS PROXY FROM](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__ASPROXYFROM-562EA9D6) of `create_pdb_clone` for
information on creating a proxy PDB

create_pdb_clone

This clause enables you to create a new PDB by cloning a source to a target
PDB. The source can be a PDB in the local CDB, or a PDB in a remote CDB. The
target PDB is the clone of the source.

If the source is a PDB in the local CDB, then the source PDB can be plugged in
or unplugged. If the source is a PDB in a remote CDB, then the source PDB must
be plugged in.

If the source is a PDB in a remote CDB, then the source and the CDB that
contains the target PDB must meet the following requirements:

  * They must have the same endian format.

  * They must have compatible character sets and national character sets, which means:

    * Every character in the source character set is available in the local CDB character set.

    * Every character in the source character set has the same code point value in the local CDB character set.

  * They must have the same set of database options installed.

Users in the PDB who used the default temporary tablespace of the source PDB
use the default temporary tablespace of the new PDB. Users who used non-
default temporary tablespaces in the PDB continue to use the same local
temporary tablespaces in the new PDB.

You can clone a united PDB or an isolated PDB with the same command. The only
difference is that the keystore password you must provide are for different
keystores.

Hot Clone a PDB: Example

    
    
       CREATE PLUGGABLE DATABASE CDB1_PDB2_CLONE FROM CDB1_PDB2
        KEYSTORE IDENTIFIED BY keystore_password

For a united PDB:

  * `keystore_password` is the `ROOT` keystore password. 

  * The wallet must be open in `ROOT`. 

For an isolated PDB:

  * `keystore_password` is the new keystore password for the PDB `CDB1_PDB2_CLONE`. 

  * The wallet must be open in `CDB1_PDB2_CLONE`. 

Clone a PDB: Example

United PDB

    
    
       CREATE PLUGGABLE DATABASE CDB1_PDB1_C AS CLONE USING '/tmp/cdb1_pdb3.pdb'
        KEYSTORE IDENTIFED BY keystore_password DECRYPT USING transport_secret

  * The wallet must be open in `ROOT`, if TDE is in use. 

  * If there are TDE keys in the `.pdb` file, you must specify `KEYSTORE IDENTIFED BY` and provide `transport_secret`. 

  * `keystore_password` is the `ROOT` keystore password. 

Isolated PDB

    
    
    CREATE PLUGGABLE DATABASE CDB1_PDB2_C AS CLONE USING '/tmp/cdb1_pdb2.pdb'

  * You need not specify `KEYSTORE IDENTIFED BY` or `transport_secret`. If specified, they are ignored. 

  * The wallet need not be open in `ROOT`. 

See Also:

[Cloning a PDB ](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=MULTI-GUID-05702CEB-A43C-452C-8081-4CA68DDA8007)

FROM

Use this clause to specify the source PDB. The files associated with the
source are copied to a new location and these copied files are then associated
with the new PDB.

The source PDB cannot be closed. It can be open as follows:

  * If the CDB that contains the source PDB (the source CDB) is in `ARCHIVELOG` mode and local undo mode, then the source PDB can be open in `READ` `WRITE` mode and fully functional during the cloning operation. This is called hot PDB cloning. 

  * If the source CDB is not in `ARCHIVELOG` mode, then the source PDB must be open `READ` `ONLY`. 

Specify the source PDBas follows:

  * If the source is a PDB in the local CDB, then use `src_pdb_name` to specify the name of the source PDB. You cannot specify `PDB$SEED` for `src_pdb_name`. Instead, use the [create_pdb_from_seed](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACEDDDF) clause to create a PDB by using the seed as a template. 

  * If the source is a PDB in a remote CDB, then use `src_pdb_name` to specify the name of the source PDB and `dblink` to specify the name of the database link to use to connect to the remote CDB. 

AS PROXY FROM

Use this clause to create a proxy PDB by referencing a different PDB, which is
referred to as the referenced PDB. The referenced PDB can be in the same CDB
as the proxy PDB or in a different CDB. A local proxy PDB is in the same CDB
as its referenced PDB, and a remote proxy PDB is in a different CDB than its
referenced PDB.

For `src_pdb_name``@``dblink`, specify the referenced PDB.

See Also:

[Creating a PDB as a Proxy PDB
](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MULTI-
GUID-4453DF44-5D16-4581-9CBF-0C7BCA85DE82)

default_tablespace

Use this clause to specify a permanent default tablespace for the PDB. Oracle
Database will assign the default tablespace to any non-`SYSTEM` user for whom
a different permanent tablespace is not specified. The tablespace must already
exist in the source PDB. Because the tablespace already exists, you cannot
specify the `DATAFILE` clause or the `extent_management_clause` when creating
a PDB with the `create_pdb_clone` clause.

pdb_storage_clause

Use this clause to specify storage limits for the new PDB. Refer to
[pdb_storage_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACJAAGI) for the full semantics of this clause.

file_name_convert

Use this clause to determine how the database generates the names of files for
the new PDB. Refer to [file_name_convert](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACHDCDF) for the
full semantics of this clause.

service_name_convert

Use this clause to determine how the database renames services for the new
PDB. Refer to [service_name_convert::=](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__SERVICE_NAME_CONVERT-575466E9) for the full
semantics of this clause.

path_prefix_clause

Use this clause to ensure that all directory object paths associated with the
PDB are restricted to the specified directory or its subdirectories. Refer to
[path_prefix_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHIIGHJ) for the full semantics of this clause.

tempfile_reuse_clause

Specify `TEMPFILE` `REUSE` to instruct the database to format and reuse a temp
file associated with the new PDB if it already exists. Refer to
[tempfile_reuse_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBGHCI) for the full semantics of this clause.

SNAPSHOT COPY

You can specify `SNAPSHOT` `COPY` only when cloning a PDB. The source PDB can
be in the local CDB or a remote CDB. The `SNAPSHOT` `COPY` clause instructs
the database to clone the source PDB using storage snapshots. This reduces the
time required to create the clone because the database does not need to make a
complete copy of the source data files.

When you use the `SNAPSHOT` `COPY` clause to create a clone of a source PDB
and the `CLONEDB` initialization parameter is set to `FALSE`, the underlying
file system for the source PDB's files must support storage snapshots. Such
file systems include Oracle Advanced Cluster File System (Oracle ACFS) and
Direct NFS Client storage.

When you use the `SNAPSHOT` `COPY` clause to create a clone of a source PDB
and the `CLONEDB` initialization parameter is set to `TRUE`, the underlying
file system for the source PDB's files can be any local file system, network
file system (NFS), or clustered file system that has Direct NFS enabled.
However, the source PDB must remain in open read-only mode as long as any
clones exist.

Direct NFS Client enables an Oracle database to access network attached
storage (NAS) devices directly, rather than using the operating system kernel
NFS client. If the PDB files are stored on Direct NFS Client storage, then the
following additional requirements must be met:

  * The source PDB files must be located on an NFS volume.

  * Storage credentials must be stored in a Transparent Data Encryption keystore.

  * The storage user must have the privileges required to create and destroy snapshots on the volume that hosts the source PDB files.

  * Credentials must be stored in the keystore using an `ADMINISTER` `KEY` `MANAGEMENT` `ADD` `SECRET` SQL statement. 

When you use the `SNAPSHOT` `COPY` clause to create a clone of a source PDB,
the following restrictions apply to the source PDB as long as any clones
exist:

  * It cannot be unplugged.

  * It cannot be dropped.

PDB clones created using the `SNAPSHOT` `COPY` clause cannot be unplugged.
They can only be dropped. Attempting to unplug a clone created using the
`SNAPSHOT` `COPY` clause results in an error.

For a PDB created using the `SNAPSHOT` `COPY` clause in an Oracle Real
Application Clusters (Oracle RAC) environment, each node that must access the
PDB's files must be mounted. For Oracle RAC databases running on Linux or UNIX
platforms, the underlying NFS volumes must be mounted. If the Oracle RAC
database is running on a Windows platform and using Direct NFS for shared
storage, then you must update the `oranfstab` file on all nodes with the
created volume `export` and `mount` entries.

Storage clones are named and tagged using the new PDB GUID. You can query the
`CLONETAG` column of `DBA_PDB_HISTORY` view to view clone tags for storage
clones.

keystore_clause

Specify this clause if the source database has encrypted data or a keystore
set.

If you want to create the PDB by cloning another PDB, and if the source
database has encrypted data or a TDE master encryption key that has been set,
then you must provide the keystore password of the target keystore in
`keystore_password` .

You can find if the source database has encrypted data by querying the
`DBA_ENCRYPTED_COLUMNS` data dictionary view or the `V$ENCRYPTED_TABLESPACES`
dynamic performance view.

You can use the `EXTERNAL STORE` clause instead of `keystore_password` to
clone a PDB that is using a united keystore. Note that you must configure the
TDE SEPS wallet first before you use this option.

You cannot use the `EXTERNAL STORE` clause for a PDB that is using an isolated
keystore.

You can set the password to a maximum length of 1024 bytes.

pdb_refresh_mode_clause

The `REFRESH` `MODE` clause applies only when cloning a PDB. The source PDB
must be in a remote CDB, that is, you must specify the source PDB using the
`FROM` `src_pdb_name``@``dblink` clause.

This clause lets you specify the refresh mode of the PDB. You can use this
clause to create a refreshable PDB. Changes in the source PDB can be
propagated to the refreshable PDB, either manually or automatically. This
operation is called a refresh. You can specify the following refresh modes:

  * `MANUAL` \- This mode allows you to refresh the refreshable PDB manually at any time by issuing an `ALTER` `PLUGGABLE` `DATABASE` `REFRESH` statement. 

  * `EVERY` `refresh_interval` `MINUTES` or `HOURS` – This mode instructs the database to refresh the refreshable PDB every `refresh_interval` of selected time units, minutes or hours. If you select `MINUTES`, the `refresh_interval` must be less than 3000. If you select `HOURS`, the `refresh_interval` must be less than 2000. This mode also allows you to refresh the PDB manually at any time by issuing an `ALTER` `PLUGGABLE` `DATABASE` `REFRESH` statement. 

  * `NONE` \- If you specify this mode, then the clone PDB is not a refreshable PDB. The database cannot refresh the PDB automatically and you cannot refresh the PDB manually. If you specify this mode, then you cannot later change the PDB into a refreshable PDB. This is the default. 

A refreshable PDB can be opened only in `READ` `ONLY` mode. A refreshable PDB
must be closed in order for a refresh to occur. If it is not closed when you
attempt to perform a manual refresh, then an error will occur. If it is not
closed when the database attempts an automatic refresh, then the refresh will
be deferred until the next scheduled refresh.

See Also:

  * `ALTER` `PLUGGABLE` `DATABASE` [REFRESH](ALTER-PLUGGABLE-DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__REFRESH-2AECEDD3) for information on refreshing a PDB manually 

  * `ALTER` `PLUGGABLE` `DATABASE` [pdb_refresh_mode_clause](ALTER-PLUGGABLE-DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__PDB_REFRESH_MODE_CLAUSE-531D291C) for information on changing the refresh mode of a PDB 

  * [Oracle Database Administratorâs Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ADMIN-GUID-B99FE87D-151B-4350-84B3-BB5E7150E414) for more information on refreshable PDBs 

RELOCATE

Use this clause to relocate a PDB from one CDB to another. The database first
clones the source PDB to the target PDB, and then removes the source PDB. The
database also moves the files associated with the PDB to a new location. This
operation is the fastest way to relocate a PDB with minimal down time. The
down time for the PDB is approximately the time required to copy the PDB's
files from their old location to their new location. The source PDB can be
open in `READ` `WRITE` mode and fully functional during the relocation
operation.

You can specify the availability level with the `AVAILABILITY` keyword. The
default availability is `NORMAL`. If you specify `AVAILABILITY` `MAX`, then
additional operations are performed to ensure a smooth migration of the
workload in a persistent connection between source and target.

In the `create_pdb_clone` clause, you must use the `FROM`
`src_pdb_name``@``dblink` syntax to identify the location of the source PDB.
For `src_pdb_name`, specify the name of the source PDB. For `dblink`, specify
a database link that indicates the location of the source PDB. The database
link must have been created in the CDB to which the PDB will be relocated. It
can connect either to the root of the remote CDB or to the remote PDB.

KEEP SOURCE

Specify `KEEP SOURCE` if you want to keep the source PDB and preserve it in an
unplugged state.

See Also:

[Relocating a PDB ](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=MULTI-GUID-75519361-3DA2-4558-A7E5-64BC16FAFC7D)

NO DATA

The `NO` `DATA` clause applies only when cloning a PDB. This clause specifies
that the source PDB's data model definition is cloned, but not the PDB's data.
The dictionary data in the source PDB is cloned, but all user-created table
and index data from the source PDB is discarded.

Restrictions on the NO DATA Clause

The following restrictions apply to the `NO` `DATA` clause:

  * The source PDB should be open in read only mode when you use the `NO` `DATA` clause to clone a PDB. 

  * You cannot specify `NO` `DATA` if the source PDB contains clustered tables, Advanced Queuing (AQ) tables, index-organized tables, or tables that contain abstract data type columns. 

HOST and PORT

These clauses are useful only if you are creating a PDB that you plan to
reference from a proxy PDB. This type of PDB is called a referenced PDB. Refer
to [HOST and PORT](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__HOST-562D36AD) for the full semantics of these
clauses.

create_pdb_from_xml

This clause enables you to create a PDB by plugging an unplugged PDB (the
source database) into a CDB (the target CDB). If the source database is an
unplugged PDB, then it may have been unplugged from the target CDB or a
different CDB.

The source database and the target CDB must meet the following requirements:

  * They must have the same endian format.

  * They must have compatible character sets and national character sets, which means:

    * Every character in the source database character set is available in the target CDB character set.

    * Every character in the source database character set has the same code point value in the target CDB character set.

  * They must have the same set of database options installed.

See Also:

  * [Plugging In an Unplugged PDB ](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=MULTI-GUID-3132C4E5-8734-458B-8B0C-EFC77A45FFA3)

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS73527) for more information on the `DBMS_PDB` package 

AS CLONE

Specify this clause only if the target CDB already contains a PDB that was
created using the same set of data files. The source files remain as an
unplugged PDB and can be used again. Specifying `AS` `CLONE` also ensures that
Oracle Database generates new identifiers, such as DBID and GUID, for the new
PDB.

USING

This clause lets you specify a file that contains information about the source
database that your are plugging in. For `filename`, specify the full path name
of the file. You can obtain this file in one of the following ways:

  * If the source database is an unplugged PDB, then the file was created by the `pdb_unplug_clause` of `ALTER` `PLUGGABLE` `DATABASE` as follows: 

    * If the filename ends with the extension .xml, then it is an XML file containing metadata about the PDB. In this case, you must ensure that the XML metadata file, as well as the PDB's data files, are in a location that is accessible to the CDB.

    * If the filename ends with the extension .pdb, then it is a PDB archive file. This is a compressed file that includes an XML file containing metadata about the PDB, as well as the PDB's data files. The PDB archive file must exist in a location that is accessible to the CDB. When you use a .pdb archive file, this file is extracted when you plug in the PDB, and the PDBâs files are placed in the same directory as the .pdb archive file. Therefore, the `source_file_directory` clause is not required. 

  * If the source database is a non-CDB, then you must create the XML metadata file using the `DBMS_PDB` package, and ensure that the XML metadata file, as well as the source non-CDB's data files, are in a location that is accessible to the CDB. 

See Also:

  * [pdb_unplug_clause](ALTER-PLUGGABLE-DATABASE.md#GUID-A29491AD-8F0F-4E52-9D94-57FC3FF8FBC7__PDB_UNPLUG_CLAUSEPDBSUNPLUGGING-2AEE4D78) of `ALTER` `PLUGGABLE` `DATABASE`

  * [Oracle Database PL/SQL Packages and Types Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=ARPLS73527) for more information on the `DBMS_PDB` package 

source_file_name_convert

Specify this clause only if the contents of the XML file do not accurately
describe the locations of the source files. If the files that must be used to
plug in the source database are no longer in the location specified in the XML
file, then use this clause to map the specified file names to the actual file
names.

  * For `filename_pattern`, specify the string for the location of the files as specified in the XML file. 

  * For `replacement_filename_pattern`, specify the string for the actual location that contains the files that must be used to create the PDB. 

Oracle Database will replace `filename_pattern` with
`replacement_filename_pattern` when searching for the source database files.

File name patterns cannot match files or directories managed by Oracle Managed
Files.

If the files that must be used to create the PDB exist in the location
specified in the XML file, you can either omit this clause or specify
`SOURCE_FILE_NAME_CONVERT=NONE`.

source_file_directory

Specify this clause only if the contents of the XML file do not accurately
describe the locations of the source files and the source files are all
present in a single directory. This clause is convenient when you have a large
number of data files and specifying a replacement file name pattern for each
file using the `source_file_name_convert` clause is not feasible.

  * For `directory_path_name`, specify the absolute path of the directory that contains the source files. The directory is scanned to find the appropriate files based on the unplugged PDB's XML file. 

You can specify this clause for configurations that use Oracle Managed Files
and for configurations that do not use Oracle Managed Files.

If the files that must be used to create the PDB exist in the location
specified in the XML file, you can either omit this clause or specify
`SOURCE_FILE_DIRECTORY=NONE`.

COPY

Specify `COPY` if you want the files listed in the XML file to be copied to
the new location and used for the new PDB. This is the default. You can use
the optional `file_name_convert` clause to use pattern replacement in the new
file names. Refer to [file_name_convert](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACHDCDF) for the
full semantics of this clause.

MOVE

Specify `MOVE` if you want the files listed in the XML file to be moved,
rather than copied, to the new location and used for the new PDB. You can use
the optional `file_name_convert` clause to use pattern replacement in the new
file names. Refer to [file_name_convert](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-EEA8-4BB7-A07F-78DC04DB1FFC__CACHDCDF) for the
full semantics of this clause.

If the storage locations are different mounts, or if the storage locations do
not support move at the OS or storage level, then the `MOVE` clause first
copies the files then deletes the originals.

NOCOPY

Specify `NOCOPY` if you want the files for the PDB to remain in their current
locations. Use this clause if there is no need to copy or move the files
required to plug in the PDB.

service_name_convert

Use this clause to determine how the database renames services for the new
PDB. Refer to [service_name_convert::=](CREATE-PLUGGABLE-
DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__SERVICE_NAME_CONVERT-575466E9) for the full
semantics of this clause.

default_tablespace

Use this clause to specify a permanent default tablespace for the PDB. Oracle
Database will assign the default tablespace to any non-`SYSTEM` user for whom
a different permanent tablespace is not specified. The `tablespace` must
already exist in the source database. Because the tablespace already exists,
you cannot specify the `DATAFILE` clause or the `extent_management_clause`
when creating a PDB with the `create_pdb_from_xml` clause.

pdb_storage_clause

Use this clause to specify storage limits for the new PDB. Refer to
[pdb_storage_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CACJAAGI) for the full semantics of this clause.

path_prefix_clause

Use this clause to ensure that all directory object paths associated with the
PDB are restricted to the specified directory or its subdirectories. Refer to
[path_prefix_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHIIGHJ) for the full semantics of this clause.

tempfile_reuse_clause

Specify `TEMPFILE` `REUSE` to instruct the database to format and reuse a temp
file associated with the new PDB if it already exists. Refer to
[tempfile_reuse_clause](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__CCHBGHCI) for the full semantics of this clause.

HOST and PORT

These clauses are useful only if you are creating a PDB that you plan to
reference from a proxy PDB. This type of PDB is called a referenced PDB. Refer
to [HOST and PORT](CREATE-PLUGGABLE-DATABASE.md#GUID-F2DBA8DD-
EEA8-4BB7-A07F-78DC04DB1FFC__HOST-562D36AD) for the full semantics of these
clauses.

create_pdb_from_mirror_copy

Specify this clause to create a pluggable database `new_pdb_name` using the
prepared files of the mirror copy `mirror_name`. The new PDB will be split
from the source database using the prepared files created by the
`prepare_clause`.

  * You must execute this clause from the root container.

  * The meaning of the other optional parameters remains unchanged by this clause.

  * You can only split one database from a prepared mirror copy. If you want to create additional splits, you must prepare a new mirror copy.

  * You can specify the database link name after you have specifed the mirror copy name in the `prepare_clause` of the `ALTER PLUGGABLE DATABASE` statement. In addition, the current CDB name should match the target CDB name specified in the `prepare_clause`. You must be a valid user in the CDB being referenced by the database link with the system privileges `CREATE SESSION` and `CREATE PLUGGABLE DATABASE`. 

  * If the database link name is omitted, then the base PDB name is looked up in the current CDB.

using_snapshot_clause

Specify this clause to create a PDB using an existing PDB snapshot that can be
identified by its name, SCN, or timestamp.

If you create a PDB specifying `SNAPSHOT` `COPY`, then the new PDB will depend
on the existence of the PDB snapshot. This will affect your ability to drop or
purge the PDB.

container_map_clause

Specify this clause in CDB Root, Application Root or both to dynamically
update changes as they happen to the new PDB.

You must note the following points with container maps:

  * The `container_map_clause` is optional. 

  * The `add_partition_clause` will add a new partition to the container map defined in the Root (CDB Root and/or Application Root) of the new PDB. 

  * The `split_partition_clause` will split an existing partition of the container map defined in the Root (CDB Root and/or Application Root) of the new PDB. 

  * In the absence of `add_partition_clause` and `split_partition_clause`, container map defined in the Root of the new PDB is not updated. 

  * For PDB relocate, container map defined in the Root (CDB Root and/or Application Root) of the source PDB are automatically updated to reflect the âdropâ of the source PDB.

  * Dynamic maintenance of container map defined using hash partitioning is not supported

Add a New Partition to a Range-Partitioned Container Map: Example

    
    
      CREATE PLUGGABLE DATABASE cdb1_pdb3
        ADMIN USER IDENTIFIED BY manager
        FILE_NAME_CONVERT=('cdb1_pdb0, cdb1_pdb3')
        CONTAINER_MAP UPDATE (ADD PARTITION cdb1_pdb3 VALUES LESS THAN (100));
        ALTER PLUGGABLE DATABASE cdb1_pdb3 OPEN

Split an Existing Partition of a Range-Partitioned Container Map to Create a
New Partition: Example

    
    
      CREATE PLUGGABLE DATABASE cdb1_pdb4
        ADMIN USER IDENTIFIED BY manager
        FILE_NAME_CONVERT=('cdb1_pdb0, cdb1_pdb4')
        CONTAINER_MAP UPDATE (SPLIT PARTITION cdb1_pdb3 
                                AT (50) 
                                INTO
                                (PARTITION cdb1_pdb3, PARTITION cdb1_pdb3)
        ALTER PLUGGABLE DATABASE cdb1_pdb4 OPEN

Verify Updated in Range-Partitioned Container Map : Example

    
    
      SELECT partition_name, high_value
        FROM dba_tab_partitions
        WHERE table_name='MAP' AND table_owner='SYS'

pdb_snapshot_clause

Specify this clause if you want to be able to create PDB snapshots.

  * `NONE` is the default. It means that no snapshots of the PDB can be created. 

  * `MANUAL` means that the PDB snapshot can only be created manually. 

  * If snapshot interval is specified, PDB snapshots will be created automatically at specified interval. In addition, a user will also be able to create PDB snapshots manually

  * If expressed in minutes, `snapshot_interval` must be less than 3000. 

  * If expressed in hours, `snapshot_interval` must be less than 2000. 

create_pdb_decrypt_from_xml

You must have the `SYSKM` privilege to execute this command.

For PDBs in united mode, the following restrictions apply:

  * You must specify the clause if you are using a TDE protected database. Otherwise it is optional.

  * You need not specify the clause for an isolated PDB.

  * The wallet must be open in `ROOT`. 

  * The wallet file is copied in all cases: `NOCOPY`, `COPY`, and `MOVE`. 

Plugging a PDB from an XML Metadata File: Example

    
    
    CREATE PLUGGABLE DATABASE CDB1_PDB2 USING '/tmp/cdb1_pdb2.xml' NOCOPY
    KEYSTORE IDENTIFIED BY keystore_password DECRYPT USING transport_secret

Plugging a PDB from an Archive File: Example

    
    
    CREATE PLUGGABLE DATABASE CDB1_PDB1_1_C USING '/tmp/cdb1_pdb3.pdb' DECRYPT USING transport_secret

For PDBs in isolated mode, you need not specify `DECRYPT USING
transport_secret`. This is not required because the wallet file is copied
during the creation of an unplugged PDB from an XML file. if you are creating
a PDB from an archive file with the `.pdb` extension, the wallet file of the
PDB is available in the zipped archive.

If the `ewallet.p12` file already exists at the destination, a backup is
automatically initiated. The backup file has the following format:
`ewallet_PLGDB_2017090517455564.p12`.

Examples

Creating a PDB by Using the Seed: Example

The following statement creates a PDB `salespdb` by using the seed in the CDB
as a template. The administrative user `salesadm` is created and granted the
`dba` role. The default tablespace assigned to any non-`SYSTEM` users for whom
no permanent tablespace is assigned is `sales`. File names for the new PDB
will be constructed by replacing `/disk1/oracle/dbs/pdbseed/` in the file
names in the seed with `/disk1/oracle/dbs/salespdb/`. All tablespaces that
belong to `sales` must not exceed 2G. The location of all directory object
paths associated with `salespdb` are restricted to the directory
`/disk1/oracle/dbs/salespdb/`.

    
    
    CREATE PLUGGABLE DATABASE salespdb
      ADMIN USER salesadm IDENTIFIED BY password
      ROLES = (dba)
      DEFAULT TABLESPACE sales
        DATAFILE '/disk1/oracle/dbs/salespdb/sales01.dbf' SIZE 250M AUTOEXTEND ON
      FILE_NAME_CONVERT = ('/disk1/oracle/dbs/pdbseed/',
                           '/disk1/oracle/dbs/salespdb/')
      STORAGE (MAXSIZE 2G)
      PATH_PREFIX = '/disk1/oracle/dbs/salespdb/';

Cloning a PDB From an Existing PDB: Example

The following statement creates a PDB `newpdb` by cloning PDB `salespdb`. PDBs
`newpdb` and `salespdb` are in the same CDB. Because no storage limits are
explicitly specified, there is no limit on the amount of storage for `newpdb`.
The files are copied from `/disk1/oracle/dbs/salespdb/` to
`/disk1/oracle/dbs/newpdb/`. The location of all directory object paths
associated with `newpdb` are restricted to the directory
`/disk1/oracle/dbs/newpdb/`.

    
    
    CREATE PLUGGABLE DATABASE newpdb FROM salespdb
      FILE_NAME_CONVERT = ('/disk1/oracle/dbs/salespdb/', '/disk1/oracle/dbs/newpdb/')
      PATH_PREFIX = '/disk1/oracle/dbs/newpdb';

Plugging a PDB into a CDB: Example

The following statement plugs the PDB `salespdb`, which was previously
unplugged, into the CDB. The details about the metadata describing `salespdb`
are stored in the XML file `/disk1/usr/salespdb.xml`. The XML file does not
accurately describe the current locations of the files. Therefore, the
`SOURCE_FILE_NAME_CONVERT` clause is used to indicate that the files are in
`/disk2/oracle/dbs/salespdb/`, not `/disk1/oracle/dbs/salespdb/`. The `NOCOPY`
clause indicates that the files are already in the correct location. All
tablespaces that belong to `sales` must not exceed 2G. A file with the same
name as the temp file specified in the XML file exists in the target location.
Therefore, the `TEMPFILE` `REUSE` clause is required.

    
    
    CREATE PLUGGABLE DATABASE salespdb
      USING '/disk1/usr/salespdb.xml'
      SOURCE_FILE_NAME_CONVERT =
        ('/disk1/oracle/dbs/salespdb/', '/disk2/oracle/dbs/salespdb/')
      NOCOPY
      STORAGE (MAXSIZE 2G)
      TEMPFILE REUSE;


[← Previous](CREATE-PFILE.md)

[Next →](create-pmem-filestore.md)
