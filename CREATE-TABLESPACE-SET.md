[Previous](CREATE-TABLESPACE.md) [Next](CREATE-TRIGGER.md) JavaScript must
be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: CREATE SEQUENCE to DROP CLUSTER](SQL-Statements-CREATE-SEQUENCE-to-DROP-CLUSTER.md)
  3. CREATE TABLESPACE SET

## CREATE TABLESPACE SET

Note:

This SQL statement is valid only if you are using Oracle Sharding. For more
information on Oracle Sharding, refer to [Oracle Database Administratorâs
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-DE8AF949-9F68-4C0C-9B5A-45401EF3C3D1).

Purpose

Use the `CREATE` `TABLESPACE` `SET` statement to create a tablespace set. A
tablespace set can be used in a sharded database as a logical storage unit for
one or more sharded tables and indexes.

A tablespace set consists of multiple tablespaces distributed across shards in
a shardspace. The database automatically creates the tablespaces in a
tablespace set. The number of tablespaces is determined automatically and is
equal to the number of chunks in the corresponding shardspace.

All tablespaces in a tablespace set are permanent bigfile tablespaces; a
tablespace set does not contain `SYSTEM`, undo, or temporary tablespaces. The
database automatically creates one data file for each tablespace. All
tablespaces in a tablespace set share the same attributes. You can modify
attributes for all tablespaces in a tablespace set with the `ALTER`
`TABLESPACE` `SET` statement.

See Also:

[ALTER TABLESPACE SET](ALTER-TABLESPACE-
SET.md#GUID-63FEDE73-C1F1-4B7A-98ED-8C34C4073549) and [DROP TABLESPACE
SET](DROP-TABLESPACE-SET.md#GUID-B14EC4C4-87C2-4E79-AB1A-044B620DF1FE)

Prerequisites

You must be connected to a shard catalog database as an SDB user.

You must have the `CREATE` `TABLESPACE` system privilege.

Syntax

create_tablespace_set::=

![Description of create_tablespace_set.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_tablespace_set.gif)  
[Description of the illustration
create_tablespace_set.eps](img_text/create_tablespace_set.md)

permanent_tablespace_attrs::=

![Description of permanent_tablespace_attrs.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/permanent_tablespace_attrs.gif)  
[Description of the illustration
permanent_tablespace_attrs.eps](img_text/permanent_tablespace_attrs.md)

([file_specification::=](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688__CJADEBBF),
See the following clauses of `CREATE` `TABLESPACE`:
[logging_clause::=](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2146497),
[tablespace_encryption_clause::=](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__TABLESPACE_ENCRYPTION_CLAUSE-5ADA8599),
[default_tablespace_params::=](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__DEFAULT_TABLESPACE_PARAMS-5ADA60FC),
[extent_management_clause::=](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2150446),
[segment_management_clause::=](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2146541),
[flashback_mode_clause::=](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__I2185336))

Semantics

tablespace_set

Specify the name of the tablespace set to be created. The name must satisfy
the requirements listed in [Database Object Naming Rules](Database-Object-
Names-and-Qualifiers.md#GUID-75337742-67FD-4EC0-985F-741C93D918DA).

IN SHARDSPACE

Specify this clause if you are using composite sharding. For
`shardspace_name`, specify the name of the shardspace in which the tablespace
set is to be created.

Omit this clause if you are using system-managed sharding. In this case, the
tablespace set is created in the default shardspace for the sharded database.

USING TEMPLATE

The `USING` `TEMPLATE` clause allows you to specify attributes for the
tablespaces in the tablespace set.

The `DATAFILE` and `permanent_tablespace_attrs` clauses have the same
semantics here as for the `CREATE` `TABLESPACE` statement, with the following
exceptions:

  * For the `DATAFILE` `file_specification` clause, you can specify only the `SIZE` clause and the `autoextend_clause`. 

  * You cannot specify the `MINIMUM` `EXTENT` `size_clause`. 

  * For the `segment_management_clause`, you can specify only `SEGMENT` `SPACE` `MANAGEMENT` `AUTO`. The `MANUAL` setting is not supported. 

See Also:

[file_specification](file_specification.md#GUID-580FA726-F712-4410-90CF-783A2DA89688)
and [permanent_tablespace_attrs](CREATE-
TABLESPACE.md#GUID-51F07BF5-EFAF-4910-9040-C473B86A8BF9__PERMANENT_TABLESPACE_ATTRS-2B5BC183)
in the documentation on `CREATE` `TABLESPACE` for the full semantics of these
clauses

Examples

Creating a Tablespace Set: Example

The following statement creates tablespace set `ts1`:

    
    
    CREATE TABLESPACE SET ts1
      IN SHARDSPACE sgr1 
      USING TEMPLATE
      ( DATAFILE SIZE 100m
        EXTENT MANAGEMENT LOCAL
        SEGMENT SPACE MANAGEMENT AUTO
      );


[← Previous](CREATE-TABLESPACE.md)

[Next →](CREATE-TRIGGER.md)
