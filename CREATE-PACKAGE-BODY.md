[Previous](CREATE-PACKAGE.md) [Next](CREATE-PFILE.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE PACKAGE BODY 

## CREATE PACKAGE BODY

Purpose

Package bodies are defined using PL/SQL. Therefore, this section provides some
general information but refers to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01372) for details of syntax and semantics.

Use the `CREATE` `PACKAGE` `BODY` statement to create the body of a stored
package, which is an encapsulated collection of related procedures, stored
functions, and other program objects stored together in the database. The
package body defines these objects. The package specification, defined in an
earlier `CREATE` `PACKAGE` statement, declares these objects.

Packages are an alternative to creating procedures and functions as standalone
schema objects.

See Also:

  * [CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-ADD0-4E46-AA56-6D1F7CA63306) and [CREATE PROCEDURE](CREATE-PROCEDURE.md#GUID-771879D8-BBFD-4D87-8A6C-290102142DA3) for information on creating standalone functions and procedures 

  * [CREATE PACKAGE](CREATE-PACKAGE.md#GUID-40636655-899F-47D0-95CA-D58A71C94A56) for a discussion of packages, including how to create packages 

  * [ALTER PACKAGE](ALTER-PACKAGE.md#GUID-47471C4C-03AB-4D78-A295-3D58C91102E0) for information on modifying a package 

  * [DROP PACKAGE](DROP-PACKAGE.md#GUID-FAE96214-2ED0-4130-8ACA-A077C7A90B23) for information on removing a package from the database 

Prerequisites

To create or replace a package in your own schema, you must have the `CREATE`
`PROCEDURE` system privilege. To create or replace a package in another user's
schema, you must have the `CREATE` `ANY` `PROCEDURE` system privilege. In both
cases, the package body must be created in the same schema as the package.

To embed a `CREATE` `PACKAGE` `BODY` statement inside an Oracle Database
precompiler program, you must terminate the statement with the keyword `END-
EXEC` followed by the embedded SQL statement terminator for the specific
language.

See Also:

[Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01372)

Syntax

Package bodies are defined using PL/SQL. Therefore, the syntax diagram in this
book shows only the SQL keywords. Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01372) for the PL/SQL syntax, semantics, and
examples.

create_package_body::=

![Description of create_package_body.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_package_body.gif)  
[Description of the illustration
create_package_body.eps](img_text/create_package_body.md)

(`plsql_package_body_source`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS2181).)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to re-create the package body if it already exists. Use
this clause to change the body of an existing package without dropping, re-
creating, and regranting object privileges previously granted on it. If you
change a package body, then Oracle Database recompiles it.

Users who had previously been granted privileges on a redefined package can
still access the package without being regranted the privileges.

See Also:

[ALTER PACKAGE](ALTER-PACKAGE.md#GUID-47471C4C-03AB-4D78-A295-3D58C91102E0)
for information on recompiling package bodies

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the package body does not exist, a new package body is created at the end of the statement.

  * If the package body exists, this is the package body you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

[ EDITIONABLE | NONEDITIONABLE ]

If you do not specify this clause, then the package body inherits
`EDITIONABLE` or `NONEDITIONABLE` from the package specification. If you do
specify this clause, then it must match that of the package specification.

plsql_package_body_source

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS2181) for the syntax and semantics of the
`plsql_package_body_source`.


[← Previous](CREATE-PACKAGE.md)

[Next →](CREATE-PFILE.md)
