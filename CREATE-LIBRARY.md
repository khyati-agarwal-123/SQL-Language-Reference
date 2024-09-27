[Previous](create-json-relational-duality-view.md) [Next](CREATE-LOCKDOWN-
PROFILE.md) JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ SQL Statements: CREATE JSON RELATIONAL DUALITY VIEW to CREATE SCHEMA](SQL-Statements-CREATE-LIBRARY-to-CREATE-SCHEMA.md)
  3. CREATE LIBRARY 

## CREATE LIBRARY

Purpose

Use the `CREATE` `LIBRARY` statement to create a schema object associated with
an operating-system shared library. The name of this schema object can then be
used in the `call_spec` of `CREATE` `FUNCTION` or `CREATE` `PROCEDURE`
statements, or when declaring a function or procedure in a package or type, so
that SQL and PL/SQL can call to third-generation-language (3GL) functions and
procedures.

See Also:

[CREATE FUNCTION](CREATE-FUNCTION.md#GUID-156AEDAC-
ADD0-4E46-AA56-6D1F7CA63306) and [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS008) for more information on functions and
procedures

Prerequisites

The `CREATE` `LIBRARY` statement is valid only on platforms that support
shared libraries and dynamic linking.

To create a library in your own schema, you must have the `CREATE` `LIBRARY`
system privilege. To create a library in another user's schema, you must have
the `CREATE` `ANY` `LIBRARY` system privilege.

To use the library in the `call_spec` of a `CREATE` `FUNCTION` statement, or
when declaring a function in a package or type, you must have the `EXECUTE`
object privilege on the library and the `CREATE` `FUNCTION` system privilege.
Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01370) for information on the `call_spec` of a
`CREATE` `FUNCTION` statement.

To use the library in the `call_spec` of a `CREATE` `PROCEDURE` statement, or
when declaring a procedure in a package or type, you must have the `EXECUTE`
object privilege on the library and the `CREATE` `PROCEDURE` system privilege.
Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS01373) for information on the `call_spec` of a
`CREATE` `PROCEDURE` statement.

To execute a procedure or function defined with the `call_spec` (including a
procedure or function defined within a package or type), you must have the
`EXECUTE` object privilege on the procedure or function (but you do not need
the `EXECUTE` object privilege on the library).

Syntax

Libraries are defined using PL/SQL. Therefore, the syntax diagram in this book
shows only the SQL keywords. Refer to [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS99948) for the PL/SQL syntax, semantics, and
examples.

create_library::=

![Description of create_library.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/create_library.gif)  
[Description of the illustration
create_library.eps](img_text/create_library.md)

(`plsql_library_source`: See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1950).)

Semantics

OR REPLACE

Specify `OR` `REPLACE` to re-create the library if it already exists. Use this
clause to change the definition of an existing library without dropping, re-
creating, and regranting object privileges granted on it.

Users who had previously been granted privileges on a redefined library can
still access the library without being regranted the privileges.

IF NOT EXISTS

Specifying `IF NOT EXISTS` has the following effects:

  * If the library does not exist, a new library is created at the end of the statement.

  * If the library exists, this is the library you have at the end of the statement. A new one is not created because the older one is detected.

You can have one of `OR REPLACE` or `IF NOT EXISTS` in a statement at a time.
Using both `OR REPLACE` with `IF NOT EXISTS` in the very same statement
results in the following error: `ORA-11541: REPLACE and IF NOT EXISTS cannot
coexist in the same DDL statement`.

Using `IF EXISTS` with `CREATE` results in `ORA-11543: Incorrect IF NOT EXISTS
clause for CREATE statement`.

[ EDITIONABLE | NONEDITIONABLE ]

Use these clauses to specify whether the library is an editioned or
noneditioned object if editioning is enabled for the schema object type
`LIBRARY` in `schema`. The default is `EDITIONABLE`. For information about
editioned and noneditioned objects, see [Oracle Database Development
Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=ADFNS99923).

plsql_library_source

See [Oracle Database PL/SQL Language
Reference](/pls/topic/lookup?ctx=en/database/oracle/oracle-
database/23/sqlrf&id=LNPLS1950) for the syntax and semantics of the
`plsql_library_source`.


[← Previous](create-json-relational-duality-view.md)

[Next →](CREATE-LOCKDOWN-PROFILE.md)
