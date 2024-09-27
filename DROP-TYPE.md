[Previous](DROP-TRIGGER.md) [Next](DROP-TYPE-BODY.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: DROP TABLE to LOCK TABLE](SQL-Statements-DROP-TABLE-to-LOCK-TABLE.md)
  3. DROP TYPE 

## DROP TYPE

Purpose

Object types are defined using PL/SQL. Refer to [Oracle Database PL/SQL
Language Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99989) for complete information on creating,
altering, and dropping object types.

Use the `DROP` `TYPE` statement to drop the specification and body of an
object type, a varray, or a nested table type.

Prerequisites

The object type, varray, or nested table type must be in your own schema or
you must have the `DROP` `ANY` `TYPE` system privilege.

Syntax

drop_type::=

![Description of drop_type.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_type.gif)  
[Description of the illustration drop_type.eps](img_text/drop_type.md)

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

Semantics

schema

Specify the schema containing the type. If you omit `schema`, then Oracle
Database assumes the type is in your own schema.

type_name

Specify the name of the object, varray, or nested table type to be dropped.
You can drop only types with no type or table dependencies. This includes
tables in the recycle bin.

When you drop a type, any dependent objects such as subtypes are not placed in
the recycle bin and any former dependent objects in the recycle bin are
purged.

If `type_name` is a supertype, then this statement will fail unless you also
specify `FORCE`. If you specify `FORCE`, then the database invalidates all
subtypes depending on this supertype.

If `type_name` is a statistics type, then this statement will fail unless you
also specify `FORCE`. If you specify `FORCE`, then the database first
disassociates all objects that are associated with `type_name` and then drops
`type_name`.

See Also:

[ASSOCIATE STATISTICS](ASSOCIATE-STATISTICS.md#GUID-
BD02BA6A-32A7-4093-A6B6-BAE860C0F834) and [DISASSOCIATE
STATISTICS](DISASSOCIATE-
STATISTICS.md#GUID-6E9A7D93-E28A-469D-97AB-2BECC2EF3C43) for more
information on statistics types

If `type_name` is an object type that has been associated with a statistics
type, then the database first attempts to disassociate `type_name` from the
statistics type and then drops `type_name`. However, if statistics have been
collected using the statistics type, then the database will be unable to
disassociate `type_name` from the statistics type, and this statement will
fail.

If `type_name` is an implementation type for an indextype, then the indextype
will be marked `INVALID`.

If `type_name` has a public synonym defined on it, then the database will also
drop the synonym.

Unless you specify `FORCE`, you can drop only object types, nested tables, or
varray types that are standalone schema objects with no dependencies. This is
the default behavior.

See Also:

[CREATE INDEXTYPE](CREATE-
INDEXTYPE.md#GUID-4A7BD0EC-B3E5-4D1D-95C5-C8B52D01D8CE)

FORCE

Specify `FORCE` to drop the type even if it has dependent database objects.
Oracle Database marks `UNUSED` all columns dependent on the type to be
dropped, and those columns become inaccessible.

Note:

Oracle does not recommend that you specify `FORCE` to drop object types with
dependencies. These include dependent tables in the recycle bin. This
operation is not recoverable and could cause the data in the dependent tables
or columns to become inaccessible.

Refer to [Managing Tables](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADMIN-GUID-16E1CE4C-0189-4CF5-8047-F5039587D130) .

VALIDATE

If you specify `VALIDATE` when dropping a type, then Oracle Database checks
for stored instances of this type within substitutable columns of any of its
supertypes. If no such instances are found, then the database completes the
drop operation.

This clause is meaningful only for subtypes. Oracle recommends the use of this
option to safely drop subtypes that do not have any explicit type or table
dependencies.

Examples

Dropping an Object Type: Example

The following statement removes object type `person_t`. See [Oracle Database
PL/SQL Language Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01383) for the example that creates this object
type. Any columns that are dependent on person_t are marked `UNUSED` and
become inaccessible.

    
    
    DROP TYPE person_t FORCE;


[← Previous](DROP-TRIGGER.md)

[Next →](DROP-TYPE-BODY.md)
