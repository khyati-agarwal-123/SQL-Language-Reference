[Previous](DROP-TYPE.md) [Next](DROP-USER.md) JavaScript must be enabled
to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [SQL Statements: DROP TABLE to LOCK TABLE](SQL-Statements-DROP-TABLE-to-LOCK-TABLE.md)
  3. DROP TYPE BODY 

## DROP TYPE BODY

Purpose

Object types are defined using PL/SQL. Refer to [Oracle Database PL/SQL
Language Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99988) for complete information on creating,
altering, and dropping object types.

Use the `DROP` `TYPE` `BODY` statement to drop the body of an object type,
varray, or nested table type. When you drop a type body, the object type
specification still exists, and you can re-create the type body. Prior to re-
creating the body, you can still use the object type, although you cannot call
the member functions.

Prerequisites

The object type body must be in your own schema or you must have the `DROP`
`ANY` `TYPE` system privilege.

Syntax

drop_type_body::=

![Description of drop_type_body.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_type_body.gif)  
[Description of the illustration
drop_type_body.eps](img_text/drop_type_body.md)

Semantics

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

schema

Specify the schema containing the object type. If you omit `schema`, then
Oracle Database assumes the object type is in your own schema.

type_name

Specify the name of the object type body to be dropped.

Restriction on Dropping Type Bodies

You can drop a type body only if it has no type or table dependencies.

Examples

Dropping an Object Type Body: Example

The following statement removes object type body `data_typ1`. See [Oracle
Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01379) for the example that creates this object
type.

    
    
    DROP TYPE BODY data_typ1;


[← Previous](DROP-TYPE.md)

[Next →](DROP-USER.md)
