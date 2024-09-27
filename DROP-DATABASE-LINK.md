[Previous](DROP-DATABASE.md) [Next](DROP-DIMENSION.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: DROP CONTEXT to DROP JAVA](SQL-Statements-DROP-CONTEXT-to-DROP-JAVA.md)
  3. DROP DATABASE LINK 

## DROP DATABASE LINK

Purpose

Use the `DROP` `DATABASE` `LINK` statement to remove a database link from the
database.

See Also:

[CREATE DATABASE LINK](CREATE-DATABASE-
LINK.md#GUID-D966642A-B19E-449D-9968-1121AF06D793) for information on
creating database links

Prerequisites

A private database link must be in your own schema. To drop a `PUBLIC`
database link, you must have the `DROP` `PUBLIC` `DATABASE` `LINK` system
privilege.

Syntax

drop_database_link::=

![Description of drop_database_link.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/drop_database_link.gif)  
[Description of the illustration
drop_database_link.eps](img_text/drop_database_link.md)

Semantics

PUBLIC

You must specify `PUBLIC` to drop a `PUBLIC` database link.

dblink

Specify the name of the database link to be dropped.

Restriction on Dropping Database Links

You cannot drop a database link in another user's schema, and you cannot
qualify `dblink` with the name of a schema, because periods are permitted in
names of database links. Therefore, Oracle Database interprets the entire
name, such as `ralph.linktosales`, as the name of a database link in your
schema rather than as a database link named `linktosales` in the schema
`ralph`.

IF EXISTS

Specify `IF EXISTS` to drop an existing object.

Specifying `IF NOT EXISTS` with `DROP` results in `ORA-11544: Incorrect IF
EXISTS clause for ALTER/DROP statement`.

Examples

Dropping a Database Link: Example

The following statement drops the public database link named `remote`, which
was created in "[Defining a Public Database Link: Example](CREATE-DATABASE-
LINK.md#GUID-D966642A-B19E-449D-9968-1121AF06D793__I2133775)":

    
    
    DROP PUBLIC DATABASE LINK remote; 


[← Previous](DROP-DATABASE.md)

[Next →](DROP-DIMENSION.md)
